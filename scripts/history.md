# Lectures 1-2: History and core concepts

## Opening videos

The pre-session videos were:

1. [Merritt Moore](https://en.wikipedia.org/wiki/Merritt_Moore) - ballet dancer and quantum phyisicist - dancing with a robot arm from [Universal Robots](https://www.universal-robots.com/). 

1. Robots from [Boston Dynamics](https://en.wikipedia.org/wiki/Boston_Dynamics) dancing.

## Goals for today

The goals for these first two sessions are to help you understand the history, and core concepts, of brain-inspired artificial intelligence, starting from when we began to realise the brain was an electrical network of neurons, through to 1986, when "connectionism" became mainstream in psychology. In the next two sessions, we'll cover state-of-the-art research in perception (session 3) and action (session 4). Having learned the basics of where AI came from, and where it is today, we'll spend the fifth session on the philosophical and ethics implications of AI. The 6th session has no new content, and is given over to discussions, questions, and essay advice. 

## Where it all started

We can trace the idea of artificial intelligence back to the Greeks. Hepheastus, a god, made Talos - a huge bronze statue that defended an island. And Pygmalion, a king, made a marble statue of his perfect woman, that Aprophdite, a goddess, then brought to life as Galatea. The two married and had a child. In the modern era, Mary Shelley's Frankenstein, published in 1818, was importantly different - now it was a not god, but a man, Victor Frankenstein, who was doing the bringing to life. He does this through the power of science. The Creature is 8ft tall, and each of his components is selected to be beautiful, but upon animation the Creature is hideous. 

## Beginning to understand the brain

At the time Mary Shelley was writing Frankenstein, we knew very little about how the brain worked. Several decades later, as the 19th century came to a close, we came to believe -  through the work of Golgi and Cajal -  that the brain was composed of discrete units. These units became known as neurons. Work continued throughout the first half of the 20th century, including at the Plymouth Marine Laboratory, where before and after the Second World War, Alan Hodgkin and Andrew Huxley did much of the work that eventually resulted in the Hodgkin-Huxley model. This is a mathematical account of the electro-chemical process by which neurons fire.

## Three abstractions

It was this work which informed the three abstractions upon which most brain-inspired AI is currently based:

The first is the idea that a neuron has a level of _output activation_, a single number that represents its current rate of firing (the rate at which it produces action potentials). This ignores what might turn out to be some important details, like the timing of the action potentials, but it's a simplification assumed throughout this course. 

The second key abstraction is that the _output activation_ of a neuron is the sum of its _input activations_. Actually, it's a bit more complex than that, but we'll come back to this. 

The third key abstraction is that an input activation is calculated by taking an output activation, and multiplying it by the strength of the connections between its inputs




## Suggested further reading

- [History of artificial intelligence](https://en.wikipedia.org/wiki/History_of_artificial_intelligence)

- [History of neuroscience](https://en.wikipedia.org/wiki/History_of_neuroscience)

- [Summary of the neuron](https://en.wikipedia.org/wiki/Neuron)

- [Hodgkin-Huxley model](https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model)

## Suggested further viewing

- [Pygmalion and Galatea](https://www.youtube.com/watch?v=lH1yMnoOD_)


## Video sources

- [Jason and the Argonauts](https://www.youtube.com/watch?v=Vk2iXkIH2xE) (1963)

- [Miscellaneous myths: Pygmalion and Galatea](https://www.youtube.com/watch?v=lH1yMnoOD_8)

- [Rocky Horror Picture Show](https://www.youtube.com/watch?v=LGzc0pIjHqw)

- [Image of Frankenstein from NPR](https://knpr.org/npr/2018-01/see-famous-monster-come-alive-frankenstein-1818-text)


## Image sources

- [Frankenstein's monster](https://en.wikipedia.org/wiki/Frankenstein%27s_monster#/media/File:Frankenstein,_or_the_Modern_Prometheus_(Revised_Edition,_1831)_Creature.jpg)

- [Golgi's drawing of the hippocampus](https://upload.wikimedia.org/wikipedia/commons/5/5e/Golgi_Hippocampus.jpg)

- [Cajal's drawing](https://en.wikipedia.org/wiki/Neuron#/media/File:PurkinjeCell.jpg)

- [Plymouth Marine Laboratory](https://twitter.com/ajwills72/status/1274308573439365120/photo/1)

- [Photo of Alan Hodgkin](https://en.wikipedia.org/wiki/Alan_Hodgkin#/media/File:Alan_Lloyd_Hodgkin_nobel.jpg)

- [Photo of Andrew Huxley](https://en.wikipedia.org/wiki/Andrew_Huxley#/media/File:Andrew_Fielding_Huxley_nobel.jpg)

- [Hodgkin-Huxley model](https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model)


The core concepts are:


Activations (firing rates)

Spreading activation

Weights (synaptic plasticity)



Learning rule (Delta rule)

Perceptron convergence theorem - AI optimism. 

XOR - AI pessimism

Backprop - (re)birth of connectionism

How brain-like is backprop?


## Demonstrations in keras

- [Minimal XOR solving with backprop](https://github.com/conwayok/keras-xor-example/blob/master/keras-xor-example/train.py)


## History

- [Perceptrons, the book (wikipedia)](https://en.wikipedia.org/wiki/Perceptrons_(book))

- [Blog on perceptrons, including a nice Rosenblatt and machine pic](https://fiascodata.blogspot.com/2018/05/a-computer-program-is-said-tolearn-from.html)

