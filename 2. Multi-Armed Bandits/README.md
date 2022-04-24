# Chapter 2 Exercises
### Exercise 2.1
**如果是*ε-贪婪*动作选择，对于两个动作且ε = 0.5的情况，贪婪动作被选择的概率是？**

概率是75%，由两部分构成：
- 50%概率源自选择贪婪动作，即1-ε = 1-0.5 = 0.5
- 25%概率源自随机动作，即ε*(1/2) = 0.25


### Exercise 2.2: *赌博机的例子*
**考虑一个*k*=4的多臂赌博机问题，几座1、2、3、4。将赌博机算法应用于这个问题，算法使用ε-贪婪动作选择，基于采样平均的动作价值估计，初始估计Q₁(*a*) = 0， $\forall a$ 。假设初始动作序列和回报是A₁ = 1, R₁ = -1, A₂ = 2, R₂ = 1, A₃ = 2, R₃ = -2, A₄ = 2, R₄ = 2, A₅ = 3, R₅ = 0。在某些时刻可能发生ε的情形，导致一个动作被随机选择。在哪个时刻这个情形肯定发生了？在哪个时刻这个情形可能发生了？**

通过表格计算$Q_t(a)$可确定贪心动作的范围:

   * 时刻 1:  0, 0, 0, 0, 0，贪心动作$\in\{1,2,3,4,5\}$，实际动作1，可能是随机
   * 时刻 2:  -1, 0, 0, 0, 0，贪心动作$\in\{2,3,4,5\}$，实际动作2，可能是随机
   * 时刻 3:  -1, 1, 0, 0, 0，贪心动作$\in\{2\}$，实际动作2，可能是随机
   * 时刻 4:  -1, -0.5, 0, 0, 0，贪心动作$\in\{3,4,5\}$，实际动作2，一定是随机
   * 时刻 5:  -1, 0.33, 0, 0, 0，贪心动作$\in\{2\}$，实际动作3，一定是随机

### Exercise 2.3:
**In the comparison shown in Figure 2.2, which method will perform best in the long run in terms of cumupative reward and probability of selecting the best acton? How much better will it be? Express your answer quantitatively.**

The method that will perform best in the long run is ε-greedy with ε = 0.01. Though it seems like the ε-greedy method with ε = 0.1 works better for 1000 steps, in the long run ε = 0.01 should outperform it. This is true because in the limit when steps tend to infinity, both methods will have the expected rewards converge to the true reward value. Since ε = 0.01 has a lower degree of randomness, it will capture a higher amount of reward. In either case any method will have an infinite reward, though the area under the curve will be bigger for ε = 0.01 if we were to select a given step much bigger than 1000 and evaluate the curve until that timestamp.

Quantitatively, we can estimate the reward obtained in each step by calculating the expected reward knowing q*(a) (the real value for each action). The expected reward value of a random guess is approximately 0, which means that a random guess' expected reward is 0. For ε = 0.1, there's a 90% chance of having a 1.5 reward value, and a .1% of having a random guess, which means a 0 reward. This results in an expected reward of 1.5 * .9 = 1.35.

We can estimate the reward for ε = 0.01 in a similar way. For ε = 0.01, there's a 99% chance of having a 1.5 reward value, and a .01% of having a random guess with 0 reward. This results in an expected reward of 1.5 * .99 = 1.485. Thus, ε-greedy with ε = 0.01 results in an expected reward value which is 0.135 units higher than ε-greedy with ε = 0.1.

### Exercise 2.4:
**If the step-size parameters, 𝛼<sub>n</sub>, are not constant, then the estimate Q<sub>n</sub> is a weighted average of previously received rewards with a weighting different from that given by (2.6). What is the weighting on each prior reward for the general case, analogous to (2.6), in terms of the sequence of step-size parameters?**

[Link to Solution PDF](./2.4.pdf)

<!-- [![alt text](./2.4.pdf  "Soliution to Problem 2.4")] (./2.4.pdf) -->

### Exercise 2.6: *Mysterious Spikes*
**The results shown in Figure 2.3 should be quite reliable because they are averages over 2000 individual, randomly chosen 10-armed bandits tasks. Why, then, are there oscillations and spikes in the early part of the curve for the optimistic method? In other words, what might make this method perform particularly better or worse, on average, on particular early steps?**

The oscillations in the early part of the optimistic method's curve seem to occur when the estimated values are still optimistic. When the curve increases, it is due to choosing the best bandit (the bandit with the highest expected reward); nevertheless, estimated values are still optimistic (much higher than their expected values). In this context, the best bandit is selected due to its optimistic value at some point during the early part of the curve, but when its estimated value becomes much closer to the real expected value, other decisions with optimistic values are chosen. This makes the curve oscillate during the early stages, until all estimated values aren't as nearly as optimal and becom much closer to the real expected value instead.

This means that for a short number of steps it isn't better to use an optimistic greedy methodology rather than a realistic e-greedy. Additionally, this trick is useful to encourage exploration only during the beginning of execution, and would just be useful for stationary problems.


### Exercise 2.7:
**Show that in the case of two actions, the soft-max distribution is the same as that given by the logistic, or sigmoid, function often used in statistics and artificial neural networks.**


[Link to Solution PDF](./2.7.pdf)

<!-- [![alt text](./2.7.pdf  "Soliution to Problem 2.4")] (./2.7.pdf) -->

