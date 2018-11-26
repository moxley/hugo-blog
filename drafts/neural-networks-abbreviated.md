# Neural Networks

An artificial neural network is inspired by biological neural networks found in
the nervous systems of animals. It is composed of interconnected neurons. In
modern literature about the subject, you'll typically see the term "neural network"
instead of "artificial neural network". You'll also see the abbreviations "NN"
for "neural network" and "ANN" for "artificial neural network".

Seen from the highest level, a neural network is composed of three main parts:
the input layer, output layer, and hidden layers. It's like a big, mathematical
function, where the input layer receives the function's arguments, the hidden
layers is the function itself, and the outputs return the function's value.
Data flows from input, through the hidden layers, to the output.

Each layer consists of a set of neurons. The neurons are connected to the
neurons from the layer before it. Each neuron itself is a function, taking
input values, and producing a single output value. The output value is then
copied and fed into the neurons of the layer that follows.

The nature of a neuron's function is beyond the scope of this document, but
one concept you should be familiar with is the concept of weights and biases.
The neuron input has a corresponding "weight", that is multiplied with the input
value. The sum of the input values times each of their weights and then forwarded
to the rest of the function. Part of the "rest of the function" includes a
"bias", which is usually an additive factor of the function. Both the weight
and the biases are adjustable, and they are adjusted as part of the neural
network's training process.
