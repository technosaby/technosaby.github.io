---
layout : single 
title: "TD-λ"
excerpt: "Understanding TD-λ algorithm based on Richard Sutton's paper 'Learning to Predict by the Methods of Temporal Differences'"
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
permalink: /projects/rl_projects/td_lambda
#toc: true
classes: wide
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav

---

# Introduction
In 1988, Richard Sutton introduced a new type of incremental learning in his paper "Learning to Predict by the Methods of Temporal Differences"
to do prediction in a Reinforcement Learning (RL) environment. Sutton's techniques not only require less memory and computation than
conventional methods, but also provide more accurate predictions. Sutton named it TD-λ algorithm. In his paper he explains it in
relation to Supervised learning approaches. Temporal Difference or TD method (often called TD -λ) is a
model free technique which falls in the category of Value Based Learning. It is an incremental way to build up the
estimates of the values of different states (outcome based) across different episodes of learning. This
method of learning from incomplete episodes is also called bootstrapping. In TD-λ algorithms, the
bootstrapping can be controlled by the λ parameter, the value of which ranges from 0 to 1. If λ = 0 or TD(0), it
behaves like a one step lookahead, where the value of the state an agent is in, can be estimated by the sum of
the 1 step future reward and the estimated value of the next state. The idea is similar to the maximum likelihood
estimate, where the bootstrap happens over 1 step.


```python
import time
import matplotlib.pyplot as plt
import numpy as np
```

# Random Walk
Sutton introduces an absorbing Markov process based bounded random walk example which is a type of
multi-step problem which can be used as a platform to understand TD-λ algorithm. In this random walk problem, there are 7
states A,B,C,D,E,F,G and the agent starts from D and can take random steps towards left or right until
it reaches the terminal (absorbing) states A, with reward 0, or G, with reward 1.

The below imagee explains a Random Walk Example, with absorbing states as A,G (in red) and B,C,D,E,F as non-terminal states(in black). The black
arrows show the path the agent can transition to while starting from D. The blue lines show a sample random walk, D->E->F->G.
![randomwalk](/assets/images/rl_assets/randomwalk.png "Random Walk")


```python
def random_walk():
    start_state = 3
    start_vector = np.array([[0, 0, 1, 0, 0]]).T
    non_terminal_vectors = [start_vector]  # B,C,D,E,F
    episode = [start_state]
    rewards = []

    while True:
        if np.random.choice([0, 1]) == 0:  # Left
            start_state -= 1
        else:  # right
            start_state += 1
        episode.append(start_state)
        if start_state == 0:
            rewards.append(0)
            break
        elif start_state == 6:
            rewards.append(1)
            break
        else:  # Non-terminal states
            rewards.append(0)
            state = np.array([[0, 0, 0, 0, 0]])
            state[0][start_state - 1] = 1
            non_terminal_vectors.append(state.T)
    return episode, rewards, non_terminal_vectors
eps, rwds, _ = random_walk()
print("For episode: ", eps, " rewards are: ", rwds)
```

    For episode:  [3, 2, 3, 4, 3, 4, 3, 2, 1, 2, 3, 4, 3, 2, 3, 2, 3, 4, 5, 6]  rewards are:  [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]
    

# Dataset Creation
All the experiments are done on a dataset which contains episodes of bounded random walk organised in
the form of 100 training sets each containing 10 sequences.


```python
def createData(training_set_size = 100, sequence_size = 10):
    training_set = []
    np.random.seed(30)
    for t in range(training_set_size):
        sequences = []
        for i in range(sequence_size):
            one_episode, rewards_episode, non_terminal_vectors_episode = random_walk()
            sequences.append([np.array(one_episode), np.array(rewards_episode),
                              np.array(non_terminal_vectors_episode)])
        training_set.append(sequences)
    return training_set
dataset = createData(training_set_size=100, sequence_size=10)
```

# TD- λ
This is the heart of the algorithm and is known as the TD-λ algorithm. Sutton in his paper
introduced TD as a relation to classical supervised learning procedure, the Widrow-Hoff rule (Delta Rule)
which is similar to perceptron learning rule.
For each observation-outcome sequence, the learner produces a set of predictions (P1, P2, .. Pm)
which is an estimate of final outcome, z. It can be written as P(xt, w), where xt is the
observation at time step t and w is a vector of modifiable parameters or weight.
Error is calculated by taking the difference from z and Pt., which is the prediction at time step t.
The weight updates are collected over time steps in an episode, and after a complete sequence is
processed (z is available),the changes are updated at once. This makes supervised learning slow
in terms of learning. Another important aspect is that due to the accumulation of weight changes over time steps,
the update matrix becomes large and memory intensive. In case of TD, for non terminal states, the weight updates equation will be,

