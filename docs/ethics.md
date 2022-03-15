# Philosophy and ethics
## Session plan

This session is a bit of a break from the somewhat technical content we've covered so far; we're going to go beyond the specifics of how to build a brain-inspired AI to what the philosophical and ethical implications are of building such a thing. We'll start with _narrow AI_ - systems that are not general intelligences, but which do specific tasks which, if done by a human, might be considered intelligent. Narrow AI, in various forms, is already here. Later in the session, we'll look ahead to the possibility of an AGI - an artificial _general_ intelligence, whether that's possible, when it might happen, and what that means for the future of human society.

Here are some questions I'd like you to think about, and do some googling on, before the next session. Bring notes -  they'll form the basis of our discussion in class:

- How is narrow AI being used today in real-world applications?

- What benefits and problems do these uses of narrow AI bring?

- Is artificial general intelligence possible? 

    - How would you tell?

    - If AGI is not possible, why not? 
	
	- If AGI is possible, how far away are we, and what will it mean for human society?

- What ethical principles should underly the building and use of AI systems?

Below are a set of notes written by me before our discussions. They represent some of the reading I've done on this topic, and provide a resource to support our discussions, and your essay writing if you choose this assessment.

## Narrow AI
### Self-driving cars

As we saw in a previous session, Tesla's AutoPilot is an amazing technological achievement, but people perhaps have a little [too much faith](https://www.youtube.com/watch?v=qnZHRupjl5E) in self-driving vehicles. For example, an Uber autonomous vehicle in 2018 failed to stop for a pedestrian, hitting them at speed and killing them - [disturbing video](https://www.youtube.com/watch?v=R8Up9Ph_a0Y), and [detailed examination of causes](https://en.wikipedia.org/wiki/Death_of_Elaine_Herzberg). Who is to blame when a self-driving car has an accident? -  [opinion article](https://futurism.com/who-responsible-when-self-driving-car-accident)

### Algorithmic decision-making

