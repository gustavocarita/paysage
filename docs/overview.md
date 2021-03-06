# Neural networks and Boltzmann machines

There are two general classes of models in machine learning: discriminative
and generative. Discriminative models can be trained to *describe* data --
e.g., to label the objects in a picture. Generative models can be trained
to *simulate* data (and, also, to describe it).

[Boltzmann machines](https://en.wikipedia.org/wiki/Boltzmann_machine) are
a type of stochastic neural network that make excellent generative models.
A Boltzmann machine represents a probability distribution using a simple
function that can be trained from data by maximizing the log-likelihood
using gradient ascent. Computing the gradient is challenging, however,
because one has to compute averages with respect to the model distribution.

Paysage provides tools for training Boltzmann machines through
1) fast approximate inference algorithms (called "initialization methods")
and
2) inference based on sampling from the model distribution using sequential
Monte Carlo methods.

## Boltzmann machines with a single hidden layer

A hidden neuron captures an unobserved latent variable that controls the
interactions between visible neurons. The joint probability distribuiton
P(v, h) is determined from an energy function E(v, h) by
P(v, h) = exp(-E(v, h ))/Z where

2) E(v, h) = -sum_i a_i(v_i) - sum_j b_j(h_j) - \sum_{ij} W_{ij} v_i h_j

and Z is a normalizing constant. Here, a_i(v_i) and b_j(h_j) are functions and
W_{ij} is a parameter that determines the interaction between visible neuron i
and hidden neuron j.

# The structure of models in paysage

### Layers:

Boltzmann machines are constructed from
[layers](layers.md).
Latent Boltzmann machines have two layers: one of visible neurons and one of
hidden neurons. Paysage layers describe the conditional activity of their
neurons. Using the notation from the previous section, layers are used to
specify the functions a_i(v_i) and b_j(h_j), and to draw random samples from
the conditional distributions (i.e., P(v|h)). Currently, the layer types are:

- [GaussianLayer](layers.md#GaussianLayer)
- [IsingLayer](layers.md#IsingLayer)
- [BernoulliLayer](layers.md#BernoulliLayer)
- [ExponentialLayer](layers.md#ExponentialLayer)

### Models:

[Models](models.md)
have a single [hidden](models.md#hidden) layer. The model classes in paysage
contain the layers and the weights (i.e. W_ij) and define the functionality for
sampling from the Boltzmann machine and computing its derivatives. Currently,
there are two types of latent models:

- [RestrictedBoltzmannMachine](models.md#hidden##RestrictedBoltzmannMachine)
- [GaussianRestrictedBoltzmannMachine](
    models.md#hidden##GaussianRestrictedBoltzmannMachine)

### Initialize:

### Fit:

### Optimizer:
