# Lectures 1-2: History and core concepts

## Opening videos

The pre-session videos were:

1. [Merritt Moore](https://en.wikipedia.org/wiki/Merritt_Moore) - ballet dancer and quantum phyisicist - dancing with a robot arm from [Universal Robots](https://www.universal-robots.com/). 

1. Robots from [Boston Dynamics](https://en.wikipedia.org/wiki/Boston_Dynamics) dancing.

## Goals (1 min)

The goals for this course  are to help you understand the history, and core concepts, of brain-inspired artificial intelligence, starting from when we began to realise the brain was an electrical network of neurons, through to today.  We'll also cover state-of-the-art research in perception and action. And, having learned the basics of where AI came from, and where it is today, we'll spend the some time  on the philosophical and ethical implications of AI. 

## Diversity 

Before we get into any of this, there's a broader social issue I'd like to address directly. In my teaching, I generally like to tell you about the people behind the work, as I think this gives a better sense of how science gets done. However, historical lack of diversity in the field means that I end up with a set of mugshots of old white men. It doesn't have to be that way, and things are beginning to change. As an antidote to the lack of diversity in what's to follow, please take a look at the much broader range of people now involved in AI - for example, see this series of interviews on [NESTA](https://www.nesta.org.uk/feature/12-women-ai/).


## Early history (2 min)

We can trace the idea of artificial intelligence back to the Greeks. Hepheastus ([pronunication](https://duckduckgo.com/?t=ffab&q=pronounce+Hepheastus&iax=videos&ia=videos&iai=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3Df8Yrm0c_kcU)), a god, made Talos - a huge bronze statue that defended an island. And Pygmalion, a king, made a marble statue of his perfect woman, that Aprophdite, a goddess, then brought to life as Galatea. The two married and had a child. In the modern era, Mary Shelley's Frankenstein, published in 1818, was importantly different - now it was a not god, but a man, Victor Frankenstein, who was doing the bringing to life. He does this through the power of science. The Creature is 8ft tall, and each of his components is selected to be beautiful, but upon animation the Creature is hideous. 

At the time Mary Shelley was writing Frankenstein, we knew very little about how the brain worked. Several decades later, as the 19th century came to a close, we came to believe -  through the work of Golgi and Cajal -  that the brain was composed of discrete units. These units became known as neurons. Work continued throughout the first half of the 20th century, including at the Plymouth Marine Laboratory, where before and after the Second World War, Alan Hodgkin and Andrew Huxley did much of the work that eventually resulted in the Hodgkin-Huxley model. This is a mathematical account of the electro-chemical process by which neurons fire.

## Three abstractions (6 min)

It was this and related work which informed the three abstractions upon which most brain-inspired AI is currently based. In the following, I'll describe these abstractions both in words, and in equations, and sometimes also with diagrams and charts. For the purposes of this course, you only need to understand one of those explanations to keep up. Ask if you're unsure.

The first key abstraction is the idea that a neuron has a level of _output activation_, a single number that represents its current rate of firing (the rate at which it produces action potentials). This ignores what might turn out to be some important details, like the timing of the action potentials, but it's a simplification assumed throughout this course. 

The second key abstraction is that the _output activation_ of a neuron is the sum of its _input activations_. 

The third key abstraction is that an input activation is calculated by taking an output activation, and multiplying it by the strength of the connections between the two neurons.

Putting it all together, the activation of a neuron is the sum of outputs of other neurons it is connected to, each multiplied by the connection weights between those neurons.

OK, time to test your understanding so far. In this example, there are two input neurons, with activations of 0.8 and 1.0. The first has a connection strength of 0.25, the other of .01. What's the output activation of the neuron? (The answer is 0.21).

OK, one more. Note that's a minus 1 there, not a 1. (The answer is -0.45). 

A couple of things to notice in that example. 

First, that connections can have a negative weight. We call these _inhibitory_ connections because the more one neuron fires, the more it inhibits the firing of the neuron it's connected to. 

Second, the output activation is negative. This makes less sense - a neuron can't have a firing rate of less than zero. 

One common way of handling the problem of negative activations is to use a _logistic_ activation function, also known as a sigmoid. The _e_ in the equation is [Euler's number](https://en.wikipedia.org/wiki/E_(mathematical_constant)), which is approximately 2.72. 

This function is useful in solving our problem, because, however negative the sum of the input activations, the output activation never falls below zero.

It's also plausible in the sense that neurons have a maximum, as well as a minimum, firing rate. With the logistic function, the output activation of a neuron never exceeds one, however large its input. 

Finally - and this is beyond the scope of current course - the logistic function is very useful in a mathematical sense in that it is easy to calculate the derivative and the integral. This helps mathematicians to understand how these systems work, and this deeper understanding allows us to build better AI. 

We'll come back to activation functions briefly in session 3, but for now we'll look at examples where it's OK to just add up the input activations.

## Storing knowledge (4 min)

A collection of at least three neurons and two connections is known as a neural network. The human brain has about 85 billion neurons with perhaps one thousand times that number of connections, but let's start small. Even the smallest neural network can store information about the world. 

I'm sure you cannot have come this far in a psychology degree without hearing about Pavlov's dogs. This is an example of a study of Pavlovian conditioning, where an animal learns to associate events it cares about (like the arrival of food) with events it does not initially care much about (like a bell ringing).  With repeated pairing the dog reacts to the bell much the same way as the food itself, i.e. it starts salivating.

Let's get very slightly more complicated and say that for this dog, while a bell leads to food, a bell plus a light does not produce food. This is called _conditioned inhibition_, and Pavlov was the first to demonstrate experimentally that dogs can learn this relationship.

We can represent what the dog learns like this. If the bell representation is active (1), food is active (1). But if the bell and light are both active, food is inactive (0).

What do the connection weights need to be in order for the neural network to store this information?

Take a moment to think about this. 

Answer: $w_{B}$ must be one, so that the activation of the bell representation leads to the activation of the food representation. When bell and light are both present, the light must 'over rule' the bell. We can represent that by setting $w_{L}$ to minus one. This way the sum of the input activations times the weights is zero, which is what we want.

Note that this leads to a prediction about the dog's future behaviour. The light has become an _inhibitor_, it will make the dog less likely to expect food. So if we, for example, now train the dog that a peppermint smell predicts food, and then later present the smell and the light together, the dog will salivate less to this peppermint-light compound than the peppermint on its own. This is called a _summation_ test and this is indeed the behaviour we observe. 

## Learning (2 min)

So, the neurons - or "nodes" - in a neural network can represent things in the world, and the connections between those nodes can be used to store information about the world. But how does that information get in there? So far, we've been working it out for the neural network and giving it the answers. 

For simple situations like the one's we've been discussing, that's OK. But the neural networks we'll talk about in future sessions, which do useful work, have millions - or even billions - of connections between hundreds of thousands of nodes. "Hand coding" those connections would be very hard, and time consuming. 

Can we get neural networks to learn what their weights should be?

Yes, we can. And, like the abstractions of activations and weights, the way we can do this is directly inspired by work in psychology and neuroscience.

By tradition, I'll focus on the work of Donald Hebb here, although as is often the case, other people did earlier  but less famous work. If this ironic aspect of history interests you, read up about Jerzy Konorski. Konorski, in turn, was predated by Santiago Cajal by about 50 years. So, in terms of historical precedent for what we call "Hebbian" learning, one can go back at least as far as Cajal's public lecture in 1894. 

### Hebbian Learning (1 min)

Anyway, Hebb famously said:

"When an axon of cell A is near enough to excite cell B and repeatedly or persistently takes part in firing it, some growth process or metabolic change takes place in one or both cells such that A's efficiency, as one of the cells firing B, is increased."

In modern times, we prefer the catchier:

"neurons that fire together wire together"

### Neuroscience of learning (1 min)

In neuroscience, this behaviour of neurons is called long-term potentiation. It was first observed in the 1960s by a number of people, including Eric Kandel in 1964 and Terje Lømo in 1966. The mechanisms at the level of individual neurons are now somewhat understood, thanks in part to work on Aplysia Californica, a sea slug with a small number of large neurons, about 20,000 neurons, with cell bodies of around 1mm. 


### Applying Hebbian learning (2 min)

This idea, called Hebb's Law, can be expressed like this:

$\Delta w_{1,2} = G.a_{1}.a_{2}$

In order words, that the change (delta) in connection strength from neuron 1 to neuron 2 is the activation of the two neurons, multiplied together. G is a number less than one, which controls the overall rate of learning.

Let's see how that works in practice.

So, the first time the bell is rung, the dog doesn't expect food and so the connection strength is zero. But, both Bell and Food representations are active (1). Let's assume a learning rate (G) of 0.1. So the change in weight (delta) is 0.1 times 1 times 1, so 0.1. 

As the two things repeatedly co-occur, the connection strength between them increases -- the network is learning. This seems to be OK for a while, but it has the odd property that the connection always gets stronger - there is no point at which learning is complete. 

This is odd for a couple of reasons. First, the strength of connection between two neurons does presumably have an upper limit - it's a real system and so can't grow infinitely. 

Second, somewhat intuitively, it seems like that, after the first thousand (or 10,000) times a bell is followed by food, there's not much more to learn. 

One can support this intuition in a number of ways. In humans, there is the ubiquitous power law of practice which, roughly speaking, says that for each additional hour of practice, you gain a little less than the previous hour. 

We see something similar in Pavlovian conditioning, as this graph from an experiment with insects shows. The x axis is number of pairings, and the y-axis is the magnitude of the response (with 100 being the maximum possible response). The different lines are for different stimulus magnitudes - more intense stimuli lead to stronger learning.

So, learning tends to slow as it proceeds. 

### Bush and Mosteller (3 min)

In 1951 two psychologists expressed that idea in an equation.

$\Delta w_{1,2} = G.(t - w_{1,2}$

Much of this equation is the same as before. It specifies delta w, the change in weight, w. G is a learning rate parameter, less than 1. 

One novel aspect here is _t_, which is the presence or absence of the thing that neuron 2 represents. The _t_ stands for "teacher", because it teaches neuron two how active it should be. 

The other new part is the activation of neuron 1 multipled by the connection strength. This might be described as the "student", or the prediction of the network. It's the input activation to neuron 2, and so its how much neuron 1 "thinks" neuron 2 should be activated, given how active neuron 1 is. 

Let's look at that with the same example as before - Pavlov's dogs.

On the first trial, we learn just as much as in Hebbian learning. The food is present, so neuron 2 should be active, so _t_ is 1. The bell rang, so a_{1} is 1. The connection starts at zero, so _w_ is zero. So the teacher predicts an activation of 1, but the student is producing an activation of zero. The difference is 1 (1 minus zero), and we multiply that by the learning rate, so we get 0.1 as the change in weight. So after the first trial, the weight goes up by 0.1.

The system learns a bit less next time. t is still 1, as is a_1, but now the weight is .1, so the difference between student and teacher is 0.9 and the weight goes up by .09. 

Each time the bell is followed by food, the connection weight goes up a bit, but less than it did last time. Eventually, the student is now the master and the learning is complete.

### The delta rule

Although Bush and Mosteller's system provides a simple way for a neural network to learn, it's not much used in modern systems. There are quite a few reasons for this, but we're going to deal with a couple - one from psychology, and one from AI.

#### Psychology

The reason from psychology is that the Bush-Mosteller system is not a good model of how people and other animals learn. Perhaps the simplest way to illustrate this is to consider the phenomenon of blocking, first reported by Kamin in 1969. It's subsequently been demonstrated many times in many species. 

Let's look at blocking in the case of a simple animal experiment. A mouse first repeatedly observes that a light is followed by food. It learns to salivate to the light. Next a tone is presented at the same time as the light, again followed by food. This also happens multiple times. Finally, the tone is presented alone, without the light. 

What does the Bush-Mosteller system predict in this case? Thoughts?

Well, if you pair light with food often enough, the association will go to 1, and then stop. Now, when you present the tone and light together, the association to the light won't increase any further, but the association between tone and food will go to one. So, when the tone is presented without the light, the mouse expects food and so salivates.

This is not what happens. In fact, little salivation occurs to the tone alone. This is how the phenomenon gets its name -  the association of the tone to the food seems to be _blocked_ by the pre-existing association of the light to the food. 

Over the coming decades, quite a lot of psychologists would propose various theories of why blocking occurs. In fact, three members of staff in our School have worked on this - myself, Chris Mitchell, and Peter Jones, and our academic 'parents' (i.e. Ph.D. and post-doc supervisors) and grandparents - Nick Mackintosh, John Pearce, Ian McLaren, Geoff Hall - worked on it, too. For today, though, we'll focus on just one theory - the Rescorla-Wagner theory, from 1972.

I'm picking on Rescorla-Wagner for two reasons. First, it's one of the earliest and simplest explanations of blocking. Second, it's basically the same theory as AI researchers came up with in the early 1960s - although the two groups seemed largely unaware of each other at the time. 

Rescorla-Wagner theory is just a minor modification on Bush and Mosteller's idea. In Bush-Mosteller, the amount a weight changes between neurons 1 and 3 depends on the difference between how active the neuron 3 should be, and the how active neuron 1 is making it. 

In some ways, that's a bit of a weird idea if there's more than two neurons. For example, in the case of a blocking experiment, the network ends up over-predicting the food. The teaching signal is 1, but the connection between light and food is 1, as is the connection between tone and food. So, the total input to the food nodes is 2, even though the teaching signal is 1.

One could argue about whether that's a problem or not. I mean, one way you could fix that is to have an activation function, like we discussed earlier, so that output activation did not exceed one. But, the Rescorla-Wagner theory takes the position that learning should stop when the sum of the input activations matches the teaching signal. In other words, when the outcome - food - is fully predicted. This idea allows it to predict blocking.

Let's see how that works. 

When the food and light are presented together, the association between them rises to one and stops, just like in Bush-Mosteller.

However, now the tone comes along. The food is already fully predicted by the light, and so from the perspective of Rescorla-Wagner, there's nothing to learn. The weight between tone and food remains at zero. This is often described as error-correcting learning - we only learn to the extent we need to in order to avoid errors.

So, now when the tone is presented on its own, the food node is not activated. Rescorla-Wagner theory predicts blocking!

#### AI

So, one reason to build a brain using the delta rule - Rescorla-Wagner theory - rather than Hebbian learning or the Bush-Mosteller equation is that it seems to be a better account of how people and other animals learn. 

Another reason comes from AI research in the 1950s and early 1960s, and is known as the convergence rule. This is a mathematical proof that, if a problem can be solved by some combination of weights in a network with a single layer of weights, then the delta rule will solve the problem in finite time.

This is pretty jaw dropping - anything that can be learned by a single-layer network _will_ be learned by the delta rule. 100% guaranteed. So, this appears to dispense with the idea of having to set these weights by hand. Just build the network, train it, and it will learn. In 1960, Frank Rosenblatt first proved this for a type of neural network called a perceptron. Related work was being done by Widrow and Hoff in the early 1960s, work that is closer to the delta-rule formulation I'm using in these lectures, and which also leads to another name for the delta rule - the least means-squared algorithm. So, this key idea is variously known as the delta rule, the LMS rule, and the Rescorla-Wagner theory.

In the late 1950s, there was a lot of excitement and hype about brain-inspired AI. For example, Frank Rosenblatt made statements in 1958 that led the  New York Times to say that these kinds of systems were "the embryo of an electronic computer that [the Navy] expects will be able to walk, talk, see, write, reproduce itself and be conscious of its existence." 

So, around 15 years before I was born, the US Navy thought it was beginning to gestate what is now called a Artificial General Intelligence. Almost a lifetime later, progress has been somewhat limited! What went wrong?

## Multilayer networks

There's an important distinction to make here. With the delta rule, a single-layer network has a mechanism by which it _will_ learn anything it _can_ learn. But what _can_ it learn? 

Well, turns out, there are some relatively simple problems single-layer networks cannot learn. For example, say a menu says that the omlette comes with chips or salad. Which of these orders fits that rule?

1. Omelette and chips

2. Omelette and salad

3. Omelette, chips, and salad

Most people say (1) and (2) fit the rule, but (3) does not. Formally speaking, this is an exclusive-or rule (XOR). You can have chips, or salad, but not both. (You also can't have neither in XOR, which might diverge a bit from the restaurant example, but let's stick with it). 

A single-layer network, with the input nodes chips and salad, can never learn that (3) is not OK. To learn (1), it needs a association of 1 between chips and OK. To learn (2) is needs an association of 1 between salad and OK. So, when presented with omlette and salad, it's really confident that this is OK. There's no set of weights that will solve this problem. 

The fact that single-layer networks cannot learn fairly simple relationships like XOR led to people in AI losing interest in brain-inspired systems. This is sometimes attributed to Minsky & Papert's highly critical book "Perceptrons", published in 1969 - sometimes described as killing off neural network research for a decade. [Whole papers in sociology](https://www.jstor.org/stable/285702?seq=1#metadata_info_tab_contents) have been written about this. 

Along with a number of other developments, the 1970s saw a marked reduction in interest in (and funding for) AI research. This is known as the First AI winter (around 1974-1980). In the UK, the Lighthill report in 1974 said:

"In no part of the field have the discoveries made so far produced the major impact that was then promised".

When things started to take off again in AI around 1980, brain-inspired systems were nowhere to be seen. It wouldn't be until the end of the 80s that things would begin to pick up again for brain-inspired AI.

### Solving XOR

While brain-inspired AI fell out of the limelight around the time I was born, all the pieces of the puzzle for its eventual resurgence were already there. Let's trace the roots of its return to form.

The first thing to note is that, well before Minsky & Papert's book, people were aware that a neural network could learn an XOR relationship, it just needed more than one layer of weights, and the concept of a _threshold_, i.e. a minimum level of input required for a unit to produce output.

With these two things, you can build a neural network that solves XOR with four neurons. Let's work through how it does that. When just one of the units is on, say the top one, what happens? Let's look first at the middle unit, which we also call a _hidden unit_ because it is hidden between the input and output units. The hidden unit receives input of one from the "chips" (C) neuron, and no input from the "salad" (S) neuron. So it's total input is one, which is lower than it's threshold of 1.5, so it produces no output.

Now, let's look at the output unit. It receives an input of 1 from C, zero from S and zero from the hidden unit. So, it's total input is 1. That's greater than its threshold of 0.5, so the output unit is active.

However, when we get both chips and salad, things are different. Specifically, the hidden unit receives an input of two, which is greater than its threshold. The output units gets an input of one from C, and input of 1 from S, but an input of -2 from the hidden unit. Overall, the activation is zero.

OK, so a neural network with a hidden neuron can solve XOR if we give it the right weights and thresholds.

The next part of the puzzle is ... how does the network learn these weights for itself? 

### Backpropagation of error

We might assume that we can use the same method as before - the delta rule (also known as Rescorla-Wagner theory). This works for the connections in blue - we know what the output should be (t), we know the prediction coming from the network ($\Sigma_{aw}$), and we know the activation of the neurons.

The problem comes with the connections in red. How should we update these? What should the output of the hidden unit be? We don't know, because the hidden unit doesn't directly represent anything observable. The input units represent chips and salad, we can observe those. The output unit represents whether this is valid choice or not, we can give the network feedback about that so it can learn. But how do we give it feedback about what its hidden unit should be doing?

The most common solution to this puzzle is called backpropagation of error. This is at the heart of most neural network systems in AI, so let's take it step by step.

First, what do we mean by "error"? Error is the difference between what the correct answer is (t) and what the student predicts. So, the delta rule changes weights to the extent that there is an error of prediction, which is why it's often referred to as a model of error-driven learning.

Now we have the concept of _error_, we can reformulate our problem. The problem is, what should the error be at the hidden unit?

Let's look at a network that is on its way to learning XOR. To make the example simpler, we're going to ignore the thresholds. The error at the output unit is -1. The idea of backpropagation of error is that the error at the output unit is passed back to the hidden unit, along the weight connecting them. So, in this example, the error and the connection are both negative, so we end up with a positive error.

Now we have an error for the hidden unit, we use it to update the weights as normal. So, the error is positive here, and thus the weights from the input units to the hidden unit will increase. This is what we want, as it'll reduce error at the output unit - in other words, we'll be closer to having learned the problem. 

And that is backpropagation of error - probably the single most important innovation in brain-inspired AI. But whose idea was it?

### History

If you ask a psychologist, they'll probably say that backprop was invented by Rumelhart, Hinton & Williams in 1986. This is because these three people did more than any other to popularize the approach to psychologists. They also made some non-trivial contributions, which we'll come to later. However, the basic idea was known around the same time as Rosenblatt's early work -- it can be traced back to work in aerospace engineering done by Henry Kelley in 1960. It took another 14 years before anyone seemed to realise the same idea could be used to train multilayer neural networks - this idea was first published by Paul Werbos in his Ph.D. thesis in 1974. 

Progress from this initial idea was slow, with the idea being picked up independently, not only by Rumelhart, Hinton & Williams in 1986 , but also by Parker, and by Yann LeCun, both in 1985. Although I've not made a detailed study, my guess is that the main thing that happened in that 'dead decade' was that computers suddenly got a lot faster and cheaper in the mid 80s, so it was possible for a wider range of people to play around with backprop and see what it could do in practice. This was in fact, to my mind, the most important contribution of Rumelhart and colleagues in this regard --- they showed the world that backprop could do useful work, that it worked _in practice_. They included their work in an enormously influential two-volume book called _Parallel Distributed Processing_. More than any other single source, this was responsible for psychologists adopting neural networks as models of human behaviour, in a field that became known as _connectionism_. When I decided to do a Ph.D. in 1994, connectionism was very much in vogue, and it was these two volumes that, along with my supervisor Ian McLaren, are largely responsible for where I did my Ph.D. and what I did it on.

### Power and limitations of backprop

So, by 1986, the world was increasingly becoming aware that you could train multilayer neural networks using backpropagation. A few years later, Hornik, Stinchcombe & White (1989), reported a very important discovery - multilayer nets are _universal approximators_. The maths is quite complex here, but the conclusion is astounding - this kind of neural net can, in principle, represent _any_ (deterministic) mapping between its inputs and its outputs, as long as it has enough hidden units.

So, mulltilayers are, in principle, really powerful - it's not possible to come up with a relationship between input and output that it cannot represent. The difficulty is that, saying it _can_ represent it is different to saying it can learn it. This is sort of the opposite to the _convergence_ theorem we discussed earlier. A single-layer delta-rule network _will_ learn anything it can learn. A multilayer network _can_ learn anything, but there remains the question of whether it _will_ learn it. 

In particular, _backprop_ is not guaranteed to learn, due to the problem of _local minima_.

#### Local minima

To understand the problem of local minima, one needs to remember that the way we train a neural network is to minimize error - when it stops making errors, it has learned. We do this by changing the weights of connections.

Let's illustrate this with the simplest possible system - two neurons and one link. The weight of that link can go from a large negative number to a large positive number. If we want to represent a simple Pavlovian relationship, such as bell -> food, then the error in our system will be zero when the weight of that connection is 1. 

In a simple system like this, it's always obvious what you should do to reduce error. If weight is greater than one, you reduce it. If it's less than one, you increase it. We can visualize this as a ball rolling down a hill - the hill has a gradient, and we go in the direction in which the gradient is most negative. For this reason, we sometimes describe learning as _gradient descent_. The simple delta rule (Rescorla-Wagner theory) performs gradient descent to learn.

The power of that simple learning algorithm is that it will always find the solution, if that solution can be represented by the network. That's because the error surfaces for single layer networks, even when there are many connections, always have a single minimum point. 

The problem with multilayer networks is that the error surface is often more complex - in particular, they can have _local minima_, which means that, depending on where the network starts, it might not learn the mapping.

In our first example, the network started with a relatively low weight, and it used gradient descent to continue to reduce the weight until any further change - increase or decrease - would have increased the error, and its stopped. It also found the solution, the error is the minimum possible error for the problem.

However, in our second example, the network started with a somewhat higher weight. It "rolls downhill" as before, and it again reaches a point where any further change - increase or decrease - would increase error. It therefore stops. However, this is not the solution to the problem - the error is higher than it could be. We say that the network has got stuck in a local minimum. Although it's obvious to us that it it continued to decrease its weight, despite the increase in error, it would eventually find the best solution. But backpropagation (at least in its basic form) will not do that, and so it fails to learn.

How much of a problem local minima are depends a lot on how likely the network is to get trapped in them for things we actually want it to learn. One of the main contributions of Rumelhart, Hinton and Williams was to show that for a range of things that people can learn, the likelihood of a backprop net getting stuck in a local minimum was very low. These demonstrations were really important in convincing psychologists to consider connectionist models as accounts of human behaviour. However, this fairly quickly hit a couple of objections, which we'll cover next.


#### Catastrophic interference

We've known for a very long time that when people learn new information, it can interfere with old information - we call this _retroactive inteference_. One example of this behaviour was reported by Barnes & Underwood (1959). Participants first learn a list of nonwords pairsed with real words (e.g. dax-regal). They then learn a second list of nonword-word pairs (e.g. dax-cabbage). This second list has the same cues (first words), but different targets (second words). In the test phase, they are shown the cues (e.g. dax) and asked what they were paired with. More time spent learning the second list leads to two things: (1) better memory of the second list, (2) worse memory of the first list. However, note that the first list is not completely forgotten.

McCloskey and Cohen (1989) showed that things are different when you train a backprop net on this problem. It can learn the first list perfectly. It can also learn the second list perfectly. The problem is, in order to learn the second list, it completely forgets the first list. This is very unlike people.

Note that McCloskey & Cohen's result came out the same year as Hornik and colleagues showed that these kind of networks can represent any mapping. So, why does it do so poorly here? Actually, the network can learn both lists just fine ... but you have to _intermix_ the training. So, rather than teaching list 1 and then list 2, you mix them up and train the items in a random order. The problem only occurs if you try and train one and then the other. 

Although that solves the problem in principle, catastrophic inference continues to cause major practical problems to this day. A robot suffering from catastrophic interference can be taught many things in the lab, because we can arrange for all those things to be mixed up so it doesn't forget. But, once it leaves the lab and makes its own way in the world, we have to prevent it from learning further. If it continued to learn, it would lose what we'd already taught it. We would have a Homer Simpson robot!

There have been various ideas for solving the catastrophic interference problem (you can read about some of them [here](https://en.wikipedia.org/wiki/Catastrophic_interference)), but in practice it's still with us today. 

#### Neural plausibility

One fairly ironic thing is that, while backprop was largely responsible for bringing brain-inspired AI back to popularity, it did so by making it less brain-like. The backprop algorithm requires one to calculate error, and pass it _back_ along the connection. Neurons just do not work like that, activation goes in one direction down a neural connection, not both. There have been various ideas for a more neurally plausible version of backprop, but they are beyond the scope for today.


## Suggested further reading

- [History of artificial intelligence](https://en.wikipedia.org/wiki/History_of_artificial_intelligence)

- [History of neuroscience](https://en.wikipedia.org/wiki/History_of_neuroscience)

- [Summary of the neuron](https://en.wikipedia.org/wiki/Neuron)

- [Santiago Ramon y Cajal](https://en.wikipedia.org/wiki/Santiago_Ram%C3%B3n_y_Cajal)

- [Jerzy Konorski](https://en.wikipedia.org/wiki/Jerzy_Konorski)

- [Donald Hebb](https://en.wikipedia.org/wiki/Donald_O._Hebb)

- [Power Law of Practice](https://en.wikipedia.org/wiki/Power_law_of_practice)

- [Long-term potentiation](https://en.wikipedia.org/wiki/Long-term_potentiation)

- [Aplysia Californica](https://en.wikipedia.org/wiki/California_sea_hare#Laboratory_use)

- [Eric Kandel](https://en.wikipedia.org/wiki/Eric_Kandel)

- [Blocking](https://en.wikipedia.org/wiki/Blocking_effect)

- [Rescorla-Wagner model](https://en.wikipedia.org/wiki/Rescorla%E2%80%93Wagner_model)

- [Perceptron](https://en.wikipedia.org/wiki/Perceptron)

- [Widrow and Hoff, and the LMS algorithm](https://isl.stanford.edu/~widrow/papers/j2005thinkingabout.pdf)

- [Perceptrons (1969)](https://en.wikipedia.org/wiki/Perceptrons_(book))

- [The sociology of the Perceptrons Controversy](https://www.jstor.org/stable/285702?seq=1#metadata_info_tab_contents)

- [Lighthill report](https://en.wikipedia.org/wiki/Lighthill_report)

- [Backpropagation](https://en.wikipedia.org/wiki/Backpropagation)

- [Rumelhart, Hinton & Williams (1986)](http://www.cs.toronto.edu/~hinton/absps/naturebp.pdf)

- [Connectionism](https://en.wikipedia.org/wiki/Connectionism)

- [Hornik, Stinchcombe & White (1989)](hornik1989.pdf)

- [McCloskey & Cohen (1989)](mccloskeycohen.pdf)

- [Catastrophic interference](https://en.wikipedia.org/wiki/Catastrophic_interference)


## Suggested further viewing

- [Pygmalion and Galatea](https://www.youtube.com/watch?v=lH1yMnoOD_)


## Video sources

- [Jason and the Argonauts](https://www.youtube.com/watch?v=Vk2iXkIH2xE) (1963)

- [Miscellaneous myths: Pygmalion and Galatea](https://www.youtube.com/watch?v=lH1yMnoOD_8)

- [Rocky Horror Picture Show](https://www.youtube.com/watch?v=LGzc0pIjHqw)

- [Image of Frankenstein from NPR](https://knpr.org/npr/2018-01/see-famous-monster-come-alive-frankenstein-1818-text)

- [Homer Simpson, "Every time I learn something..."](https://www.youtube.com/watch?v=MNeWZwUn3x0)

## Image sources

In order of appearance (roughly):

- [Diversity in AI research](https://www.nesta.org.uk/feature/12-women-ai/)

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

- [Aplysia Californica](https://en.wikipedia.org/wiki/California_sea_hare#/media/File:Aplysia_californica.jpg)

- [Terje Lomo](https://www.uniforum.uio.no/nyheter/2003/08/professor-terje-loemo-tildelt-anders-jahres-store-medisinske-pris.html?vrtx=email-a-friend)

- [Eric Kandel](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Eric_Kandel_01.JPG/1024px-Eric_Kandel_01.JPG)

- [Leon Kamin](https://upload.wikimedia.org/wikipedia/en/a/a5/Leon_Kamin.jpg)

- [Nick Mackintosh](https://www.psychol.cam.ac.uk/news/professor-nicholas-mackintosh)

- [John Pearce](https://www.cardiff.ac.uk/people/view/1175169-pearce-john)

- [Bob Rescorla](https://www.bestmastersinpsychology.com/30-most-influential-psychologists-working-today/)

- [Alan Wagner](https://pagesped.cahuntsic.ca/sc_sociales/psy/introsite/lexique/definitionsw.htm)

- [Ian McLaren](http://psychology.exeter.ac.uk/staff/profile/index.php?web_id=Ian_McLaren)

- [Andy Wills](https://www.plymouth.ac.uk/staff/andy-wills)

- [Chris Mitchell](https://www.plymouth.ac.uk/staff/christopher-mitchell)

- [Peter Jones](https://www.researchgate.net/profile/Peter-Jones-57)

- [Geoff Hall](https://duckduckgo.com/?q=geoff+hall+psychology&t=ffab&iax=images&ia=images&iai=https%3A%2F%2Fwww.york.ac.uk%2Fmedia%2Fpsychology%2Fimages%2Fpeople%2Femeritus-faculty%2FGeoff%2520200x300.jpg)

- [Perceptron Mark 1](https://upload.wikimedia.org/wikipedia/en/5/52/Mark_I_perceptron.jpeg)

- [Pictures of Rosenblatt and Perceptron](https://fiascodata.blogspot.com/2018/05/a-computer-program-is-said-tolearn-from.html)

- [Bernard Widrow](https://en.wikipedia.org/wiki/Bernard_Widrow#/media/File:Widrow_with_Adaline.svg)

- [James Lighthill](https://en.wikipedia.org/wiki/James_Lighthill)

- [Book cover for Perceptrons](https://www.amazon.co.uk/perceptrons-introduction-computational-geometry-expanded/dp/0262631113)

- [Seymour Papert](https://en.wikipedia.org/wiki/Seymour_Papert)

- [Marvin Minksy](https://en.wikipedia.org/wiki/Marvin_Minsky)

- [salad](https://totsfamily.com/green-salad-recipe-homemade-honey-mustard-dressing/)

- [salad, omelette, chips](https://www.tripadvisor.com/LocationPhotoDirectLink-g1190956-d6102631-i300833541-Restaurante_O_Farolim-Ponta_do_Pargo_Calheta_Madeira_Madeira_Islands.html)

- [simple error gradient](https://www.desmos.com/calculator)

- [Sun-1 workstation](https://en.wikipedia.org/wiki/Sun-1)

- [Rumelhart, Hinton, Williams](https://aiws.net/the-history-of-ai/aiws-house/page/2/)

- [Paul Werbos](https://en.wikipedia.org/wiki/Paul_Werbos)

- [Henry Kelley](https://www.gwern.net/docs/ai/1989-cliff.pdf)


## Demonstrations in keras

- [Minimal XOR solving with backprop](https://github.com/conwayok/keras-xor-example/blob/master/keras-xor-example/train.py)


## Links not yet used



- [Yann LeCunn](https://en.wikipedia.org/wiki/Yann_LeCun)

- [Amazing neural network firing glass brain](https://www.youtube.com/watch?v=xRwW9tNQqDw)

- [Single neuron firing](https://www.youtube.com/watch?v=lhkK6jURljs)

## Exercises

- Extinction
- Over-expectation
- Superconditioning

