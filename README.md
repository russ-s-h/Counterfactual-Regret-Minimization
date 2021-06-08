# Counterfactual-Regret-Minimization

Algorithm obtained from [An Introduction to Counterfactual Regret Minimization](http://modelai.gettysburg.edu/2013/cfr/cfr.pdf).

## Rock, Paper, Scissors

The game of Rock Paper Scissors is fairly simple. For our case, lets suppose we are playing Rock Paper Scissors for money and because it is a childrens game we will only play for a dollar a game. If there is a winner the player takes both dollars, otherwise each player retains their dollar. Thus defining the pay-off matrix of the game as:

|   |   R  |   P  |   S  |
|---|:----:|:----:|:----:|
| R |  0,0 | -1,1 | 1,-1 |
| P | 1,-1 |  0,0 | -1,1 |
| S | -1,1 | 1,-1 |  0,0 |

## Regret Matching

The most essential part of Counterfactual Regret Minimization is the concept of "regrets". A "regret" is the understanding that it would have been better to play a different move instead of the one that was played. For example, if the algorithm plays rock while a human plays paper, the algorithm will "regret" not playing either paper or scissors (but will regret not playing scissors more cause that would have mean earning a dollar).

However choosing the action that you most regretted previously is not a wise descision as this can be easily exploited by an intellegent opponent. One way of acheviving such a strategy (that can't be exploited) is by using *regret matching* where the next action is selected at random with a distribution that is proportional to positive regrets.

The algorithim for `innerTrain` is as follows:

1.   Compute a regret-matching strategy profile.
2.   Add the strategy profile to the strategy sum.
3.   Select each player's action according to their strategy.
4.   Compute the regrets.
5.   Add the player's regrets to each player's cummulative regret.

## RPS Equilibrium

In any two player zero-sum game (like Rock Paper Scissors) if both players use regret matching to update their strategies as the number of interations tends to infinity, the pair of strategies converge to a Nash Equilibrium.

**But can we prove it?**

In `train2p` we train both players against each other's strategy. We employ a similiar strategy to `train` however we wish to train both players through a number of rounds (defined as `oiterations`).

When both players use CFR, the strategies approach 0.33333, 0.33333, 0.33333. This is the logical resting place for this strategy going up against itself, as it will throw rock about 1/3rd of the time, throw paper about 1/3rd of the time, and throw scissors 1/3rd of the time (and thus proving the Nash Equilibrium point for Rock Paper Scissors as neither player has no other maximizing strategy available).