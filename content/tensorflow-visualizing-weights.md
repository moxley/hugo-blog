---
layout: post
title: "Visualizing Neuron Weights During Training"
date: '2018-11-26T03:49:14Z'
comments: true
categories: ["tensorflow"]
published: true
---

![weights during training](https://s3-us-west-2.amazonaws.com/moxicon-public/blog/tensorflow-visualizing-weights/two-weights-training-2.png)

I have a deep interest in knowing exactly how a neural network works. Not only do
I want to know the theory, I want to know-- in practice-- what's happening to the neuron's weights
as the network is being trained.

With TensorFlow, it took a lot of work and investigation to finally get to a point where I had something that
visualized weights being trained.

It seemed that TensorFlow was putting roadblocks at every possible path to getting the valuees of the
changing weights. For graph calculations-- the kind that TensorFlow is based on-- it's only possible
to read values in the graph during the graph's session. That's not an issue if you have a reference
to the session. But for models built with Keras, the session is created and destroyed behind
the scenes.

I saw that TensorFlow provides a way to save a model's state to a file. I tried digging
into that mechanism to get the chaning weights, but I only ran into deadends. I tried
using TensorFlow's "eager execution" mode, but I was not able to get any of my Keras-based
models to work.

It turns out the `tf.keras.Model` exposes a method called `get_weights()`. This
returns a Python array containing the weights and biases of the model. The
solution seems so easy in retrospect. Below is a demo of visualizing weights of
a very simple neural network.

## Getting Model Parameters During Training

Defined as a user story:

* As a Tensorflow programmer
* I want the ability to read a model's parameters during training
* So that I can visualize them

Let's create a very simple model with `tf.keras`. It will consist of a single
neuron on a single layer. It will have two inputs.

We're going to train the model to change its weights to `[1.0, 1.0]`, so that
the neuron becomes equivalent to its activation function.

First, import the necessary dependencies:

```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.contrib import eager as tfe
import numpy as np
import matplotlib.pyplot as plt
```

Create the model:

```python
# Sequential: https://www.tensorflow.org/api_docs/python/tf/keras/models/Sequential
model = keras.Sequential([
    keras.layers.Dense(1, input_shape=(2,), activation='tanh')
])

learning_rate = 0.5
optimizer = tf.train.GradientDescentOptimizer(learning_rate)
model.compile(optimizer=optimizer,
              loss='mean_squared_error',
              metrics=['accuracy'])
```

For a single-neuron network, we need an activation function that is completely
differentiatiable. In other words, the graph of the function shouldn't have any
horizontal lines or vertical lines or gaps in it. Otherwise, it could fail
to improve during training, depending on where the weights start off. `tanh`
fits the bill.

![tanh function](https://s3-us-west-2.amazonaws.com/moxicon-public/blog/tensorflow-visualizing-weights/tanh-function.png)

Generate the training data and corresponding labels:

```python
# This function is used to generate training labels
# We need to match neuron's activation function
def tanh(x):
    x_sum = np.sum(x)
    return np.tanh(x_sum)

train_data = np.random.random((500, 2))
train_labels = np.array(list(map(tanh, train_data)))
```

Let's see how the model performs before training:

```python
test_data = np.random.random((10, 2))
test_labels = np.array(list(map(tanh, test_data)))

test_loss, _ = model.evaluate(test_data, test_labels)
print('loss:', test_loss)
# loss: 0.19740669429302216
```

Not great, eh? That's what we expect for an untrained network.

Here's how we record the weights during training:

```python
# Records the weights throughout the training process
weights_history = []

# A custom callback
# https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/Callback
class MyCallback(keras.callbacks.Callback):
    def on_batch_end(self, batch, logs):
        weights, _biases = model.get_weights()
        w1, w2 = weights
        weights = [w1[0], w2[0]]
        print('on_batch_end() model.weights:', weights)
        weights_history.append(weights)


callback = MyCallback()
```

We create a custom callback that inherits from `keras.callbacks.Callback`.

When we call fit() to train the model, we pass in the callback:

```python
# fit(): https://www.tensorflow.org/api_docs/python/tf/keras/models/Sequential#fit
model.fit(train_data, train_labels, epochs=10,
          verbose=False, callbacks=[callback])
```

Watching the output, you'll see updated weights at the end of each training batch.
They should approach `1.0`.

Now, `weights_history` will have the historical weights.

Now let's see how well the model performs, after training:


```python
test_loss, _ = model.evaluate(test_data, test_labels)
print('loss:', test_loss)
# loss: 0.00015836639795452356
```

As loss of `0.0002` is much better than `0.2`.

Let's plot the historical weight values during training:

```python
plt.figure(1, figsize=(6, 3))
plt.plot(weights_history)
plt.show()
```

Test 1:
![weights during training 1](https://s3-us-west-2.amazonaws.com/moxicon-public/blog/tensorflow-visualizing-weights/two-weights-training-1.png)

Test 2:
![weights during training 3](https://s3-us-west-2.amazonaws.com/moxicon-public/blog/tensorflow-visualizing-weights/two-weights-training-3.png)

And that's it. We've successfully visualized neuron weights during training.