![nonterminal](/assets/images/rl_assets/rl_td_3.png "Equation for non terminal states")

while in case of terminal states as there is no Pt+1, it gets replaced by the final outcome or reward (z).

![terminal](/assets/images/rl_assets/rl_td_4.png "Equation for terminal states")

In the TD equation, the weight changes depend on the successive predictions Pt+1 and Pt or temporal difference between
successive predictions. Thus the update is small and light in memory. Till now, it was assumed that the weight updates
are made such that all predictions are altered to an equal amount. Now if controlled alterations are needed (for example,
more alterations  to recent predictions) then a variable λ is used to control it. This gave rise to the TD- λ algorithm.
The use of eligibility to calculate the  decay for the bootstrapping is another important aspect of the algorithm.


```python
def td_lambda(sequence, lambda_val, w, alpha = 0.01):
    rewards = sequence[1]
    x = sequence[2]
    delta_wt = np.zeros((1, 5))
    es = np.zeros((1,5))
    z = rewards[-1]
    for t, stateVector in enumerate(x):
        es[0][np.where(stateVector == 1)[0][0]] += 1
        if t == len(x) - 1: # Terminal State
            Pt = np.dot(w.T, x[t])
            delta_w = alpha * (z - Pt) * es
        else: # Non Terminal states
            # Pt+1 - Pt will be scalar
            p_t1 = np.dot(w.T, x[t + 1])
            p_t = np.dot(w.T, x[t])
            delta_w = alpha * (p_t1 - p_t) * es
        delta_wt += delta_w
        es = lambda_val * es
    return delta_wt
```

# Training by repeated presentations
In this experiment Sutton presents the dataset with 100 training sets each containing 10 sequences of random walk.
The Td-λ algorithm is run on each sequence of the training set till convergence is met, but the weight updates from
each sequence of the training set are not passed to the actual weight. Instead the weight updates are done only
when a training set is completed. To test the power of convergence, the initial weights are set to [0.9,0.7,0.5,0.3,0.1]
such that they are just opposite to ideal values. This test is run with a very low learning rate (𝛼 = 0.01) for different values of λ.
The Root Means Square Error (RMSE) is calculated from ideal weights and the final weight updates.
The RMSE values are plotted for different values of  λ.


```python
lambdaValues = [0, 0.1, 0.3, 0.5, 0.7, 0.9, 1]
alpha = 0.01
sigma = 0.001
idealWeights = np.arange(1, 6) / 6.0
errorValues = []
lambdaValIterations = []
for lambdaVal in lambdaValues:
    rmses = []
    iterations = 0
    start = time.time()
    for trainingSet in dataset:
        w = np.array([0.9,0.7,0.5,0.3,0.1])
        while True:
            iterations += 1
            results = []
            for sequence in trainingSet:
                results.append(td_lambda(sequence, lambdaVal, w, alpha))
            deltaW = np.sum(results, axis = 0)
            # https://sparrow.dev/numpy-norm/
            if np.linalg.norm(deltaW) < sigma:
                #if DEBUG: print("Convergence after iterations " + str(iterations))
                break
            w += deltaW[0]
        # Calculate Error
        rmse = (np.sum((idealWeights - w) ** 2) / 5) ** 0.5
        rmses.append(rmse)
    errorValues.append(np.mean(rmses))
    end = time.time()
    lambdaValIterations.append(end-start)

plt.plot(lambdaValues, errorValues, '-o')
plt.xlabel('λ',size=12)
plt.xticks([0,0.1,0.3,0.5,0.7,0.9,1.0])
plt.yticks([0.11, 0.12, 0.13, 0.14, 0.15, 0.16, 0.17])
#plt.ylim(0.1,0.18)
#plt.xlim(-0.05, 0.55)
plt.ylabel('ERROR', size=12)
plt.title('Reproduction of Figure 3', size=17)
plt.annotate('Widrow-Hoff', (0.65, errorValues[-1]), fontsize=14)
plt.show()
```


    
![png](/assets/images/rl_assets/rl_td_1.png)
    


The most important goal of doing this experiment is to get the intuition of convergence.
Here the weights updates are not being added to the main weights after each sequence, thus the learning is not so good and so the error is more.

