---
layout: "post"
title: "History of Parallel Distributed Processing"
author: "Allison Jia (’20)"
print_publication: true
tags: issue3
categories: Perspectives
related_image:
---

*PDP: Understanding How Neurons Model Human Decision Making Processes*

<!--excerpt-->
From a biological perspective, a neuron works by taking inputs from its dendrites and calculating a weighted sum of the dendritic inputs in the soma (cell body). The axon hillock (where soma connects to the axon) then checks whether the weighted sum is large enough to pass the threshold limit, where the neuron will fire if the threshold is passed and stay at rest if otherwise. Thus, the idea of the artificial neuron was derived from the principles of a biological neuron (Chandra).

The early development of artificial neural networks took off in 1943 when neurophysiologist Warren S. McCulloch and logician Walter H. Pitts published “A Logical Calculus of Ideas Immanent in Nervous Activity,” where they developed a mathematical model of an artificial neuron (also known as an MCP neuron) (Loiseau). The MCP neuron has a binary output of either 0 (the neuron will stay at rest) or 1 (the neuron will fire), determined by the binary n excitatory inputs and 1 maximum-effect inhibitory input. If the inhibitory value is 0, the model acts as a biological neuron: the values of the excitatory inputs will be summed together and placed through a step function, which outputs a 1 if the excitatory input sum exceeds the threshold limit and fires the neuron, or outputs a 0 if the input sum does not exceed the limit and keeps the neuron at rest. Otherwise, if the inhibitory value is 1, the neuron will never fire (Chandra).

In 1949, psychologist Donald Hebb introduced the idea of synaptic plasticity, laying the groundwork for the development of parallel distributed processing (PDP). Hebbian theory suggests that when two neurons fire together over and over again, their connection is strengthened and their efficiency increases (Hebb). 
Taking Hebbian theory into account, Cornell psychologist Frank Rosenblatt developed the first perceptron in 1958. Initially intended to be a machine instead of a program, Rosenblatt’s “Mark 1 Perceptron” was built for image recognition for 400 pixel images, but its implementation was essentially realized to be a trainable artificial neuron (Loiseau). By eliminating absolute inhibition and equal contributions of integer input values, Rosenblatt’s perceptron differed from the MCP neuron in that it could “learn” from the data by changing the amount of influence (weight) some inputs had over others. The perceptron also took a bias, or a constant added to the weighted sum of input values to help fit data to the model, and enabled inputs to be positive or negative to create excitatory or inhibitory effects respectively on the output. Moreover, Rosenblatt developed a supervised learning algorithm that allowed the perceptron to calculate the correct activation weights, or set of values determining the connection strength between neurons, directly from the training data. 

While Rosenblatt made significant contributions to improving the initial MCP neuron, many limitations still remained, primarily in that his perceptrons could only handle classification tasks for linearly separable classes (Ibanez). Here, linear separability refers to whether or not an n-1 dimensional surface (eg. 1D line) could separate different groups in an n dimensional space (eg. 2D space) (AI Shack). In 1969, Marvin Minsky and Seymour Papert published their book, Perceptrons: An Introduction to Computational Geometry, criticizing Rosenblatt’s work based on this restriction. Highlighting the limitations of single layer perceptrons (where input nodes are directly linked to output nodes through weights), Minsky and Papert proved that Rosenblatt’s perceptrons failed to learn the non-linearly separable XOR function, suggesting that the perceptron could not be applicable for even the most basic logical operations (Loiseau). Minsky’s disparaging comments about the limitations of Rosenblatt’s perceptrons combined with his prediction of impending doom for future perceptron research are often thought to have contributed to the “AI winter” of the 1970s (Dickson). 

Fortunately, David Rumelhart, Geoffrey Hinton, and Ronald Williams’ 1986 paper “Learning representations by back-propagating errors” marked the end of the 1970s AI Winter. Though initially theorized by Rosenblatt, these researchers developed an algorithm called “backpropagation” (Rumelhart, et al.). This algorithm calculates error by comparing the perceptron’s calculated output with the target output and relays the error backwards through all the perceptron’s layers, so that the perceptron can adjust the weights to minimize the error accordingly (CSU Lab). By establishing this backpropagation algorithm, Rumelhart, Hinton, and Williams successfully brought to life Rosenblatt’s idea of creating a feed-forward network (where information only moves in one direction from input to output), also known as a multilayer perceptron, based on backpropagation learning (Rumelhart, et al.).

Rumelhart, Hinton, and James McClelland went on to popularize PDP in their 1986 book, “Parallel Distributed Processing, Volume 1 Explorations in the Microstructure of Cognition: Foundations.” Consolidating the research done on PDP in the 1970s, they detailed the three general principles for the PDP model: the representation of information is distributed, memory and knowledge are stored within connections between neurons, and learning happens as connection strength changes gradually through experience (MIT Press). 

As the field of artificial intelligence is rapidly expanding in the 21st century, PDP continues to be the foundation for modern neural networks. Lying at the intersection of neuroscience, psychology, and computer science, PDP is vital to understanding the way neurons work to model human decision making processes.

Works Cited

Chandra, Akshay L. “McCulloch-Pitts Neuron — Mankind’s First Mathematical Model of a Biological Neuron,” https://towardsdatascience.com/mcculloch-pitts-model-5fdf65ac5dd1

Dickson, Ben. “What is the AI Winter?”, https://bdtechtalks.com/2018/11/12/artificial-intelligence-winter-history/

Hebb, Donald O. “The Organization of Behavior,” New York: Wiley, pg. 62. 

Ibanez, David. “Artificial Neural Networks - The Rosenblatt Perceptron,” https://www.neuroelectrics.com/blog/artificial-neural-networks-the-rosenblatt-perceptron/

Loiseau, Jean-Christophe B. “Rosenblatt’s Perceptron, the first modern neural network,” https://towardsdatascience.com/rosenblatts-perceptron-the-very-first-neural-network-37a3ec09038a

MIT Press. "PDP Research Group.", mitpress.mit.edu/contributors/pdp-research-group. 

CSU Lab. “History of the Perceptron” https://web.csulb.edu/~cwallis/artificialn/History.htm

Rumelhart, et al. "Learning Representations by Back-Propagating Errors,”
www.nature.com/articles/323533a0.pdf. Accessed 31 Oct. 2019.
