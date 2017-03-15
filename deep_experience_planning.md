# Deep Experience Planning: Leveraging Local Planning with Learned Value Functions

Alexander Neitz, Kyrill Schmid, Lisbeth Claessens, Lenz Belzner

## Introduction

We investigate the combination of statistical online planning based on local search and value function approximations learned from past observations. Many current state-of-the-art statistical online planners perform some kind of finite-horizon search. In many application domains, the search horizon is far smaller than episode length or system lifetime. This raises the question of how to evaluate of final search states, i.e. states reached by a particular search run when the finite horizon is met. Deep Experience Planning (DEEP) aims at leveraging statistical online planning with the use of value function approximations learned from previously observed system transitions.

## Related Work

A non-exhaustive list of potentially related work.

- Syam, Rafiuddin, Keigo Watanabe, and Kiyotaka Izumi. "An adaptive actor-critic algorithm with multi-step simulated experiences for controlling nonholonomic mobile robots." Soft Computing 11.1 (2007): 81-89. [[PDF](http://repository.unhas.ac.id/bitstream/handle/123456789/2640/fulltext.pdf?sequence=1)]
- Mahmood, Ashique Rupam, Huizhen Yu, and Richard S. Sutton. "Multi-step Off-policy Learning Without Importance Sampling Ratios." arXiv preprint arXiv:1702.03006 (2017). [[PDF](https://arxiv.org/pdf/1702.03006.pdf)]
- Kristopher De Asis, J. Fernando Hernandez-Garcia, G. Zacharias Holland, and Richard S. Sutton. "Multi-step Reinforcement Learning: A Unifying Algorithm" arXiv preprint arXiv:1703.01327 (2017).
  [[PDF](https://arxiv.org/pdf/1703.01327.pdf)]
- Li, Yuxi. "Deep Reinforcement Learning: An Overview." arXiv preprint arXiv:1701.07274 (2017). [[PDF](https://arxiv.org/pdf/1701.07274.pdf)]
- Weinstein, Ari, and Michael L. Littman. "Open-Loop Planning in Large-Scale Stochastic Domains." AAAI. 2013. [[PDF](http://ai2-s2-pdfs.s3.amazonaws.com/14d2/f4b8bb7c2ecb14c0072d9e25ba4c9ee59b68.pdf)]

## Deep Experience Planning

The key idea of DEEP is to learn a value function approximation from observed transitions, and to use the learned approximation as a heuristic for evaluating state reached at the search horizon of a statistical online planner. In some sense, the search strategy used for sampling the domain model can be seen as an actor, while the learned value function acts as a critic. Our hypothesis is that using a value function approximation this way improves overall performance of a statistical online planner.

### Local Planning

A DEEP agent maintains a simulation of the environment in order to sample potential consequences of its action choices. Based on these simulations, the DEEP agent is able to evaluate the quality of its behavioral options, and can act w.r.t. some given optimization objective (e.g. maximization of expected reward). Passing a current state and an action to the simulation allows to sample a potential successor state and an observed reward. Given a state space $$S$$, an action space $$A$$, and a reward domain $$R$$, a simulation $$\Delta$$ has the following form.

$$\Delta : P( S \times R \vert S \times A )$$

Current statistical simulation-based planners perform simulation up to some horizon $$h$$. For such a simulation, the planning agent observes a sequence of states, actions and rewards like the following:

$$s_0, a_0, r_0, s_1, r_1, a_1, ..., s_{h-1}, a_{h-1}, r_{h-1}, s_h$$

Based on these observations, a possible optimization criterion is the cumulative reward, i.e. the sum of rewards gathered from executing the corresponding plan $$p  = a_0, a_1, ..., a_{h-1}​$$, i.e. the sequence of actions. A planning agent estimates the quality $$Q​$$ of a plan by using the cumulative reward.

$$Q(p) = \sum_{0 \leq i \leq h} r_i$$

### Local Planning with a Value Function

While the basic local planning approach as described above can be very effective, DARTS enhances the estimation of action evaluation by employing a value function in order to estimate the expected value of the final simulation state $$s_h$$. For a given MDP $$(S, A, T, R)$$ with state-action transition distribution $$T  : P(S \vert S \times A)$$ and reward function $$R : S \times A \times S \rightarrow \mathbb{R}$$, the value function is recursively defined as follows.

$$V(s) = \max_a \left( \sum_{s'} T(s' \vert s, a) \cdot \left( R(s, a, s') + \gamma V(s') \right) \right)$$

That is, the value function of a state is defined by the best action the is executable in this state, where 'best' is determined w.r.t. potential future reward.

In the case of a DEEP planner, the transition function $$T$$ and the reward function $$R$$ of the MDP may only be available implicitly via the simulation $$\Delta$$. In this case, the value function can be defined via the expectation of future reward.

$$V(s) = \max_a \left( \mathbb{E}_{s, r \sim \Delta(s, a)} \left[  r + \gamma V(s') \right] \right)$$

Given a value function, a DEEP agent alters the estimation of action sequence quality by adding the value of the final state. In some sense, the DEEP agent enhances its local planning with global information obtained via the value function.

$$Q_{DEEP}(p) = \sum_{0 \leq i \leq h} r_i + V(s_h)$$

### Learning a Value Function Approximation from Experience

In order to leverage its planning capabilities, a DEEP agent uses a value function for improving its action quality estimates. We now discuss how an approximation of the value function can be learned from observed transitions by using a temporal difference update rule for measuring the approximation error. When modeling the value function approximation with a neural network, we can use stochastic gradient descent to reduce the temporal difference error. Let $$V'$$ be the current value function approximation of the agent. For given observed transitions $$(s, a, s', r)$$, we can now define the following tuple as a regression target:

$$(s, r + \gamma V'(s'))$$

That is, given some input state $$s$$, we want the value function approximation network to output $$r + \gamma V'(s')$$ as a rough approximation of the real value of $$s$$. Given enough observed transitions and training iterations, the network modeling $$V'$$ starts approximating $$V$$.

### Using a Target Network to Stabilize Training

As $$V'$$ is a changing target, in particular in the beginning of the learning process, we use a more stable target network $$V''$$ for mitigating stability issues when training $$V'$$. Then, we train $$V'$$ on tuples of the following form.

$$(s, r + \gamma V''(s'))$$

The target network $$V''$$ is replaced with the current $$V'$$ after a fixed number of training iterations. By using the less volatile target network $$V''$$ for estimating state values yields a stabilization of the training process.

## Experimental Results

TODO

## Conclusion and Outlook

TODO:
- Impact of search depth?
- Potential application for accelerating RL?