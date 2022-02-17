# Lectures 1-2: History and core concepts

## Opening videos

The pre-session videos were:

1. [Merritt Moore](https://en.wikipedia.org/wiki/Merritt_Moore) - ballet dancer and quantum phyisicist - dancing with a robot arm from [Universal Robots](https://www.universal-robots.com/). 

1. Robots from [Boston Dynamics](https://en.wikipedia.org/wiki/Boston_Dynamics) dancing.

## Goals for today (1 min)

The goals for these first two sessions are to help you understand the history, and core concepts, of brain-inspired artificial intelligence, starting from when we began to realise the brain was an electrical network of neurons, through to 1986, when "connectionism" became mainstream in psychology.  In the next two sessions, we'll cover state-of-the-art research in perception (session 3) and action (session 4). Having learned the basics of where AI came from, and where it is today, we'll spend the fifth session on the philosophical and ethics implications of AI. The 6th session has no new content, and is given over to discussions, questions, and essay advice. 

## Early history (2 min)

We can trace the idea of artificial intelligence back to the Greeks. Hepheastus, a god, made Talos - a huge bronze statue that defended an island. And Pygmalion, a king, made a marble statue of his perfect woman, that Aprophdite, a goddess, then brought to life as Galatea. The two married and had a child. In the modern era, Mary Shelley's Frankenstein, published in 1818, was importantly different - now it was a not god, but a man, Victor Frankenstein, who was doing the bringing to life. He does this through the power of science. The Creature is 8ft tall, and each of his components is selected to be beautiful, but upon animation the Creature is hideous. 

At the time Mary Shelley was writing Frankenstein, we knew very little about how the brain worked. Several decades later, as the 19th century came to a close, we came to believe -  through the work of Golgi and Cajal -  that the brain was composed of discrete units. These units became known as neurons. Work continued throughout the first half of the 20th century, including at the Plymouth Marine Laboratory, where before and after the Second World War, Alan Hodgkin and Andrew Huxley did much of the work that eventually resulted in the Hodgkin-Huxley model. This is a mathematical account of the electro-chemical process by which neurons fire.

## Three abstractions (5 min)

It was this work which informed the three abstractions upon which most brain-inspired AI is currently based:

The first is the idea that a neuron has a level of _output activation_, a single number that represents its current rate of firing (the rate at which it produces action potentials). This ignores what might turn out to be some important details, like the timing of the action potentials, but it's a simplification assumed throughout this course. 

The second key abstraction is that the _output activation_ of a neuron is the sum of its _input activations_. Actually, it's a bit more complex than that, but we'll come back to this. 

The third key abstraction is that an input activation is calculated by taking an output activation, and multiplying it by the strength of the connections between the two neurons.

Putting it all together, the activation of a neuron is the sum of outputs of other neurons it is connected to, multiplied by the connection weights between those neurons.

OK, time to test your understanding so far. In this example, there are two input neurons, with activations of 0.8 and 1.0. The first has a connection strength of 0.25, the other of .01. What's the output activation of the neuron? 

OK, one more. Note that's a minus 1 there, not a 1. 

A couple of things to notice in that example. 

First, that connections can have a negative weight. We call these _inhibitory_ connections because the more one neuron fires, the more it inhibits the firing of the neuron it's connected to. 

Second, the output activation is negative. This makes less sense - a neuron can't have a firing rate of less than zero. This is what I meant about the calculation of output activation being a bit more complex than just adding up.

## Activation functions (1 min)

One common way of handling the problem of negative activations is to use a _logistic_ activation function, also known as a sigmoid. 

This function is useful in solving our problem, because, however negative the sum of the input activations, the output activation never falls below zero.

It's also plausible in the sense that neurons have a maximum, as well as a minimum, firing rate. With the logistic function, the output activation of a neuron never exceeds one, however large its input. 

Finally -- and this is beyond the scope of current course -- the logistic function is very useful in a mathematical sense in that it is easy to calculate the derivative and the integral. This helps mathematicians to understand how these systems work, and this deeper understanding allows us to build better AI. 

We'll come back to activation functions briefly in session 3, but for now we'll look at examples where it's OK to just add up the input activations.

## Storing knowledge (4 min)

A collection of at least three neurons and two connections is known as a neural network. The human brain has about 85 billion neurons with perhaps one thousand times that number of connections, but let's start small. Even the smallest neural network can store information about the world. 

I'm sure you cannot have come this far in a psychology degree without hearing about Pavlov's dogs. This is an example of a study of Pavlovian conditioning, where an animal learns to associate events it cares about (like the arrival of food) with events it does not initially care much about (like a bell ringing).  With repeated pairing the dog reacts to the bell much the same way as the food itself, i.e. it starts salivating.

Let's get very slightly more complicated and say that for this dog, while a bell leads to food, a bell plus a light does not produce food. This is called _conditioned inhibition_, and Pavlov was the first to demonstrate experimentally that dogs can learn this relationship.

We can represent what the dog learns like this. If the bell representation is active (1), food is active (1). But if the bell and light are both active, food is inactive (0).

What do the connection weights need to be in order for the neural network to store this information?

Take a moment to think about this. 

Answers?

$w_{B}$ must be one, so that the activation of the bell representation leads to the activation of the food representation. When bell and light are both present, the light must 'over rule' the bell. We can represent that by setting $w_{L}$ to minus one. This way the sum of the input activations times the weights is zero, which is what we want.

Note that this leads to a prediction about the dog's future behaviour. The light has become an _inhibitor_, it will make the dog less likely to expect food. So if we, for example, now train the dog that a peppermint smell predicts food, and then later present the smell and the light together, the dog will salivate less to this peppermint-light compound than the peppermint on its own. This is called a _summation_ test and this is indeed the behaviour we observe. 

## Learning

So, the neurons - or "nodes" - in a neural network can represent things in the world, and the connections between those nodes can be used to store information about the world. But how does that information get in there? So far, we've been working it out for the neural network and giving it the answers. 

For simple situations like the one's we've been discussing, that's OK. But the neural networks we'll talk about in future sessions, which do useful work, have millions - or even billions - of connections between hundreds of thousands of nodes. "Hand coding" those connections would be very hard, and time consuming. 

Can we get neural networks to learn what their weights should be?

Yes, we can. And, like the abstractions of activations and weights, the way we can do this is directly inspired by work in psychology and neuroscience.

By tradition, I'll focus on the work of Donald Hebb here, although as is often the case, other people did earlier, better, but less famous work. If this ironic aspect of history interests you, read up about Jerzy Konorski.

## Hebbian Learning

Anyway, Hebb famously said:

"When an axon of cell A is near enough to excite cell B and repeatedly or persistently takes part in firing it, some growth process or metabolic change takes place in one or both cells such that A's efficiency, as one of the cells firing B, is increased."

In modern times, we prefer the catchier:

"neurons that fire together wire together"

This idea, called Hebb's Law, can be expressed like this:

$\Delta w_{1,2} = G.a_{1}.a_{2}$

In order words, that the change (delta) in connection strength from neuron 1 to neuron 2 is the activation of the two neurons, multiplied together. G is a number less than one, which controls the overall rate of learning.

Let's see how that works in practice.

So, the first time the bell is rung, the dog doesn't expect food and so the connection strength is zero. But, both Bell and Food representations are active (1). Let's assume a learning rate (G) of 0.1. So the change in weight (delta) is 0.1 times 1 times 1, so 0.1. 

As the two things repeatedly occur, the connection strength between them increases -- the network is learning. This seems to be OK for a while, but it has the odd property that the connection always gets stronger - there is no point at which learning is complete. 


This is odd for a couple of reasons. First, the strength of connection between two neurons does presumably have an upper limit - it's a real system and so can't grow infinitely. 

Second, somewhat intuitively, it seems like that, after the first thousand (or 10,000) times a bell is followed by food, there's not much more to learn. 

One can support this intuition in a number of ways. In humans, there is the ubiquitous power law of practice which, roughly speaking, says that for each additional hour of practice, you gain a little less than the previous hour. We see something similar in Pavlovian conditioning, as this graph from an experiment with insects shows. 

So, learning tends to slow as it proceeds. 

## Bush and Mosteller

In 1951 two mathematical psychologists expressed that idea in an equation.

$\Delta w_{1,2} = G.(t - w_{1,2}$

Much of this equation is the same as before. It specifies delta w, the change in weight, w. G is a learning rate parameter, less than 1. 

One novel aspect here is _t_, which is the presence or absence of the thing than neuron 2 represents. The _t_ stands for "teacher", because it teaches neuron two how active it should be. 

The other new part aspect is the activation of neuron 1 multipled by the connection strength. This might be described as the "student", or the prediction of the network. It's the input activation to neuron 2, and so its how much neuron 1 "thinks" neuron 2 should be activated, given how active neuron 1 is. 

Let's look at that with the same example as before - Pavlov's dogs.

On the first trial, we learn just as much as in Hebbian learning. The food is present, so neuron 2 should be active, so _t_ is 1. The bell range, so a_{1} is 1. The connection starts at zero, so _w_ is zero. So the teachers predicts an activation of 1, but the student is producing an activation of zero. The difference is 1 (1 minus zero), and we multiply that by the learning rate, so we get 0.1 as the change in weight. So after the first trial, the weight goes up by 0.1.

The system learns a bit less next time. t is still 1, as is a_1, but now the weight is .1, so the difference between student and teacher is 0.9 and the weight goes up by .09. 

Each time the bell is followed by food, the connection weight goes up a bit, but less than it did last time. Eventually, the student is now the master and the learning is complete.




- Hebbian 

- Bush-Mosteller

- LTP (do slugs)

- Delta rule (blocking?)

- Convergence rule

- We're up to late 50s, early 60s in AI. 




## Suggested further reading

- [History of artificial intelligence](https://en.wikipedia.org/wiki/History_of_artificial_intelligence)

- [History of neuroscience](https://en.wikipedia.org/wiki/History_of_neuroscience)

- [Summary of the neuron](https://en.wikipedia.org/wiki/Neuron)

- [Jerzy Konorski](https://en.wikipedia.org/wiki/Jerzy_Konorski)

- [Donald Hebb](https://en.wikipedia.org/wiki/Donald_O._Hebb)

- [Power Law of Practice](https://en.wikipedia.org/wiki/Power_law_of_practice)

## Suggested further viewing

- [Pygmalion and Galatea](https://www.youtube.com/watch?v=lH1yMnoOD_)


## Video sources

- [Jason and the Argonauts](https://www.youtube.com/watch?v=Vk2iXkIH2xE) (1963)

- [Miscellaneous myths: Pygmalion and Galatea](https://www.youtube.com/watch?v=lH1yMnoOD_8)

- [Rocky Horror Picture Show](https://www.youtube.com/watch?v=LGzc0pIjHqw)

- [Image of Frankenstein from NPR](https://knpr.org/npr/2018-01/see-famous-monster-come-alive-frankenstein-1818-text)


## Image sources

In order of appearance:

- [Image on goals slide](https://www.itprotoday.com/sites/itprotoday.com/files/Neural_network.jpg)

- [Frankenstein's monster](https://en.wikipedia.org/wiki/Frankenstein%27s_monster#/media/File:Frankenstein,_or_the_Modern_Prometheus_(Revised_Edition,_1831)_Creature.jpg)

- [Golgi's drawing of the hippocampus](https://upload.wikimedia.org/wikipedia/commons/5/5e/Golgi_Hippocampus.jpg)

- [Cajal's drawing](https://en.wikipedia.org/wiki/Neuron#/media/File:PurkinjeCell.jpg)

- [Plymouth Marine Laboratory](https://twitter.com/ajwills72/status/1274308573439365120/photo/1)

- [Photo of Alan Hodgkin](https://en.wikipedia.org/wiki/Alan_Hodgkin#/media/File:Alan_Lloyd_Hodgkin_nobel.jpg)

- [Photo of Andrew Huxley](https://en.wikipedia.org/wiki/Andrew_Huxley#/media/File:Andrew_Fielding_Huxley_nobel.jpg)

- [Hodgkin-Huxley model](https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model)

- [Neuron graphic on output activation slide](https://www.youtube.com/watch?v=8IFoUWb8kLQ), see 2:25. 

- [Logistic function](https://en.wikipedia.org/wiki/Logistic_function)

- [Pavlov and Seraphima](https://en.wikipedia.org/wiki/Ivan_Pavlov#/media/File:%D0%9F%D0%BE%D1%80%D1%82%D1%80%D0%B5%D1%82._%D0%9F%D0%B0%D0%B2%D0%BB%D0%BE%D0%B2_%D0%98.%D0%9F._%D0%B8_%D0%B5%D0%B3%D0%BE_%D0%B1%D1%83%D0%B4%D1%83%D1%89%D0%B0%D1%8F_%D1%81%D1%83%D0%BF%D1%80%D1%83%D0%B3%D0%B0_%D0%A1.%D0%92._%D0%9A%D0%B0%D1%80%D1%87%D0%B5%D0%B2%D1%81%D0%BA%D0%B0%D1%8F._%D0%98%D1%8E%D0%BB%D1%8C1880%D0%B3(c)%D0%90.%D0%AF%D1%81%D0%B2%D0%BE%D0%B8%D0%BD._(pavlovs_museum).jpg)

- [Thought bubble](https://www.seekpng.com/png/detail/771-7713174_thought-bubble-thinking-bubble-png.png)

- [Jerzy Konorski](https://en.wikipedia.org/wiki/Jerzy_Konorski#/media/File:Jerzy_Konorski.jpg)

- [Donald Hebb](https://en.wikipedia.org/wiki/Donald_O._Hebb#/media/File:Donald_Hebb.gif)

- [Acquisition curve](https://www.researchgate.net/publication/8036457_Associative_learning_of_plant_odorants_activating_the_same_or_different_receptor_neurones_in_the_moth_Heliothis_virescens/download) from Skiri et al. (2005, Journal of Experimental Biology). 

- [Bob Bush](https://www.sas.upenn.edu/psych/history/bushtext.htm))))

- [Fred Mosteller](https://www.azquotes.com/quote/989087)

- ["Now I am the master"](https://en.wikipedia.org/wiki/Star_Wars_(film))


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


## Links not yet used

- [Perceptrons, the book (wikipedia)](https://en.wikipedia.org/wiki/Perceptrons_(book))

- [Blog on perceptrons, including a nice Rosenblatt and machine pic](https://fiascodata.blogspot.com/2018/05/a-computer-program-is-said-tolearn-from.html)

- [Amazing neural network firing glass brain](https://www.youtube.com/watch?v=xRwW9tNQqDw)

- [Single neuron firing](https://www.youtube.com/watch?v=lhkK6jURljs)
