---
layout: post
title: "Introduction to Neural Networks"
date: '2018-10-07T18:38:56Z'
comments: true
categories: ['machine learning', 'ai']
published: false
---
## Machine Learning

Machine Learning is a technology involving computational "models" that are
trained to recognize patterns and relations in data. The models are then used to
make predictions about data they have never seen before. This is in contrast to
traditional software engineering, where the program is explicitly programmed how
to recognize patterns.

Machine Learning models solve types of problems where it is difficult to craft
programming code to recognize patterns, such as detecting whether a photo has a
aardvark in it. Some examples of complex or messy data are: images of
hard-written text, photographs and video, spoken human speech, stock market
behavior.

In practice, machine learning models have two phases of their existence. First,
the model is trained to recognize patterns in data. Then, the model is used to
make predictions about patterns in data it has never seen before.

## Neural Network

One class of machine learning models is the Neural Network (NN). Neural networks
are inspired by biological neural networks found in the nervous systems of
animals, especially those found in the brain. Even though they are inspired by
biological neural networks, artificial neural networks (ANNs) typically work
very differently from their biological counterparts.

Like biological neural networks, ANNs have neurons. Neurons connect together
to form a network. They have multiple inputs from which to receive signals
from other neurons. In a biological neuron, these inputs are called "dendrites".

A neuron has a single output. In a biological neuron, this output is called an
"axon". Even though the output signal initially follows one path, the path may
split into multiple paths before reaching other neurons.

## Layers

Artificial neuron networks are much more orderly than biological ones.
For the artificial kind, we typically group neurons together into layers. Layers
are stacked against each other, with neurons in one layer feeding signals to
the neurons in the next.

Artificial neural networks have a clear beginning and end. A layer called input
layer forms the beginning, and the output layer forms the end. In between these
two are layers referred to as "hidden" layers. Signals flow from input
layer, through the hidden layers, and finally out the output layer.

Layers connect to each other from their neuron outputs to the inputs of the
neurons in the next layer. Sometimes a single neuron in one layer will connect
to all the neurons in the next layer, and sometimes a neuron will only connect
to some of the neurons in the next layer. It depends on the type of layer. When
a neuron connects to all the neurons in the next layer, we call that "dense"
connectivity.

When we work with artificial neural networks, we don't typically work with
individual neurons. Instead, we define the layers of the network, then we
interact with the input and output layers of the network.

## Signals and Values

We just learned that neurons connect to each other, sending signals from one
to the next. In an artificial neural network, these signals are simply numbers,
usually real numbers that can be negative or positive.

In biological neural networks, signals are mathmatically continuous, while in ANNs, they are
discrete. A an artificial neuron receives a series of sets of numbers at its
inputs, with each input receiving a single number from the set. In turn, the
artificial neuron outputs a single number.

## Forward Propagation

Each layer in an ANN receives its input values and calculates their result
as the output values. It does this all in one step. After that, the next
layer in the network takes those values, and makes its own calculation.

The network processes values from one layer to the next until the output
layer is reached. This process is called Forward Propagation.

## Input Weights

Imagine a presidential council. Each council member gives their input to the
president. The president considers each council member by a certain degree, some
more than others, perhaps some even negatively, or perhaps not at all, before
making a decision.

Neurons work in a similar way, where the council members are the neuron's
inputs. The amount of consideration the president gives to each council member
is called the "weight". The decision the present provides is the neuron's
output value.

## Activation Function

A neuron takes all its input values and adds them together. It feeds the
resulting value into a so-called "activation function". The role of this
function is to decide whether to produce a meaningful output based on the
inputs. The greater the weighted inputs sum is, the more likely the activation
function is to produce a positive output. Conversely, the more negative the
weighted input sum is, the more likely the activation function (depending on the
type) is to product a negative output. If the weighted inputs is zero or
near zero, the activation function will likely produce exactly zero.

## Parameters

The input weights are a type of "parameter" of the neuron. Each weight counts
as a parameter. Some parameters change over time, as a network is "trained".
Weights are an example of a parameter that changes during training.

## Bias

Another parameter found in a neuron is "bias". Like weights, bias also factors
into the activation function. Neurons only have one bias parameter. The bias
value is simply added to the weighted sum of the inputs before being passed to
the activation function. The bias also changes during network training.

## Backpropagation

So how does a neural network get trained? The key process for training is called
backpropagation. In this process, we start with input values that are paired
with output values that we already know ahead of time are the correct output
values. For example, if we wanted a neural network to add two numbers together,
the network would input two numbers, such as 2 and 3, and, we already know
ahead of time that the answer is 5. Then we have the network calculate what
it thinks the answer should be. Let's say the network came up with 7, which
is off by 2.

Backpropagation is applied to the network for that incorrect answer. Not only is
the fact of the incorrect answer applied, but how off the answer was is applied
to it. How much the answer was off is called _loss_.

After backpropagation is applied, the next time the same inputs are given,
the answer will be slightly closer to the correct answer. As this process
is repeated over and over for the same inputs, the answer will approach
the correct answer. Interestingly, at first it will move towards the
correct answer very slowly, but as it iterates, it will increase its
rate of approach. Then, as it gets closer to the correct answer, it will
start to slow down again, slower and slower, never quite reaching the
perfect answer.

This is fine for the same given inputs, but it isn't a useful network. The power
of neural networks comes into play when the relationship between inputs and
outputs is messy. For example, one neural network model might be created to
predict home prices for a set of factors. These factors might include: how close
the property is to its city's downtown; what the average home price is for the
area sorrounding the property; what the crime rate is in the neighborhood.

the network propagates a set of
inputs progressively through the layers until the output. Then, the output
is compared to what we know the value should be. The goal is to produce
an output that matches exactly what we know it's supposed to be.

## Conclusion

Now, you should have enough of a theoretical foundation to start learning to
use neural networks.
