---
layout: post
title: "Introduction to TensorFlow"
date: '2018-10-07T18:38:56Z'
comments: true
categories: ['tensorflow', 'machine learning', 'ai']
published: false
---
## Machine Learning Models

A model implements a technique for solving a machine learning problem. It
typically has inputs and outputs. Data flows from the inputs, through the model,
and out through the outputs. Using the model typically has two phases: training
and prediction. The goal of the model is to make it detect patterns in the
input. We say that the model makes a "prediction" about what patterns might in
the inputs. The prediction may be correct or incorrect, or somewhere in between.
The better the prediction, the more useful the model is.

## Tensorflow

"TensorFlow™ is an open source software library for high performance numerical
computation."

TensorFlow is much more than way to build neural networks. In the documentation,
you won't find the term "neuron", because that term doesn't fit with all
the types of models TensorFlow can represent. Instead, the documentation uses
agnostic terminology, such as "elements" or "units", instead of "neurons".

## Using Python

The most common programming language to use TensorFlow with is Python. This
article will focus entirely on using Python to program TensorFlow.

It is assumed you have some experience with Python. If not, check out the
guide on the Python language home page: https://www.python.org/

### Running TensorFlow on Own Machine

When running code that uses TensorFlow, you have a choice of running it on your
own machine, or running it in the cloud.

The advantage of running Python on your own machine is convenience. You don't
need to be connected to the internet, and you can save your work as simple
files on your computer's storage.

The disadvantage is that your computer probably doesn't have the special-purpose
hardware needed to run some of the more demanding machine learning models. A
machine learning model might take 10 minutes to train in the cloud, and the same
model may take 10 _hours_ to train locally on your computer.

The first several examples in the official TensorFlow tutorials aren't
demanding enough on hardware to make much of a difference between your computer
and the cloud, so you might be fine until you get further into the tutorials.

There are two recommended approaches to using Python on your computer for
working with TensorFlow:

- Using pip within a virtual environment
- Python in Docker

According to this article, it is highly recommended _not_ to use pip to
install TensorFlow and its dependencies: https://towardsdatascience.com/stop-installing-tensorflow-using-pip-for-performance-sake-5854f9d9eb0c

Directions for setting up a virtual environment [can be found
here](https://www.tensorflow.org/install/pip).

If you're very familiar with Docker, that might be a good way to go. But
otherwise, I recommend setting up a virtual Python environment.

Directions for Docker [can be found here](https://www.tensorflow.org/install/),
in the "Run a TensorFlow container" section.

### Running TensorFlow in the Cloud

Google provides services for easily running TensorFlow in the cloud. The best
and easiest is to use Google Colab. Google Colab is a web-based interactive
tool that lets you run code in the cloud, and it also lets your turn your code
into a living document by letting you add text content between bits of code.

## A Very Simple Neural Network

Now that we have a good foundation on what neural networks are, we're ready to
create our own neural network model with TensorFlow.

For the input weights, TensorFlow uses the term "kernel" to represent the input
weights together in a matrix.

This tutorial assumes you are inputting the sample code directly into the
Python interactive interpreter (aka, the REPL).

```python
import tensorflow.keras.layers as layers

# Need this for interactive use
tf.enable_eager_execution()

# Create a "Dense" layer with 3 nodes (neurons)
layer = layers.Dense(3)

# Check the input weights
# At this point, there are no inputs to the layer
layer.weights
# []
```

`tf.constant()` creates a tensor. A tensor is the basic building block behind
Tensorflow. It's a multidimensional array.
Here's we create a tensor for a one-dimensional array with the values 2, 3
The tensor has a "shape" of `(2,)`, which means it's a single dimensional
array with the first dimension having a dimensionality (length) of 2.

```python
tf.constant([2,3])
# <tf.Tensor: id=37, shape=(2,), dtype=int32, numpy=array([2, 3], dtype=int32)>
```

A layer is basically a function that takes its inputs as arguments.
We will use `tf.constant()` to construct an input.

When we call the layer as a function, it expects a batch of inputs. To keep
things simple, we'll use a batch size of one input.

Let's say we want the values 2 and 3 to be the input to the layer. There are
a couple things we need to do to pass those values to the layer function:

1. Convert the input (values) to floats.
2. Wrap the input in an array representing the batch.

Here's what that will look like:

```python
batch = tf.constant([[2.0, 3.0]])

# Call the layer
output = layer(batch)

# Here's what the output looks like:
output
# <tf.Tensor: id=64, shape=(1, 3), dtype=float32, numpy=array([[-2.2658331 ,  0.25054717, -1.0271099 ]], dtype=float32)>
```

The output is a Tensor. It has a unique ID. It has a a data type (`dtype`) of `float32`
Its value (`numpy`) is `array([[-2.2658331 ,  0.25054717, -1.0271099 ]], dtype=float32)`
Where did this random-looking values come from?
They are derived from the inputs and the input "weights".
The weights are created when the layer first learns what the input looks like.
During training, the weights will change slowly, usually towards a single ideal value.

What are the weight values?

```python
layer.weights
# [<tf.Variable 'dense_1/kernel:0' shape=(2, 3) dtype=float32, numpy=
# array([[ 0.14040971, -0.43764877,  0.0035274 ],
#        [-0.84888417,  0.37528157, -0.34472156]], dtype=float32)>, <tf.Variable 'dense_1/bias:0' shape=(3,) dtype=float32, numpy=array([0., 0., 0.], dtype=float32)>]
```

In the `numpy` value, there is a multidimensional array. The first dimension
has a length of 2. This represents the number of inputs.
The second dimension has a length of 3. This represents the number of neurons.
Each neuron has 2 weights. You might think that it makes sense that the
neuron's weights would all reside within the same array. That's actually not
the case. The weights are grouped by input instead.
