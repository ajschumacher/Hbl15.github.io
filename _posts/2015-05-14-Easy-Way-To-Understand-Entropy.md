---
layout: post
title: Easy Way to Understand Entropy for Decision Tree.
---
 
How do you built a Decision Tree? 

Easiest answer: [sklearn.DecisionTreeClassifier](http://scikit-learn.org/stable/modules/tree.html)

Ok, now that I get that out of the way, how do you build a decision tree from scratch? Which features to choose as the root, as the nodes in the next level, as the node in the next next level...? 

I was curious about it, so I spend sometime reading wiki and some other literature. They were...--tough-- to get through. I did however to get through them after 5 hours @_@... To save time for you, this is my simple write up of how to build a decision tree:


### What is entropy?
Common answer: Entropy measure how mixed-up/impure your data is.

Answer with example: Say you look at a population and you care about gender. If you have 5 males and 5 females, your entropy is HIGH (=1) because your population is very well mixed (you are as likely to come across a male as coming across a female).

* And if you want some math equation:

S ={5 males, 5 females}

Entropy(S) = -p<sub>male</sub>log<sub>2</sub>p(male) - p<sub>female</sub>log<sub>2</sub>p(female)</sub>) 



Entropy(S) = -1/2log<sub>2</sub>(1/2) - 1/2log<sub>2</sub>(1/2) = 1 


 

