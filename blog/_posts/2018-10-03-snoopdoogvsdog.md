---
layout: post
comments: true
title:  "Snoop dogg vs dog"
excerpt: how to blog using jekyll
date:   2018-10-03 15:46:37 -0400
categories: blog
---

## Can deep Learning model differentiate between Snoop dogg vs a real dog? 

Recently, deep CNN based models have shown exceptional performance in classifying images. These system are sometimes better
than a human on specific tasks such as image classification, character recognition, Alpha Go. Tasks such as classification are evaluation on large datasets such
as ImageNet which has millions of images. There are 1000 object categories having thousand of images per category. These 
systems output a probabilty score *p* which shows how likely an image belongs to one of those classes. However, classification systems are not robust to the out-of-the-distribution examples. When presented  with examples that are beyond 1000
categories, they are still with some probability classified as one of the 1000 classes. Thus, these systems are
currenlty not well equipped to know how to say "this object is not similar to any of the object category that I have ever seen". However, it is very essential to know when a model is uncertain about such examples. In AI systems that are used for medical puposes, self driving cars or many other critical applications models must have some ways to know whether they are absolutely certain abouth their decision. So, to encourage researchers to formulate novel algorithms and proper evaluation strategies, we **( http://klab.cis.rit.edu/ )** have created a "Dogg vs dog" dataset that consists of 245,000 images with 15 types of dog classes and 20,000 images of the most famous Hip-Hop artist "Snoop Dogg" (https://en.wikipedia.org/wiki/Snoop_Dogg).

![png](/assets/dogg.jpg)

The train dataset will be released soon while the *test dataset will not be released* immediately for fair evaluation. Instead, participants
will be provided an online evaluation page where they can submit their predicitions and we will provide them the evalauation
results.

## More on the datsets and baselines will be released soon!!
