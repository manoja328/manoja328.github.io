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
than a human on task specific problems such as image recognition problems. These systems are evaluation on large datasets such
as ImageNet which has millions of images. There are 1000 object categories having thousand of images per category. These 
systems output a probabilty score "p" which shows how likely an image belongs to one of those classes. Classification systems
although are not robust to the out-of-the-distribution examples. When presented  with examples that are beyond 1000
categories, they are still given some probability of belonging to one of the 1000 classes. Thus, currenlty these systems are
not well equipped to know how to say "I have never seen such type of object before and it is not similar to any of the object 
category that i have ever seen".

To help researchers formulate novel algorithm and proper evaluation strategies,  we ( http://klab.cis.rit.edu/ ) have create
a "Dogg vs dog" dataset that consists of 245,000 images with 15 types of dog classes and 20,000 images of the most famous rapper
of the world "Snoop Dogg". The train dataset will be released soon while the test dataset *will not be released*. Instead, participants
will be provided an online evaluation page where they can submit their predicitions and we will provide them the evalauation
results.