# Analysing Learning Rate
In this experiment Sutton tries to summarize the performance of the algorithm based on different learning rates.
Here, the initial weights are set to 0.5, while in the previous experiment it was random. The weight updates happen
after every sequence of each training set and there is no convergence criteria, and the update is run once for each
training set. This experiment is done over different values of λ and 𝛼 to find the optimal learning rate with
minimum RMSE.


```python
alphas = np.arange(0, 0.75, 0.05) # alphas = np.arange(0, 15, 0.05)
ideal_weights = np.arange(1, 6) / 6.0
lambda_val_List = [0.0, 0.3, 0.8, 1.0]
error_values = dict()
for lambda_val in lambda_val_List:
    result_for_alphas = []
    for alpha in alphas:
        rms_errors = []
        #if DEBUG: print("lambda value " + str(lambdaVal), "learning rate " + str(alpha))
        for trainingSet in dataset:
            w = np.full(5, 0.5)
            for sequence in trainingSet:
                w += td_lambda(sequence, lambda_val, w, alpha)[0]
            rmse = (np.sum((ideal_weights - w) ** 2) / 5) ** 0.5
            rms_errors.append(rmse)
        result_for_alphas.append(np.mean(rms_errors))
    error_values[lambda_val] = result_for_alphas

for lambda_val in lambda_val_List:
    if lambda_val == 0.3:
        plt.plot(alphas[:10], error_values[lambda_val][:10], '-o', label='λ = {}'.format(lambda_val))
        plt.annotate('λ = {}'.format(lambda_val), (0.48, error_values[lambda_val][:10][-1]))
    elif lambda_val == 0.8:
        plt.plot(alphas[:10], error_values[lambda_val][:10], '-o', label='λ = {}'.format(lambda_val))
        plt.annotate('λ = {}'.format(lambda_val), (0.48, error_values[lambda_val][:10][-1]))
    elif lambda_val == 1.0:
        plt.plot(alphas[:9], error_values[lambda_val][:9], '-o', label='λ = {}'.format(lambda_val))
        plt.annotate('λ = {} (Widrow-Hoff)'.format(lambda_val), (0.2, error_values[lambda_val][:9][-1]))
    else: # 0.0
        plt.plot(alphas[:10], error_values[lambda_val][:10], '-o', label='λ = {}'.format(lambda_val))
        plt.annotate('λ = {}'.format(lambda_val), (0.48, error_values[lambda_val][:10][-1]))

plt.ylabel('ERROR', size=12)
plt.xlabel('α', size=12)
plt.ylim(0.0,0.7)
plt.xlim(-0.05, 0.55)
plt.xticks([0.0,0.1,0.2,0.3,0.4,0.5])
plt.yticks([0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7])
plt.title('Reproduction of Figure 4', size=17)
plt.legend(loc='upper left')
plt.show()
```


    
![png](/assets/images/rl_assets/rl_td_2.png)
    


In the output of this experiemnt when 𝛼 = 0, the error values for different values of λ are the same (around 0.25),
which shows that there is no learning. It is seen that the better results are obtained with the intermediary values.
The best value is seen when λ = 0.3 and 𝛼 = 0.2. If we see for all different values of λ, Windrow-Hoff performed worse
in all scenarios because it takes the final outcome of the sequence as the best estimate of its expected value, while in TD
(with smaller λ) predictions are made to match the expected value in every step of the sequence and thus there is learning
at every step of the sequence. Hence the learning is faster.

# Conclusion
As this paper was written in 1988, when RL might not be a very popular topic, Sutton tried to relate the concept
of TD-λ with Supervised Learning, such that readers can get the idea easily. Using the experiments in his paper,
Sutton explained the potential of TD algorithms while running using less memory and with less computation
yet generating more accurate results than conventional methods. The success of TD algorithms have made a big
contribution to fields of research. One of them is the TD-Gammon program developed in 1992 by Gerald
Tesauro which was not only in almost the same level to top human backgammon players, but also explored
strategies that humans might not have thought of before.

# References
1. Richard S. Sutton, Learning to Predict by the Methods of Temporal
Differences, GTE Laboratories Incorporated, 40 Sylvan Road,
Waltham, MA 02254, USA, 1988
2. Richard S Sutton and Andrew G Barto. Reinforcement learning: An
introduction. 2nd Ed. MIT press, 2020. url: http://incompleteideas.net/book/the-book-2nd.html.
3. TD-Gammon, Wikipedia, https://en.wikipedia.org/wiki/TD-Gammon

