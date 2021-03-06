# Action

## Rules of backgammon

## The challenge of backgammon

- There are 10^20 board states, so you can't just have a look-up table.

- The deep-search strategies used by, for example, chess computers don't work. At each turn, there are 21 possible dice combinations, and about 20 legal moves per dice combination. This is too large to reach reasonable depth, even for supercomputers. 

- Handcoding the knowledge of experts (hard, and expert knowledge changes over time)

- TD-gammon plays against itself. 


## Reinforcement learning 

- Agent observes a state (input pattern)

- Agent produces an action (output pattern)

- Agent receives a reinforcement as a number 

- Reinforcement is often delayed, only available at the end of sequence of states and actions. How does it apportion credit and blame to each of the various inputs and outputs? (temporal credit assignment problem). 

## Temporal difference

- [temporal difference learning](https://en.wikipedia.org/wiki/Temporal_difference_learning)

### Notes on Sutton (1988)

Will it rain on Saturday?

State : Prediction

Weather on Monday  : 50% rain on Saturday

Weather on Tuesday : 75% rain on Saturday - TD learning: OK, I could increase my prediction of rain on Saturday under the conditions seen on Monday. 


Sequence: x1, x2, ... xm, z - each x is a vector of observations at time t, z is the outcome. x are measurements or features; z is a scalar. 

Many such sequences observed

For each sequence the learner generates a set of predictions P1, P2, ... Pm, each of which is an estimate of z. 

In this example, each Pt is predicted from state xt. 

And that prediction is calculated from weights, and the state so prediction P is dependent on the state at time t and the weights - P(xt, w)

Learning is a rule for updating w. For now, w is changed only once for each outcome sequence. For each observation, delta wt is calculated. When a complete sequence is processed, delta w is the sum of all those changes. 

The calculation of delta_w at each timestep can be done in the normal way. For example, assuming a single-layer net, we can use the delta rule. Assuming a multilayer net, we can use backprop. 

The thing to notice, though, is that none of this can be done until the outcome is known.

But it turns out you can do this as you go along by using the prediction on time step t+1 as the teaching signal for the prediction on time step t, and multiplying, not by x (input activation on timestep t), but by the sum of x from timestep 1 to the current timestep. It's wild, but the maths turns out exactly the same as the 'at the end' calculation if you do this. 

Why bother? Because it saves on memory - you only have to store the sum of x, not each x. It also allows the computations to be spread over the time it takes to observe the sequence, rather than having to do them all at the end. 

This is known as the TD(1) algorithm, indicating that every previous time step contributes equally to the weight change calculation. 

As a variation, one can make more recent timesteps contribue more to the weight change on that timestep. In principle, one could use any decreasing function, but it's handy to use an exponential of the form lambda^(t-k) where 0 <= lambda <= 1. It's handy because you can work out the sum of x on the next time step by taking it on the previous timestep, multiplying by lambda and adding x on the current time step. This is known as the TD(lambda) algorithm.

From this, we can see that TD(1) is a special case of TD(lambda), but also that another special case is TD(0), which reduces to just the delta rule with the actual outcome replaced by the next prediction. 


### Notes on Tesauro (1991)
This is the original TD-gammon paper, reaching the performance of a tournament-level human player.

## Links

- [wikipedia Backgammon page](https://en.wikipedia.org/wiki/Backgammon)

- [Reinforcement Learning texbook - Sutton & Barto, 2020](http://incompleteideas.net/book/RLbook2020.pdf)

- [TD gammon implementation on github](https://github.com/dellalibera/td-gammon)

- [Expert player writes about TD-gammon](https://bkgm.com/books/Robertie-LearningFromTheMachine.html)

- [IBM RS/6000 used for TD-gammon](https://en.wikipedia.org/wiki/IBM_RS/6000#Type_7007)
