# Perception

## Opening videos

- 1997: IBM's Deep Blue computer beats world grandmaster Gary Kasparov at chess; the [BBC news clip](https://www.youtube.com/watch?v=KF6sLCeBj0s) marks the 20th anniversary of this success.

- 2019: [Tesla's full self-driving demo](https://www.youtube.com/watch?v=tlThdr3O5Qo)

- 2021: [Pig, dog, pig, dog, loaf of bread](https://www.youtube.com/watch?v=r2GjEvFUsYw) - In the 2021 film, [The Mitchells vs. The Machines](https://www.netflix.com/gb/title/81399614), an AI armageddon is averted in part through the limitations of AI object recognition. Current-day AI really is this bad at object recognition, at least sometimes. 

## Introduction

In the [core concepts](core.md) section of this course we saw that, by the end of the 1980s, we had developed multilayer artificial neural networks that could in principle learn any mapping between input and output, and that we had a system - backprop - that sometimes allowed them to learn this mapping for themselves. Yet, this brain-inspired approach would not make it to the forefront of developments in AI for more than twenty years. For example, a decade after backprop was popularized, a computer - [Deep Blue](https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer)) - beat the world chess champion Gary Kasparov. But there was nothing brain-inspired about how Deep Blue did this - it used what is known as [symbolic AI](https://en.wikipedia.org/wiki/Symbolic_artificial_intelligence), using large databases of previous chess games, and search algorithms specially written for the purpose of playing chess, plus new computer chips specifically designed to speed up those algorithms. The development of Deep Blue was the culmination of a 12 year project for engineer [Feng-Hsiung Hsu](https://en.wikipedia.org/wiki/Feng-hsiung_Hsu)  ([pronounciation](https://www.howtopronounce.com/feng-hsiung-hsu)) and the team that worked with him. 

## Moravec's paradox

While computers have been able to beat humans at chess since before most of the class were born, they're still not very good at recognising basic objects ... like dogs, pigs, and loaves of bread. This seems surprising at first sight, but it's a widely-observed problem in AI. As [Stephen Pinker](https://en.wikipedia.org/wiki/Steven_Pinker) once wrote, "the main lesson of thirty-five years of AI research is that the hard problems are easy and the easy problems are hard." ([Pinker, 1994](https://en.wikipedia.org/wiki/The_Language_Instinct)). In AI, this is often known as [Moravec's paradox](https://en.wikipedia.org/wiki/Moravec%27s_paradox), and roboticist [Rodney Brooks](https://en.wikipedia.org/wiki/Rodney_Brooks) (inventor of the [Roomba](https://en.wikipedia.org/wiki/Roomba) robot vacuum cleaner) has made similar observations.

## AlexNet

Ten years ago, a [paper](https://proceedings.neurips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf) was published that turned the world on to the idea that the hard problem of easy object recognition might be solved by brain-inspired AI. The roots of this work go back to 1980 - before the popularization of backprop. But, more than any other single paper, the work by Alex Krichevsky in 2012 - dubbed AlexNet -  influenced people to use brain-inspired AI to try and solve real-world object recognition problems. But, let's start from the beginning.

## Visual neuroscience and the Neocognitron

The multilayer networks we covered in the last section of the course are not that similar to the human visual system. 

First, traditional networks are quite shallow, often with only one hidden layer, while the primate visual system has [many layers](van1992information.pdf).

Second, traditional networks are _densely connected_, in other words, every neuron in layer 1 is connected to every neuron in layer 2 and so on. The brain is generally much more _sparsely_ connected - there are many fewer connections than in a densely connected system. 

Third, this sparse connectivity is not random. Neurons in early visual cortex have simple _receptive fields_, i.e. they respond only to stimulation in a particular area of the visual field. And, as we've known since the work of Hubel and Weisel in the early 1960s, there is _neuronal tuning_, i.e. different neurons respond to different patterns in their receptive fields. For example, one might respond most to a vertical line, responding less as the line becomes less vertical. Another might respond most to a horizontal line, and so on. 

Fourth, as we go deeper into visual cortex, the cells become more [complex](https://en.wikipedia.org/wiki/Complex_cell), for example less sensitive to the position of the line in the receptive field. 

Many of these properties were built into Kunihiko Fukushima's ([pronounciation](https://www.howtopronounce.com/kunihiko-fukushima))  [Neocognitron](https://en.wikipedia.org/wiki/Neocognitron), which was published in 1980 and is the first example of what came to be known as a convolutional neural network. However, as with so much of the history of brain-inspired AI, it would be decades before this approach to object classification became dominant.

## LeNet

In 1989, Yann LeCun and colleagues published what is generally considered to be the first modern convolutional neural network. This system could classify handwritten digits with high accuracy - a practically useful task since postal ("zip") codes in the US are just digits. We'll spend some time looking at the structure of this groundbreaking system.

### The convolutional filter

At the heart of LeNet is the concept of the convolutional filter. Inspired by the structure of visual cortex, a convolutional filter has a receptive field - in our simple example on the slides,  a 2 x 2 square of pixels in a black and white picture. A convolutional filter is just a single-layer network, like we studied before. It takes input from a number of units, four in our example, and this passes down connections of varying weight. The output unit sums all the inputs, and passes it through an activation function to produce an output. 

It's easier to see how this functions as a feature detector with a 3 x 3 receptive field. As shown on the slides, one can come up with a set of weights that means the filter responds most strongly to a vertical line, less to a diagonal line, and not at all to a consistent luminance across its field. 

So far, there's nothing new here. What makes a convolutional filter different to a standard single-layer network is that the same filter - the same set of weights - is used all across the image. 

This makes the network dramatically more constrained. In a dense network with 256 inputs and 16 hidden unit, there are 256 x 16 = 4,096 connections, each of which could take a different value. With a single 5 x 5 convolutional filter, there are just the 25 connection strengths of the filter.

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

It would take the field 20 years to get from the classification of handwritten digits to the classification of real-world objects ... like dogs, pigs, and loaves of bread. Why so long? It's tempting to assume that we were waiting for some brilliant insight, some breakthrough in the algorithms, that would allow the networks to learn at a more human-like rate. To a limited extent, that is true but mostly, progress in the field primarily came from two other sources. 

First, computing power has grown exponentially since 1970 ([Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law)). Around 2006, much of this [continued growth](https://www.nextbigfuture.com/2017/04/for-commoners-using-cpus-meaningful.html) came from hardware designed to play games - graphics cards (GPUs). It turned out that the sort of calculations one needs to make great graphics in games are similar to those one needs to train brain-inspired AI. In 2010, Dan Ciresan showed the potential of GPUs for deep learning, and the field quickly adopted this idea.

Second, when LeNet was published in 1989, there was no World Wide Web (1993), and no consumer-level digital cameras, let alone smartphones (2007). So, getting the very large sets of labelled pictures one would need to train a neural network was very difficult. However, by 2009, [ImageNet](https://en.wikipedia.org/wiki/ImageNet) had been launched - an online database that now contains around 14 million images - around several hundred images for common categories, and around 20,000 different categories of object. 

With these two revolutions in place, things moved quite quickly - within three years, AlexNet - a convolutional neural network trained on ImageNet using two GPUs - had won an international image classification competition, substantially beating the runner-up. Everything had come together at the right time, and AlexNet became massively influential, both in research, and in the real world. 

In research, the AlexNet paper has now been cited over [100,000 times](https://scholar.google.co.uk/scholar?hl=en&as_sdt=0%2C5&q=ImageNet+Classification+with+Deep+Convolutional+Neural+Networks&btnG=) - to give you a sense of scale, everything I've ever published in a 30-year career has been cited around [2,000 times](https://scholar.google.com/citations?user=SXkN-cgAAAAJ&hl=en&oi=ao) _in total_.

In the real-world, the startup company created by the authors of AlexNet was [acquired by Google](https://www.utoronto.ca/news/google-acquires-u-t-neural-networks-company) a year later, in 2013. Thus began a headhunt, with the top cognitive scientists who had spent long academic careers in these areas suddenly moving, part- or full-time, to major tech companies. [Geoff Hinton](https://en.wikipedia.org/wiki/Geoffrey_Hinton) joined Google and Yann LeCun [joined facebook](https://www.linkedin.com/in/yann-lecun/) the following year.

### Structure of AlexNet

So, how does AlexNet differ from LeNet? Here, I'm going to give a simplified description, for full details read the [AlexNet paper](krizhevsky2012imagenet.pdf). In particular, I'm not going to cover the concept of _max pooling_, which is used in AlexNet but is now increasingly considered to cause problems and is not a major feature of most state-of-the-art models today. I'm also not going to cover their techniques of _data augmentation_ - basically taking the set of training images and generating many more images from them by using automated PhotoShop-like techniques. 

Basically, though, having faster computers and bigger sets of images meant that we now had enough computing power and enough training items to train much larger, more complex networks. AlexNet was more complex that LeNet in the following ways:

**Hi-res colour**: AlexNet is designed to use higher-resolution, coloured images. LeNet took images that were 16 x 16 pixel black-and-white images. AlexNet takes 256 x 256 pixel images in full colour. Handling higher resolution is just a matter of more computing power, but handling colour needed some modification. In AlexNet, the three colour channels of the image - red, blue, and green - are used as the input to a 3D convolutional layer. So, while LeNet uses 2D convolution on layer 1 and 3D convolution in layer 2, ALexNet uses 3D convolution from the outset.

**Deeper**: The convolutional part of AlexNet is much deeper than LeNet. LeNet had two convolutional layers, while AlexNet has five convolutional layers. Similarly, LeNet has two dense layers, while AlexNet has three. The authors were able to demonstrate that the depth of AlexNet was important to its performance - training a version of AlexNet with even one less convolutional layer led to worse performance. 

**ReLU**:  Since the 80s, neural networks typically used a sigmoid activation function or similar. AlexNet uses a rectified linear (ReLU) system, where if the input is negative, the output is zero, otherwise the output is the same as the input. [Nair and Hinton](https://icml.cc/Conferences/2010/papers/432.pdf) had come up with this idea a couple of years earlier, and in the AlexNet paper they report simulations that show this change of activation function speeds learning by a factor of six. Given AlexNet took around 6 days to train, this makes a big real-world difference - without ReLU, AlexNet would likely take more than a month to train. One irony of ReLU, as with backprop, is that it isn't neurally plausible - neurons have a maximum firing rate as well as a minimum firing rate, and this was one of the original inspirations of the sigmoid function.

**Grouping**: There were a couple of other things AlexNet did. The first one was considered by them to be a "hack" to get around hardware limitations, but was later discovered to improve performance. This was 2012, and AlexNet needed too much memory to fit on a single GPU card of the time. So, they split the network across two cards, and they did this by splitting the filters - so half the filters for a given layer run on one graphics card and the other on the second graphics card. As well as solving the technical problem, it simplifies the network - there are fewer connections in total, and it turns out this improves performance - see the ResNeXt model [Xie et al., 2017](https://arxiv.org/pdf/1611.05431.pdf). We'll come back later to why that might be. 

**Dropout**: The other thing they did, quite deliberately to improve performance in this case, was to use _dropout_. Dropout is where, on every training trial, you ignore a random 50% of the connections in a layer. These ignored connections don't pass activation forward, nor error back. It's a different 50% of connections each time. This roughly doubles the amount of time it takes to train the network, but it also improves its ultimate performance in much the same way as grouping does - see [Hinton et al. (2012)](https://arxiv.org/pdf/1207.0580.pdf). Again, we'll come back to that later.

## ResNet

What's happened in this area in the last 10 years? For the purpose of this session, we're only going to go up to 2016, because that's when a research group at Microsoft introduced ResNet ([He et al., 2016](https://arxiv.org/pdf/1512.03385v1.pdf)). Although that was a few years ago now, it's still pretty close to the state of the art.

The period 2012 to 2016 was characterised by increasing the depth of the network. LeNet had 4 layers, while AlexNet had 8. So, more seemed like better. Over the next few years this increased to 16 layers in [VGG](ttps://arxiv.org/pdf/1409.1556.pdf) and around 30 layers in models like [Inception](https://arxiv.org/pdf/1409.4842v1.pdf). This did lead to perfomance gains, so the strategy seemed justified.

The thing was, though, as the networks got deeper, they got harder and harder to train. A number of approaches were taken to address this, but the ResNet team brought to the world's attention that the problem remained unsolved.

The ResNet team included lead author Kaiming He, and senior scientist Jian Sun, both working at Microsoft Research, an offshoot of the company that brought you Microfost Windows, and Microsoft Office. This team pointed out that deeper networks were not just harder to train; after a certain point their terminal performance at the end of training was not as good as a shallower network. 

This is very odd. A deeper network never needs to be worse than a shallower network. The easiest way to see this is to take the shallower network and add a number of layers that do nothing but copy the input they get and pass it to the next layer (these are called _identity_ layers). You can add as many of these layers as you like without changing the performance of the network. 

The ResNet team therefore hypothesized that if you gave the network these identity mappings, it might learn better. So ResNet is made of builing blocks of some convolutional layers with a "shortcut" set of identity connections - they just pass the input of the building block to its output. The block's job is therefore to learn the mapping between the input and the output _minus_ the input. This is known as _residual_ learning, the term _residual_ coming from statistics, meaning what is left over after, for example, assuming the points fall on a straight line. (There was also another trick they used, called a _bottleneck building block_. We didn't cover this in class because [later work](https://arxiv.org/pdf/2003.13678.pdf) indicates that such bottlenecks do not help.) 

With this concept of residual building block, the ResNet team were able to further increase the depth of their networks, first to 34 layers, then 50 layers, and ultimately 152 layers. In 2016, ResNet152 was state of the art. Things have not improved that much since then, and ResNet-like systems are still in use today in state-of-the-art applications.

## Applied uses

What are those applications? It's hard to be sure, because while companies such as facebook appear to be using AI extensively, getting details on exactly what they do and how can be tough. 

One thing we do know is that the convolutional neural networks we've discussed can be used to [automatically detect pornographic images](https://arxiv.org/pdf/1511.08899.pdf) (Moustafa, 2015), and so there's a reasonable chance facebook and other social media companies use CNNs in this way to block pornographic content. 

An area where we know CNNs are used is in self-driving cars. In summer 2021, Tesla did a [3-hour live stream](https://www.youtube.com/watch?v=j0z4FweCy4M) on how the AI works in their AutoPilot system. If you can spare the time, watch the whole thing, it's the best introduction to state of the art in autonomous vehicles I've seen. The [self-driving demo](https://www.youtube.com/watch?v=tlThdr3O5Qo) we viewed in class was from 2019.

## Why so deep?

So, brain-inspired neural networks are being used in real-world applications that, in some senses, allow machines to see. But why do they have so many layers? Earlier in the course, we covered the fact that any multilayer network with sufficient hidden units can represent any deterministic mapping between its inputs and its outputs. So, in principle, the other 150 layers of ResNet152 just aren't needed. So, why have these deeper, sparser, more brain-like systems been so successful?

The answer is that, despite being deeper, CNNs are in fact simpler than traditional densely connected networks. A modern CNN takes images that are 224 x 224 x 3. So, they have about 150,000 input units. They classify that input into perhaps 1,000 categories. And it's not unusual for a densely connected network to have as many hidden units as input units (often, it's many more). But let's be conservative and say you only need half as many hidden as input units. This still gives you around 11 billion connections. ResNet50 has around 25 million parameters - that's about 400 times fewer connections. 

Having fewer connections makes the network faster to train. It also reduces the networks' ability to _overfit_. Conceptually, we can think of overfitting as when a model tries to fit the noise in a set of data - the stuff that you would not see again if you collected the data again. In statistics, for example, we often fit a simple straight line model to data - we call this linear regression. Overfitting could be illustrated by instead connecting the data points in a dot-to-dot fashion. Such a line fits the data more closely, but is not particularly useful for predicting what will happen in future.

In a similar way, if the number of connections in a network grows too large, it will tend of overfit the training sample. We can see this happening when we test the network on pictures it hasn't yet seen - if it's dramatically worse on these test items than on the training items, the likelihood is that the model is overly flexible, it has too many parameters, and it has overfit the training data.  CNNs, relative to dense networks, reduce the number of parameters and hence potentially reduce the chances of overfitting. 


## How good is the state of the art?

How good are modern object recognition systems? Ancedotally, really good! There are plenty of examples, from about 2014 onwards, of both software engineers and neuroscientists claiming human-level performance for these systems. 

We can put numbers to this. A relatively recent system - [PNASNet](https://openaccess.thecvf.com/content_ECCV_2018/papers/Chenxi_Liu_Progressive_Neural_Architecture_ECCV_2018_paper.pdf) - scored over 95% accuracy on ImageNet. This sounds pretty impressive, until you notice that "Top 5" condition. To explain - when the model is presented with an image of say, a cat, we look at the five things the model thinks it is most likely to be. Now, let's say the model says it's most likely to be a hatstand, and if not an orange, but if it's not that they maybe a battleship, but if not a dandelion, but if not it's a cat ... then it counts as getting it right. This does not seem like such a great measure. A more realistic answer comes from what's called "Top 1" performance, also known as ... getting it right. On this basis, the model gets about a quarter of all images wrong, which doesn't necessarily sound that human-like.

But that's not the end of the story. As we already covered, these systems are trained on very large sets of images. In order to create such large sets, engineers trawl the internet. That's all very well, if the internet contains a representative subset of the objects in our world. But the evidence is that it doesn't. Andrei Barbu and colleagues, working at MIT, took what is quite a psychological approach to this problem and collected a [much better controlled set of images](https://proceedings.neurips.cc/paper/2019/file/97af07a14cacba681feacf3012730892-Paper.pdf). They did this by directing people, via their phones to take pictures of objects at a range of different angles and against a range of different backgrounds. However, the computer systems do appallingly on this more representative subset. In fact, they get most things wrong, with a Top-1 accuracy of around 30%. 

How good are people on these better-controlled images? Perhaps people would also struggle, given the variety of objects and backgrounds? We collected some data on this question.

In this experiment we chose 10 categories of object from the Andrei Barbu's set. We didn't pick 10 categories at random. Rather, we picked 10 categories which, on the basis of simulations run by Andrei, were among the hardest for ResNet152. They're all pretty every day types of category, which a priori we would think people would be reasonably competent at classifying. For each of the 10 categories, we sampled 30 example pictures, giving us 300 images in total. Each image was presented for a fixed amount of time, then removed. The participant then has as much time as they like to make their selection by pressing the appropriate number key. The numbered list remains on the screen when the picture disappears, so performance on this task is presumably driven mainly by object recognition performance rather than, say, difficulty in using the response system. 

We used two different presentation times - 200 ms and 1000 ms. The relevance of 200 ms is that systems like ResNet are feedforward only. The brain's visual system is recurrent - in other words it also has feedback links -  but at 200ms there is little time for recurrent activity, reducing the humans to (approximately) a feedforward system. We chose 1000ms as a longer-interval comparison, while keeping it short enough for the whole experiment to fit within a single 30 minute session. 

As we can see from this slide, people were way better than a leading AI system. The blue bars, somewhat misleadingly labelled 'as objectnet' are in fact the performance of ResNet152 - a leading AI system - on these ten categories. The comparison is only approximate, because the ResNet results come from Andrei's paper, and are hence assessed across all the images in his set for each category -- rather than the subset of 30 images per category we showed the participants. Nonetheless, it gives us a ball park figure, which is that ResNet is between 1% and about 13% accurate, depending on the category. Even at 200ms, people are much better than this - generally between 80% and 90% accurate.

## How do we improve the state of the art?

Clearly, there is a problem to solve. Artificial neural networks, which at first sight seem quite good at object recognition and also quite neurally inspired, turn out to be really brittle. Do psychology or neuroscience hold any clues? As I mentioned earlier, one difference was that the machines are feedforward while the human brain also has feedback connections. This may be part of the answer, but the high accuracy people show at 200 ms in our study suggests that even the feed forward part of the human system well exceeds machine performance. So, what are the machines doing wrong? Well, perhaps they are not human enough. Because, despite superificial similarities, these systems are not currently that human like.

For example, for humans, the overall shape of an object is among the most important things that identify it as that object. The shillouette at the top left is clearly a camel. The one on the bottom left is not a camel - or, at least, a horribly injured or deformed one. To the machine, these are equally good examples of camels ([Baker et al., 2018](https://journals.plos.org/ploscompbiol/article/file?id=10.1371/journal.pcbi.1006613&type=printable)).

Another example - or perhaps the other side of the same coin - is that these machine systems have a very strong prior to select the simplest solution. In a study by [Malhotra et al.](https://cpb-eu-w2.wpmucdn.com/blogs.bristol.ac.uk/dist/1/411/files/2021/05/1-s2.0-S0042698920300742-main.pdf), the images the machine is trained on have a single pixel -- near invisible to the human eye -- that perfectly predicts the category membership of the item. The system correctly classifies the objects when that pixel is preserved. However, it gets all the answers wrong when that single pixel is changed to one that predicts a different category. Even if you take the single pixel out, rather than replacing it with a misleading one, the machine systems suffer a very substantial loss of accuracy. People, presumably, don't suffer from this kind of problem. 

I think the direction one needs to go in, in terms of the development of these machine systems, is to work on making them less brittle. And, the human brain seems like a pretty good exemplar of a system that does not break so easily as the machine systems. So, perhaps the way forward here is to develop machine systems that are more human like. For example, work by [Evans et al. (2022)](https://cpb-eu-w2.wpmucdn.com/blogs.bristol.ac.uk/dist/1/411/files/2022/02/1-s2.0-S0893608021004780-main.pdf), who have attempted to build machine systems whose lower layers are more directly modelled on the known properties of early visual cortex, and there seem to be some interesting results there.

## Summary

By 1997, computers could beat the best humans in the world at playing chess, but apparently simple tasks like classifying everyday objects turned out to be much harder. The brain-inspired roots of trying to solve this simple-hard problems of everyday life start in 1980, when Fukushima built a network that was more like the primate brain than the systems we'd previously looked at. His neocognitron was deeper - it had more layers of connections. It was sparser - there were fewer connections. And these connections were not random, they were arranged into receptive fields. In 1989, Yann LeCun published the first modern network of this type, networks that came to be known as convolutional neural networks. His creation, LeNet, could classify handwritten digits to high levels of accuracy. 

It would take more than 20 years to get from handwritten digits to photographs of everday objects. Not much changed in those 20 years in terms of the basic design of these CNNs - what changed was that we got a lot more computing power. And, thanks to the internet, we got access to very large sets of images to train the networks on. These things came together in AlexNet in 2012, a massively influential brain-like system that beat less brain-like systems in a major competition. AlexNet was deeper than LeNet, and also used some design improvements, like ReLU and dropout. 

The next four years was a period of rapid development, with CNNs getting progressively deeper. One barrier to increasing depth was the network degradation problem - as networks got beyond about 20 layers, their performance on the training items got worse. In principle, this should never happen because the deeper networks could always just copy the output of the shallower network across its extra levels. This insight led the ResNet team to explicitly include these identity connections as shortcuts in the network. This was sufficient to allow very deep networks, with ResNet152 having 152 layers of connections. 

The use of CNNs for object recognition began to become commerical from around 2013. Today, most Big Tech companies use CNNs as part of their AI systems. For example, it seems likely that facebook use them for content moderation, and we know that they form part of the self-driving AutoPilot system in Tesla cars.

The success of CNNs is in some ways paradoxical. We know that multilayer nets are universal approximators, so in principle anything that ResNet152 does with all its layers could be done with just two layers of connections. One of the advantages of CNNs is that they are, despite their depth, much less complex than a shallow, fully-connected network. This makes them easier to train, and it also seems to make them less prone to over-fitting. 

For about a decade now, people have been claiming that CNNs had reached human levels of performance in object classification. This claim does not seem to be well founded, as a series of studies from around 2018 onwards has demonstrated. Real-world classification performance of CNNs sits around 70% errors according to the ObjectNet benchmarks, while people generally make fewer than 10% errors on the same benchmarks. Also humans, quite sensibly, use shape as a primary predictor of object categories, while networks do not and so end up making some odd decisions. They are also overly sensitive to minute, irrelevant details in images in a way people are not. Perhaps further work in making these systems more like primates will help.

## Further reading

- [Neuroscience of the visual cortex](https://en.wikipedia.org/wiki/Visual_cortex)

- [Convolutional neural networks](https://en.wikipedia.org/wiki/Convolutional_neural_network)

- [History of GPU use for CNNs](https://people.idsia.ch/~juergen/computer-vision-contests-won-by-gpu-cnns.html)

- [History of machine learning](https://labelyourdata.com/articles/history-of-machine-learning-how-did-it-all-start)

- [AlexNet](https://en.wikipedia.org/wiki/AlexNet)

- [Real-world applications of machine learning](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7983091/pdf/42979_2021_Article_592.pdf)

- [Machine learning at Big Tech companies](https://medium.datadriveninvestor.com/how-machine-learning-is-applied-at-big-tech-companies-73b11cd79745)

- [Anything by the Bristol Generalization Group](https://mindandmachine.blogs.bristol.ac.uk/publications/)

### Very mathematical

- [Universal approximation theoreom](https://en.wikipedia.org/wiki/Universal_approximation_theorem)