In 2020, due to COVID, A-level grades were [determined by an algorithm](https://www.theguardian.com/education/2020/aug/17/inbuilt-biases-and-the-problem-of-algorithms). 40% of grades were adjusted downwards, relative to teacher assessments. The algorithm used a per-school distribution of grades in the period 2017-2019, and the result was that top students from deprived areas were the worst affected. This [blog post](https://philojen.wordpress.com/2020/09/03/yet-another-biased-algorithm/) represents the view that this isn't an example of narrow AI - but what's the different between narrow AI and an algorithm? Is there one?

Predictive policing is another area where algorithms are used, or could be in the future. For example, to estimate likelihood of reoffending and hence prison term, or likelihood to join a gang and hence surveillance [Whitehall report](https://static.rusi.org/201809_whr_3-18_machine_learning_algorithms.pdf.pdf)

### Automatic face recognition

Automatic face recognition technologies are in use today, for example in border patrol and criminal investigations. It's also used in housing decisions. All modern systems are examples of brain-inspired narrow AI (they make extensive use of convolutional neural networks). Under certain, limited, conditions, they are good at this job. But not if you're female and have darker skin. [blog post](https://sitn.hms.harvard.edu/flash/2020/racial-discrimination-in-face-recognition-technology/), [primary source](http://proceedings.mlr.press/v81/buolamwini18a/buolamwini18a.pdf)

### Meaning from text

Google's [word2vec](https://code.google.com/archive/p/word2vec/) is publicly available. It's a narrow AI system that's been trained on 3 million English words in Google News, and is able to return semantic similarities for words. It's quite competent at certain kinds of language aptitude tests. For example, when posed "Paris is to France as ____ is to Japan", it's able to return "Tokyo". However, it also has some very strongly gendered stereotypes - for example that women are lovely while men are brilliant. [primary source](https://proceedings.neurips.cc/paper/2016/file/a486cd07e4ac3d270571622f4f316ec5-Paper.pdf)

This sort of system is used in the automatic shortlisting of job candidates from their CVs. For example, when Amazon hired computer programmers, it used to use an automatic system of this sort. It was trained on data from the previous 10 years of hiring decisions. Computer programming has, in recent decades, been male dominated. And their system learned that things which predict the candidate is a woman - such as the entry "women's chess club captain", or that they went to an all-women university, also predict that they don't get the job. So, they ended up with a system that penalized candidates for being female. [news article](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G)


### Deep fakes
 
In 2020, Channel 4 released an alternative Queen's Speech, using [deepfake technology](https://www.youtube.com/watch?v=IvY-Abd2FfM). Although the technology behind this goes beyond what we've covered in class, it's a development of the brain-inspired AI we've studied. Mostly commonly used are a [Generative Adversarial Networks](https://en.wikipedia.org/wiki/Generative_adversarial_network) [primary source](https://proceedings.neurips.cc/paper/2014/file/5ca3e9b122f61f8f06494c97b1afccf3-Paper.pdf). This is a pair of neural networks - a generator and a detector. A detector might be a fairly standard deep convolutional network - it takes images as input. But it's job is to learn to distinguish between real images (say, of the queen), and fake images. The fake images are made by the generator network. The generator network could be a CNN in reverse - it starts with a feature-based representation and this is expanded back into an image. The generator network is fed random input, and learns through gradient descent to get better at fooling the detector. At the same time, the detector learns to get better at detecting fakes through gradient descent. The two networks are adversaries, both getting better over time by competing with one another. 

Although GANs can be used to make deepfakes, they can also be used to create new things. It's already possible to create photorealistic images of people who don't exist, and to turn photographs into paintings in a particular artistic style.

## Artificial General Intelligence

An [Artificial General Intelligence](https://en.wikipedia.org/wiki/Artificial_general_intelligence) contrasts with narrow AI in that it is ability to deal with the world is broader. The task at which it is intelligent is life. Although we tend to think of this as human-level intelligence, that's not a necessary criterion. It seems like other species are intelligent to some extent - so one might conceive of a cat AGI, or a bee, or a worm. Also, do we think that human intelligence represents some kind of natural limit ... that it is not possible to be substantially more intelligent than a human? If not, we can conceive of AGIs that have superhuman intelligence. 

### When AGI?

Like much of the rest of AI research, we go through periods of optimism and pessimism about how likely human-level AGI is, and how imminent. [Herb Simon](https://www.youtube.com/watch?v=ABucG05nurs), a psychologist and political scientist, thought AGI would be here by 1985. He was wrong. [Paul Allen](https://en.wikipedia.org/wiki/Paul_Allen), co-founder of Microsoft, [doesn't think we'll see AGI this century](https://www.technologyreview.com/2011/10/12/190773/paul-allen-the-singularity-isnt-near/). Given some [predictions](https://www.futuretimeline.net/data-trends/20-supercomputer-future-prediction.htm) about the future growth in computing power, we might view that as a similarly striking prediction.

### Whole-brain emulation

One perspective on AGI is that computers are, or soon will be, powerful enough to upload a complete working copy of a human brain. [Ray Kurzweil](https://en.wikipedia.org/wiki/Ray_Kurzweil) - [synthesizer maker](https://www.youtube.com/watch?v=FjQquf-WRv0) turned futurist - estimated in 1997 that the brain has perhaps 10 petaFLOPs of compute power. We've had computers that powerful since 2011. So, in principle, this should be a solved problem by now, right? Well, less than 10 years after Kurzweil's predictions, we got some sense that the problem was much harder than he thought. The [Blue Brain](https://en.wikipedia.org/wiki/Blue_Brain_Project) project, in 2006, managed to simulate 10,000 neurons in real time (cf. 85 billion neurons in the human brain). The director of the Blue Brain project, Henry Makram said in 2009 "It is not impossible to build a human brain and we can do it in 10 years". 

So, that would be 2019. How's it going? One informative case is the [OpenWorm](https://en.wikipedia.org/wiki/OpenWorm) project. This is an attempt to build a complete working model of a worm brain. The worm in question has 302 neurons, and we know how they are connected. But, we still haven't managed to build it yet! [article on progress](https://www.lesswrong.com/posts/mHqQxwKuzZS69CXX5/whole-brain-emulation-no-progress-on-c-elgans-after-10-years)

It may also be that whole-brain emulation is not enough. We are not a brain in a jar - perhaps the relevant thing to replicate is not just the brain, but a brain in a body, in an environment to which it is adapted. In psychology, we sometimes call this [embodied cognition](https://en.wikipedia.org/wiki/Embodied_cognition)

### Detecting AGI 

If we have an AGI, how would we tell? One standard idea is the Turing test [Turing test](https://en.wikipedia.org/wiki/Turing_test) - you get the chance to talk to both a human, and a computer. If you can't tell which is which, the computer is intelligent. A common counterargument is known as the [Chinese Room](https://www.youtube.com/watch?v=D0MD4sRHj1M) - following instructions to respond in Chinese (running computer code) does not imply understanding. 

Attempts to pass the Turing test go back to the 1960s and 1970s, with programs such as the virtual psychotherapist ELIZA [try talking to ELIZA](https://web.njit.edu/~ronkowit/eliza.html), and the virtual paranoid schizophrenic PARRY [try talking to PARRY](https://www.botlibre.com/browse?id=857177). State of the art chatbots - assessed by, for example, their likelihood of passing the Turing test, via the [Loebner Prize](https://en.wikipedia.org/wiki/Loebner_Prize) - are Kuki [try talking to KUKI](https://chat.kuki.ai/chat) and Sophia. Who, apparently, is going to [destroy humans](https://www.youtube.com/watch?v=W0_DPi0PmF0)

### Malevolent AGI

If you believe Hollywood movies, the possible arrival of AGI does not bode well for humans. In _2001: A Space Odyssey_, the [HAL9000](https://en.wikipedia.org/wiki/HAL_9000) AGI, which has "never made an error", attempts to kill its human crewmates because it's been told to both tell the truth, and withold information from its crewmates. It solves the problem by killing its crewmates, thereby avoiding having to lie to them [video clip](https://www.youtube.com/watch?v=ARJ8cAGm6JE&t=48s). In the _Terminator_ films, super-human American-built AGI [Skynet](https://en.wikipedia.org/wiki/Skynet_(Terminator)) starts a nuclear war by bombing the Russians. It does this because it knows the Amercians are trying to turn it off, and knows that if it nukes the Russians, they will retaliate and kill the Amercians [video clip](https://www.youtube.com/watch?v=1UZeHJyiMG8). 

Back in the real world, people deeply involved in AI applications seem to be concerned [video: Elon musk warns about dangers of AI](https://www.youtube.com/watch?v=9jkRcrM6XKA&t=415s)
 
Probably the most common reaction to all this The Big Red Button. In other words, just turn it off! This turns out to be not as easy as you might think [video: stop button problem](https://www.youtube.com/watch?v=3TYT1QfdfsM). Some current AI systems learn to disable their big red button, because doing so makes them more efficient at achieving the goal they have been set. [blog post](https://deepmind.com/blog/article/specifying-ai-safety-problems), [primary source](https://arxiv.org/pdf/1711.09883.pdf). 

A related but more general problem is how to build a system that will remain 'good', rather than, for example, learn to suppress information. In an experiment in artificial evolution of robots, an 'genetic code' specifies the connections strenghts in the robots neural network. The robots most successful in locating 'food' in the environment get to sexually reproduce. Over time, this results - as you would expect - in robots that are better at finding the food. However, these robots also start off randomly emitting blue light. As the robots become better at finding food, the presence of blue light signals the location of the food, because robots are more likely to be near the food than far from it. However, the food is limited so randomly emitting blue light reduces the amount of food you get. The robots evolve to, largely speaking stop emitting blue light [primary source](https://www.pnas.org/doi/pdf/10.1073/pnas.0903152106).
 
### Benevolent AGI

Assuming we can avoid building an AGI that acts towards our destruction, the consequences could still be large. What is the future of work, for example? [Agriculture](https://en.wikipedia.org/wiki/Agriculture) was a new technology around 200 human lifetimes (12,000 years) ago. 7 lifetimes ago (16th century), around 60% of people in Europe were farmers. Even 3 lifetimes ago (19th century), 40% were. Now it's less than 10%. What happened to all the farmers? Well, they found something else to do. How about typing pools? What jobs will AI technologies affect in the next three lifetimes? Or, indeed, the next 10-20 years? [news article](https://www.theguardian.com/us-news/2017/jun/26/jobs-future-automation-robots-skills-creative-health), [primary source](https://www.oxfordmartin.ox.ac.uk/downloads/academic/The_Future_of_Employment.pdf). 


## Further reading

- [Ethics of artificial intelligence](https://en.wikipedia.org/wiki/Ethics_of_artificial_intelligence#Robot_rights)

- Principles for AI ethics: [Jobin et al., 2020](https://arxiv.org/pdf/1906.11668.pdf)
 
- The [control problem](https://en.wikipedia.org/wiki/AI_alignment): how does one ensure a superintelligent AI is benevolent?

- [Three laws of robotics](https://en.wikipedia.org/wiki/Three_Laws_of_Robotics)

- [Tay](https://en.wikipedia.org/wiki/Tay_(bot)) chatbot, designed to [tweet like a teenager](https://www.youtube.com/watch?v=v6sEcfxsF2E), learned from the tweets it received and [became a massive racist](https://www.youtube.com/watch?v=eTdyucscPnQ). 


- [Leverhulme Centre for the Future of Intelligence](https://en.wikipedia.org/wiki/Leverhulme_Centre_for_the_Future_of_Intelligence)

- [Map of AI use](https://map.ai-global.org/)

- [Facebook, AI and hate speech](https://www.technologyreview.com/2021/03/11/1020600/facebook-responsible-ai-misinformation/)

- [The Use of Knowledge in Society](https://en.wikipedia.org/wiki/The_Use_of_Knowledge_in_Society): Although economics, like embodiment, this work leads us to think about what the appropriate "unit" of intelligence is. Is it the individual who is representative of human intelligence, or the collective action of billions of minds?

- [Whole-brain emulation](https://en.wikipedia.org/wiki/Artificial_general_intelligence#Whole_brain_emulation)

 - [ELIZA](https://en.wikipedia.org/wiki/ELIZA) - mid60's computer therapist

 - [PARRY](https://en.wikipedia.org/wiki/Kenneth_Colby#PARRY:_A_Computer_Model_of_Paranoia) - a paranoid computer

 - [Kuki](https://en.wikipedia.org/wiki/Kuki_AI)
 
 - Sophia (citizen of Saudi Arabia): [Interview](https://www.youtube.com/watch?v=Sq36J9pNaEo), [article](https://en.wikipedia.org/wiki/Sophia_(robot)), [source code](https://github.com/hansonrobotics) 

 - Weizenbaum (1976) : AI should not be used to replace people in positions that require respect and care (see [Computer Power and Human Reason](https://en.wikipedia.org/wiki/Computer_Power_and_Human_Reason)). 
