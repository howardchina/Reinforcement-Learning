# Chapter 2 Exercises
### Exercise 2.1
**如果是*ε-贪婪*动作选择，对于两个动作且ε = 0.5的情况，贪婪动作被选择的概率是？**

概率是75%，由两部分构成：
- 50%概率源自选择贪婪动作，即1-ε = 1-0.5 = 0.5
- 25%概率源自随机动作，即ε*(1/2) = 0.25


### Exercise 2.2: *赌博机的例子*
**考虑一个*k*=4的多臂赌博机问题，几座1、2、3、4。将赌博机算法应用于这个问题，算法使用ε-贪婪动作选择，基于采样平均的动作价值估计，初始估计Q₁(*a*) = 0，<!-- $\forall a$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cforall%20a">。假设初始动作序列和回报是A₁ = 1, R₁ = -1, A₂ = 2, R₂ = 1, A₃ = 2, R₃ = -2, A₄ = 2, R₄ = 2, A₅ = 3, R₅ = 0。在某些时刻可能发生ε的情形，导致一个动作被随机选择。在哪个时刻这个情形肯定发生了？在哪个时刻这个情形可能发生了？**

通过表格计算$Q_t(a)$可确定贪心动作的范围:

   * 时刻 1:  0, 0, 0, 0, 0，贪心动作<!-- $\in\{1,2,3,4,5\}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cin%5C%7B1%2C2%2C3%2C4%2C5%5C%7D">，实际动作1，可能是随机
   * 时刻 2:  -1, 0, 0, 0, 0，贪心动作<!-- $\in\{2,3,4,5\}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cin%5C%7B2%2C3%2C4%2C5%5C%7D">，实际动作2，可能是随机
   * 时刻 3:  -1, 1, 0, 0, 0，贪心动作<!-- $\in\{2\}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cin%5C%7B2%5C%7D">，实际动作2，可能是随机
   * 时刻 4:  -1, -0.5, 0, 0, 0，贪心动作<!-- $\in\{3,4,5\}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cin%5C%7B3%2C4%2C5%5C%7D">，实际动作2，一定是随机
   * 时刻 5:  -1, 0.33, 0, 0, 0，贪心动作<!-- $\in\{2\}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cin%5C%7B2%5C%7D">，实际动作3，一定是随机

### Exercise 2.3:
**在图2.2的对比中, 从累计收益和选择最佳动作的概率大角度考虑，哪一个方法会在长期表现最好？好多少？定量地表述你的答案。**

表现最好的方法会是ε=0.01的ε-贪心方法。虽然ε=0.1的ε-贪心方法在1000步表现更好，但是长期来看ε=0.01的ε-贪心方法会更好。因为步数趋于无穷时，两个方法的期望收益都会收敛到真实收益。由于ε=0.01的随机性比ε=0.1更小，ε=0.01具有更高的收益。

定量地说，我们可以估计期望收益，也就是<!-- $\mathbb{E}^{\epsilon}[R_t]=(1-\epsilon)\max_a Q_t(a) + \epsilon \sum_{i=1}^{10} Q_t(i)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cmathbb%7BE%7D%5E%7B%5Cepsilon%7D%5BR_t%5D%3D(1-%5Cepsilon)%5Cmax_a%20Q_t(a)%20%2B%20%5Cepsilon%20%5Csum_%7Bi%3D1%7D%5E%7B10%7D%20Q_t(i)">。将<!-- $Q_{t}(a)=q_*(a)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=Q_%7Bt%7D(a)%3Dq_*(a)">代入得<!-- $\mathbb{E}^{\epsilon}[R_t]=(1-\epsilon)\max_a q_*(a) + \epsilon \sum_{i=1}^{10} q_*(i)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cmathbb%7BE%7D%5E%7B%5Cepsilon%7D%5BR_t%5D%3D(1-%5Cepsilon)%5Cmax_a%20q_*(a)%20%2B%20%5Cepsilon%20%5Csum_%7Bi%3D1%7D%5E%7B10%7D%20q_*(i)">。实际价值<!-- $q_*(a)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=q_*(a)">是采样自一个均值为0方差为1的标准正态分布，所以将<!-- $\sum_{i=1}^{10} q_*(i)=0$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Csum_%7Bi%3D1%7D%5E%7B10%7D%20q_*(i)%3D0">带入得<!-- $\mathbb{E}^{\epsilon}[R_t]=(1-\epsilon)\max_a q_*(a)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cmathbb%7BE%7D%5E%7B%5Cepsilon%7D%5BR_t%5D%3D(1-%5Cepsilon)%5Cmax_a%20q_*(a)">。所以ε=0.01比ε=0.1期望收益高，前者是后者的(1-0.01)/(1-0.1)=1.1倍。

### Exercise 2.4:
**如果步长参数$\alpha_n$不是常数，那么估计$Q_n$就是一个前面接受的收益的加权平均，其权值与公式(2.6)给出的不同。对于这个步长参数，类似于公式(2.6)，每个先前收益的权重的通用表达式是什么？

