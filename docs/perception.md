# Perception

## Opening videos

- 1997: IBM's Deep Blue computer beats world grandmaster Gary Kasparov at chess; the [BBC news clip](https://www.youtube.com/watch?v=KF6sLCeBj0s) marks the 20th anniversary of this success.

- 2021: [Pig, dog, pig, dog, loaf of bread](https://www.youtube.com/watch?v=r2GjEvFUsYw) - In the 2021 film, [The Mitchells vs. The Machines](https://www.netflix.com/gb/title/81399614), an AI armageddon is averted in part through the limitations of AI object recognition. Current-day AI really is this bad at object recognition, at least sometimes. 

## Introduction

In the [core concepts](core.md) section of this course we saw that, by the end of the 1980s, we had developed multilayer artificial neural networks that could in principle learn any mapping between input and output, and that we had a system - backprop - that sometimes allowed them to learn this mapping for themselves. Yet, this brain-inspired approach would not make it to the forefront of developments in AI for more than twenty years. For example, a decade after backprop was popularized, a computer - [Deep Blue](https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer)) - beat the world chess champion Gary Kasparov. But there was nothing brain-inspired about how Deep Blue did this - it used what is known as [symbolic AI](https://en.wikipedia.org/wiki/Symbolic_artificial_intelligence), using large databases of previous chess games, and search algorithms specially written for the purpose of playing chess, plus new computer chips specifically designed to speed up those algorithms. The development of Deep Blue was the culmination of a 12 year project for engineer [Feng-Hsiung Hsu](https://en.wikipedia.org/wiki/Feng-hsiung_Hsu)  ([pronounciation](https://www.howtopronounce.com/feng-hsiung-hsu)) and the team that worked with him. 

## Moravec's paradox

While computers have been able to beat humans at chess since before most of the class were born, they're still not very good at recognising basic objects ... like dogs, pigs, and loaves of bread. This seems surprising at first sight, but it's a widely-observed problem in AI. As [Stephen Pinker](https://en.wikipedia.org/wiki/Steven_Pinker) once wrote, "the main lesson of thirty-five years of AI research is that the hard problems are easy and the easy problems are hard." ([Pinker, 1994](https://en.wikipedia.org/wiki/The_Language_Instinct)). In AI, this is often known as [Moravec's paradox](https://en.wikipedia.org/wiki/Moravec%27s_paradox), and roboticist [Rodney Brooks](https://en.wikipedia.org/wiki/Rodney_Brooks) (inventor of the [Roomba](https://en.wikipedia.org/wiki/Roomba) robot vacuum cleaner) has made similar observations.

## AlexNet

Ten years ago, a [paper](https://proceedings.neurips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf) was published that turned the world on to the idea that the hard problem of easy object recognition might be solved by brain-inspired AI. The roots of this work go back to 1980 - before the popularization of backprop. But, more than any other single paper, the work by Alex Krichevsky in 2012 - dubbed AlexNet -  influenced people to use brain-inspired AI to try and solve real-world object recognition problems. But, let's start from the beginning.

## Visual neuroscience and the Neocognitron

The multilayer networks we covered in the last section of the course are not that similar to the human visual system. 

First, traditional networks are quite shallow, often with only one hidden layer, while the primate visual system has [many layers](van1992information.pdf)

Second, traditional networks are _densely connected_, in other words, every neuron in layer 1 is connected to every neuron in layer 2 and so on. The brain is generally much more _sparsely_ connected - there are many fewer connections than in a densely connected system. 

Third, this sparse connectivity is not random. Neurons in early visual cortex have simple _receptive fields_, i.e. they respond only to stimulation in a particular area of the visual field. And, as we've known since the work of Hubel and Weisel in the early 1960s, there is _neuronal tuning_, i.e. different neurons respond to different patterns in their receptive fields. For example, one might respond most to a vertical line, responding less as the line becomes less vertical. Another might respond most to a horizontal line, and so on. 

Fourth, as we go deeper into visual cortex, the cells become more [complex](https://en.wikipedia.org/wiki/Complex_cell), for example less sensitive to the position of the line in the receptive field. 

Many of these properties were built into Kunihiko Fukushima's ([pronounciation](https://www.howtopronounce.com/kunihiko-fukushima))  [Neocognitron](https://en.wikipedia.org/wiki/Neocognitron), which was published in 1980 and is the first example of what came to be known as a convolutional neural network. However, as with so much of the history of brain-inspired AI, it would be decades before this approach to object classification became dominant.

## LeNet

In 1989, Yann LeCun and colleagues published what is generally considered to be the first modern convolutional neural network. This system could classify handwritten digits with high accuracy - a practically useful task since postal ("zip") codes in the US are just digits. We'll spend some time looking at the structure of this groundbreaking system.

### The convolutional filter

At the heart of LeNet is the concept of the convolutional filter. Inspired by the structure of visual cortex, a convolutional filter has a receptive field - in our simple example a 2 x 2 square of pixels in a grayscale picture. A convolutional filter is just a single-layer network, like we studied before. It takes input from a number of units, four in our example, and this passes down connections of varying weight. The output unit sums all the inputs, and passes it through an activation function to produce an output. 

It's easier to see how this functions as a feature detector with a 3 x 3 receptive field. As shown in the example in class, one can come up with a set of weights that means the filter responds most strongly to a vertical line, less to a diagonal line, and not at all to a consistent luminance across its field. 

So far, there's nothing new here. What makes a convolutional filter different to a standard single-layer network is that the same filter - the same set of weights - is used all across the image. 

This makes the network dramatically more constrained. In a dense network with 256 inputs and 64 hidden units, there are 256 x 64 = 16,384 connections, each of which could take a different value. With a single 5 x 5 convolutional filter, there are just the 25 connection strengths of the filter. 

**Filter banks**: In the same way that different neurons in V1 have different tunings (different features they detect), so LeNet had multiple different filters - 12 filters, in fact.

### 3D convolutional filter

The next layer of LeNet is another set of convolutional filters. Like visual cortex, these more "complex" units have larger receptive fields. This is achieved in a similar way to the first set of filters. A given filter has one set of weights, that are applied across the image, generating a smaller number of output units than input units. In the case of LeNet, the output of a second-stage filter is a 4 x 4 set of units. 

However, it's a bit more complex in this second filter, because the input is not a single set of nodes - it's a set of 12 filters. To handle this, LeNet uses a 3D convolutional filter. This is just like the 2D filter, except that it takes the same 5 x 5 set of units from each of the previous filters.

**Filter banks**: Like the first convolutional layer, the 3D convolutional layer has 12 different filters.

Note: Any given 3D filter in LeNet only takes connections from 8 of the 12 2D filters, but I've ignored this for simplicity here, and because in more modern CNNs, all filters from the previous layer tend to be used. 

### Dense layers

Having developed a set of feature representations, the rest of LeNet is just a standard one hidden-layer network. Each of the 192 hidden units in the second convolutional layer are connected to each of the 30 units units in the next layer. Then, each of these 30 hidden units is connected to each of the ten output units (one for each of the digits being classified: 0 to 9). 

### Training with backprop

LeCun then trained the network using backprop; the network was trained on 7291 examples of single handwritten digits and was presented with each 23 times, for a total of 167693 training trials. It went on to make 5% errors on a test set of digits it had not seen before. 

In summary, LeNet could learn to classify handwritten digits from their images. Using a digital camera and a computer with some custom hardware, LeNet could classify the digits in US zip codes at around 10 digits a second with a 5% error rate. This is in the rough area of human-level performance in terms of accuracy, and arguably faster than people, too. Brain-inspired AI was able to solve the human-easy, AI-hard problem of digit recognition back in 1989. However, it learned very slowly and needed a very large set of examples to learn from  - needing almost 170,000 training trials across 7,000 different examples to learn 10 digits. 

## AlexNet

### Big data, big compute

It would take the field 20 years to get from the classification of handwritten digits to the classification of real-world objects ... like dogs, pigs, and loaves of bread. Why so long? It's tempting to assume that we were waiting for some brilliant insight, some breakthrough in the algorithms, that would allow the networks to learn at a more human-like rate. But no, progress in the field came from two sources. 

First, computing power has grown exponentially since 1970 ([Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law)). Around 2006, much of this [continued growth](https://www.nextbigfuture.com/2017/04/for-commoners-using-cpus-meaningful.html) came from hardware designed to play games - graphics cards (GPUs). It turned out that the sort of calculations one needs to make great graphics in games are similar to those one needs to train brain-inspired AI. In 2010, Dan Ciresan showed the potential of GPUs for deep learning, and the field quickly adopted this idea.

Second, when LeNet was published in 1989, there was no World Wide Web (1993), and no consumer-level digital cameras, let alone smartphones (2007). So, getting the very large sets of labelled pictures one would need to train a neural network was very difficult. However, by 2009, [ImageNet](https://en.wikipedia.org/wiki/ImageNet) had been launched - an online database that now contains around 14 million images - around several hundred images for common categories, and around 20,000 different categories of object. 

With these two revolutions in place, things moved quite quickly - within three years, AlexNet - a convolutional neural network trained on ImageNet using two GPUs - had won an international image classification competition, substantially beating the runner-up. Everything had come together at the right time, and AlexNet became massively influential, both in research, and in the real world. 

In research, the AlexNet paper has now been cited over [100,000 times](https://scholar.google.co.uk/scholar?hl=en&as_sdt=0%2C5&q=ImageNet+Classification+with+Deep+Convolutional+Neural+Networks&btnG=) - to give you a sense of scale, everything I've ever published in a 30-year career has been cited around [2,000 times](https://scholar.google.com/citations?user=SXkN-cgAAAAJ&hl=en&oi=ao) _in total_.

In the real-world, the startup company created by the authors of AlexNet was [acquired by Google](https://www.utoronto.ca/news/google-acquires-u-t-neural-networks-company) a year later, in 2013. Thus began a headhunt, with the top cognitive scientists who had spent long academic careers in these areas suddenly moving, part- or full-time, to major tech companies. [Geoff Hinton](https://en.wikipedia.org/wiki/Geoffrey_Hinton) joined Google and Yann LeCun [joined facebook](https://www.linkedin.com/in/yann-lecun/) the following year.

### Structure of AlexNet





## Plan
   

- AlexNet (Krizhevsky, Sutskever, Hinton, 2012)


   - Colour

   - Deeper 

   - ReLu
   
   - Grouping
   
- Why so deep? (Universal approximator paradox) ... what does the neural inspiration bring? (Fewer parameters - easier to train, less overfitting)

   - The problem of overfitting

- Big Tech wakes up

   - Purchase of the AlexNet company by Google
   
   - The great head hunt (facebook, Uber, Microsoft)

- ResNet (Microsoft, 2016)

   - Close to state of the art

   - Going deeper
   
   - Solving the network degradation problem
   
   - The idea of a Residual Network

- Applied uses

   - Content monitoring at facebook
   
   - Self-driving cars

- How good is state of the art?
 
   - The belief (Yamins & DiCarlo, 2016)
   
   - Top-5 accuracy
   
   - Top-1 accuracy
   
   - Objects in the real world (Barbu et al., 2019)
   
   - Overly-sensitive to tiny changes (Malhorta et al., 2020)
   
   - Insufficiently sensitive to shape (Baker et al., 2018)
   
- How do we make it better?

   - Take the neuroscience more seriously
   
   - Bias the learning rules against simple solutions. 


## Further reading

- [Neuroscience of the visual cortex](https://en.wikipedia.org/wiki/Visual_cortex)

- [Convolutional neural networks](https://en.wikipedia.org/wiki/Convolutional_neural_network)

- [History of GPU use for CNNs](https://people.idsia.ch/~juergen/computer-vision-contests-won-by-gpu-cnns.html)

- [History of machine learning](https://labelyourdata.com/articles/history-of-machine-learning-how-did-it-all-start)

- [AlexNet](https://en.wikipedia.org/wiki/AlexNet)

### Very mathematical

- [Universal approximation theoreom](https://en.wikipedia.org/wiki/Universal_approximation_theorem)
