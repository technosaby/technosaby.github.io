---
layout : single 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/others_assets/cv_banner_image.jpg
title: "Face Recognition"
tagline: "Face recognition using PCA, (Ada)Boosting, and the Viola-Jones algorithm"
description: "This project implements face recognition using PCA, (Ada)Boosting, and the Viola-Jones algorithm. Here no library is used, instead they are implemented from scratch to understand their working techniques.This project focusses on these objectives:
* Learn the advantages and disadvantages of PCA, Boosting, and Viola-Jones.
* Learn how face detection/recognition work, explore the pros & cons of various techniques applied to this problem area.
* Identify the inherent challenges of working on these face detection methods."
permalink: /projects/cv/face_recognition
classes: wide
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---
# Project Goal 
This project implements face recognition using PCA, (Ada)Boosting, and the Viola-Jones algorithm. Here no library is used, instead they are implemented from scratch to understand their working techniques.

This project focusses on these objectives:
* Learn the advantages and disadvantages of PCA, Boosting, and Viola-Jones.
* Learn how face detection/recognition work, explore the pros & cons of various techniques applied to this problem area.
* Identify the inherent challenges of working on these face detection methods.

## Principal Component Analysis 
Principal component analysis (PCA) is a technique that converts a set of attributes into a smaller set of
attributes, thus reducing dimensionality. Applying PCA to a dataset of face images generates eigenvalues and
eigenvectors, in this context called eigenfaces. The generated eigenfaces can be used to represent any of the
original faces. By only keeping the eigenfaces with the largest eigenvalues (and accordingly reducing the
dimensionality) we can quickly perform face recognition.
In this section, PCA is used to identify people in face images. The Yalefaces dataset is used to recognize each individual person.

### Image of a mean face
Each image is read from the dataset and resized to a certain dimension. Then a data structure X is created that contains all resized images. Each row of this array is a flattened image. Now an array is used to obtain the mean face (𝜇) by averaging each image. 

![Average Face](/assets/images/others_assets/cv_mean_face.png)

## EigenFace
In this section, the eigenvectors and eigenvalues are used to determine the vectors with largest covariance. The top 10 eigenvectors (in descending order) based on their eigenvalues are given below.

![Eigen Face](/assets/images/others_assets/cv_eigen_face.png)

## Voila Jones Image Recognition
Haarlike features can be used to train classifiers restricted to using a single feature. The results from this process can be then applied in the boosting algorithm explained in the Viola-Jones paper. Here a dataset of images that contain faces are used and they are 
referred as positive examples. Additionally, a dataset of images is used which contain images of other objects and thus referred as negative examples.
The boosting algorithm is coded as discussed in the ViolaJones paper.

# Solution
[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/cv/ps06) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]