<!-- $\begin{align*}
Q_{n+1}&=Q_n + \alpha_n(R_n-Q_n) \\
&=\alpha_n R_n + (1-\alpha_n)Q_n \\
&=\alpha_n R_n + (1-\alpha_n) (\alpha_{n-1} R_{n-1} + (1-\alpha_{n-1})Q_{n-1}) \\
&=\alpha_n R_n + (1-\alpha_n) \alpha_{n-1} R_{n-1} + (1-\alpha_n)(1-\alpha_{n-1})Q_{n-1} \\
&=\alpha_n R_n + (1-\alpha_n) \alpha_{n-1} R_{n-1} + (1-\alpha_n)(1-\alpha_{n-1})(\alpha_{n-2} R_{n-2} + (1-\alpha_{n-2})Q_{n-2}) \\
&=\alpha_n R_n + (1-\alpha_n) \alpha_{n-1} R_{n-1} + (1-\alpha_n)(1-\alpha_{n-1})\alpha_{n-2} R_{n-2} + (1-\alpha_n)(1-\alpha_{n-1})(1-\alpha_{n-2})Q_{n-2} \\
&=(\prod_{i=1}^n{1-\alpha_i})Q_1 + \sum_{i=1}^{n} (\alpha_i \prod_{j=i+1}^n{1-\alpha_j})R_{i}
\end{align*}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cbegin%7Balign*%7D%0AQ_%7Bn%2B1%7D%26%3DQ_n%20%2B%20%5Calpha_n(R_n-Q_n)%20%5C%5C%0A%26%3D%5Calpha_n%20R_n%20%2B%20(1-%5Calpha_n)Q_n%20%5C%5C%0A%26%3D%5Calpha_n%20R_n%20%2B%20(1-%5Calpha_n)%20(%5Calpha_%7Bn-1%7D%20R_%7Bn-1%7D%20%2B%20(1-%5Calpha_%7Bn-1%7D)Q_%7Bn-1%7D)%20%5C%5C%0A%26%3D%5Calpha_n%20R_n%20%2B%20(1-%5Calpha_n)%20%5Calpha_%7Bn-1%7D%20R_%7Bn-1%7D%20%2B%20(1-%5Calpha_n)(1-%5Calpha_%7Bn-1%7D)Q_%7Bn-1%7D%20%5C%5C%0A%26%3D%5Calpha_n%20R_n%20%2B%20(1-%5Calpha_n)%20%5Calpha_%7Bn-1%7D%20R_%7Bn-1%7D%20%2B%20(1-%5Calpha_n)(1-%5Calpha_%7Bn-1%7D)(%5Calpha_%7Bn-2%7D%20R_%7Bn-2%7D%20%2B%20(1-%5Calpha_%7Bn-2%7D)Q_%7Bn-2%7D)%20%5C%5C%0A%26%3D%5Calpha_n%20R_n%20%2B%20(1-%5Calpha_n)%20%5Calpha_%7Bn-1%7D%20R_%7Bn-1%7D%20%2B%20(1-%5Calpha_n)(1-%5Calpha_%7Bn-1%7D)%5Calpha_%7Bn-2%7D%20R_%7Bn-2%7D%20%2B%20(1-%5Calpha_n)(1-%5Calpha_%7Bn-1%7D)(1-%5Calpha_%7Bn-2%7D)Q_%7Bn-2%7D%20%5C%5C%0A%26%3D(%5Cprod_%7Bi%3D1%7D%5En%7B1-%5Calpha_i%7D)Q_1%20%2B%20%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%20(%5Calpha_i%20%5Cprod_%7Bj%3Di%2B1%7D%5En%7B1-%5Calpha_j%7D)R_%7Bi%7D%0A%5Cend%7Balign*%7D">
题目答案是<!-- $R_i$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=R_i">的权重<!-- $\alpha_i \prod_{j=i+1}^n{1-\alpha_j}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Calpha_i%20%5Cprod_%7Bj%3Di%2B1%7D%5En%7B1-%5Calpha_j%7D">。

### Exercise 2.5：设计并且实施一项实验来证实采用采样平均方法去解决非平稳问题的困难。使用一个10臂测试平台的修改版本，其中所有的<!-- $q_*(a)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=q_*(a)">初始时相等，然后进行随机游走（比如说每一步所有的<!-- $q_*(a)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=q_*(a)">都加上一个均值为0标准差为0.01的正态分布的增量）。为其中一个使用采样平均和增量式计算的动作-价值方法，为另一个使用常数步长参数且<!-- $\alpha=0.1$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Calpha%3D0.1">的动作-价值方法，并做出如图2.2所示的分析。采用<!-- $\epsilon=0.1$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cepsilon%3D0.1">，并且取很长的时间（比如10 000步）。


[答案 见ex2.5.ipynb](./ex2.5.ipnb)

<img src="./ex2.5_output.png">


### Exercise 2.6: *Mysterious Spikes*
**The results shown in Figure 2.3 should be quite reliable because they are averages over 2000 individual, randomly chosen 10-armed bandits tasks. Why, then, are there oscillations and spikes in the early part of the curve for the optimistic method? In other words, what might make this method perform particularly better or worse, on average, on particular early steps?**

The oscillations in the early part of the optimistic method's curve seem to occur when the estimated values are still optimistic. When the curve increases, it is due to choosing the best bandit (the bandit with the highest expected reward); nevertheless, estimated values are still optimistic (much higher than their expected values). In this context, the best bandit is selected due to its optimistic value at some point during the early part of the curve, but when its estimated value becomes much closer to the real expected value, other decisions with optimistic values are chosen. This makes the curve oscillate during the early stages, until all estimated values aren't as nearly as optimal and becom much closer to the real expected value instead.

This means that for a short number of steps it isn't better to use an optimistic greedy methodology rather than a realistic e-greedy. Additionally, this trick is useful to encourage exploration only during the beginning of execution, and would just be useful for stationary problems.


### Exercise 2.7:
**Show that in the case of two actions, the soft-max distribution is the same as that given by the logistic, or sigmoid, function often used in statistics and artificial neural networks.**


[Link to Solution PDF](./2.7.pdf)

<!-- [![alt text](./2.7.pdf  "Soliution to Problem 2.4")] (./2.7.pdf) -->

