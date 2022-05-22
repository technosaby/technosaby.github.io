---
layout : single 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
title: "Chatbot"
tagline: "An AI based Chatbot to answer questions about a class syllabus"
description: "The goal of this project is to create a chatbot (your own Jill Watson) which is a text based agent (virtual Teacing Assistant) to answer questions about the class syllabus (in FAQ format). Using Natural Language Processing and Natural Language Understanding, the objective is to accept a question from the student (autograder) and select the best response from the FAQ. 
When a virtual TA responds with incorrect information it is very frustrating to the student.  So the student (autograder) will provide feedback to the agent on whether the response was correct. The agent is expected to learn from this additional data and improve as it is used. 
The goal for the project is to develop a classifier using Knowledge based AI (KBAI) techniques. There are many available libraries which makes like easier in this project. The usage of them are avoided so that a deeper understanding can be gained about the working mechanism.  KBAI as a subject deals with an AI agent doing reasoning to “think like humans”, I decided to go with finding sentence similarity based on semantic nets and corpus statistics. I took reference from “Sentence Similarity Based on Semantic Nets and Corpus Statistics by Yuhua Li, David McLean, Zuhair A. Bandar, James D. O’Shea, and Keeley Crockett” in modelling my AI agent"
permalink: /projects/ai/
author: Sabyasachi Ghosal
classes: wide
sidebar:
  nav: others_nav
---

# Goal of the project
The goal of this project is to create a chatbot (your own Jill Watson) which is a text based agent (virtual Teacing Assistant) to answer questions about the class syllabus (in FAQ format). Using Natural Language Processing and Natural Language Understanding, the objective is to accept a question from the student (autograder) and select the best response from the FAQ. 
When a virtual TA responds with incorrect information it is very frustrating to the student.  So the student (autograder) will provide feedback to the agent on whether the response was correct. The agent is expected to learn from this additional data and improve as it is used. 
The goal for the project is to develop a classifier using Knowledge based AI (KBAI) techniques. There are many available libraries which makes like easier in this project. The usage of them are avoided so that a deeper understanding can be gained about the working mechanism. 

# Solution Idea
The solution of this chat bot project is a type of Retrieval-Based model which uses a repository of KBAI FAQ corpus (predefined responses) and some kind of heuristics to pick an appropriate response based on the input and context. When a question is asked to the chat bot, it checks that if there exists a similar question in the KBAI FAQ corpus, if it is able to find the question, it provides the corresponding response for that matched question else it treats the question as an out of domain (OOD) question. So two questions (asked question, one from corpus) is compared to check if they are similar. 
Among the different similarity approaches, I have used a Text-based Similarity (a type of string similarity approach using calculation of cosine coefficients) based approach for implementing the bot.
This project implements an algorithm that takes the semantic information and word order information of sentences to calculate the semantic similarity using the lexical database and corpus statistics. This makes the model very generic and also makes it easily adaptable to different domains. KBAI as a subject deals with an AI agent doing reasoning to “think like humans”, I decided to go with finding sentence similarity based on semantic nets and corpus statistics. I took reference from “Sentence Similarity Based on Semantic Nets and Corpus Statistics by Yuhua Li, David McLean, Zuhair A. Bandar, James D. O’Shea, and Keeley Crockett” in modelling my AI agent. 


# Source Code & Report 

[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/ai/Chatbot) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]
