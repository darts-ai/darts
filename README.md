# Distributed Autonomous Real-Time Systems

The DARTS group is studying a variety of problems and research questions in the field of distributed autonomous real-time systems. Here, we want to give an overview of ongoing research in our group. Don't hesitate to follow the provided links for more information. In case you want to get in touch for any research-related reason, feel free to contact us.

<p align="center">
  <img src='img/adamOil.jpg' width='25%' />
</p>

## DEPLER - Hybrid Statistical Control

DEPLER is a project that aims to study challenges and prospects of combining statistical online planning and deep learning of global models in single and multi-agent systems, both in discrete and continuous state and time domains. See the [DEPLER project page](depler.md) for more information.

Currently, we are studying the combination of statistical online planning with global value functions (or distributions) learned from prior experience in order to improve planning effectiveness. The idea is to combine the effectiveness and precise value estimations obtained by bounded statistical local planning with learned [value functions](https://en.wikipedia.org/wiki/Bellman_equation) capturing the general value distribution in the state space. While classical statistical planners use a heuristic value when they reach their simulation horizon, we instead estimate the value of the final state of a search trace with an estimated value learned from former experience of the agent. To enable generalization, we use a deep learning approach for modeling and training the value function estimate.

## Local Interaction and Emergence

Another direction of current research is the enhancement of multi-agent systems based on local planning with global learning. In this setting, system behavior is an emergent result from many local interation of individually planning and coordinating agents. See [our paper](https://arxiv.org/pdf/1702.07544.pdf) for a framework realizing this idea with statistical online planning in a distributed way. We also provide accompanying [code on github](https://github.com/lenzbelzner/doolp). One idea to expand on this framework is to exploit globally learning statistical relations of local states and interaction patterns and global effects relevant for quality of the system's overall behavior. The learned global relation in turn be used to enhance the local agents' activities, influencing emergent global system behavior and further global learning.

## Statistical Verification and Quality Assessment

We also study verification and quality assessment of systems that build their behavior with statistical online planning. Here, the task is to effectively and efficiently determine useful statistical bounds on plan values or requirement satisfaction/violation probabilities. The problem is that any estimates established in the course of planning are usually pretty loose, as the observed value distribution typically is not i.i.d., because the sampling distribution changes based on previously simulated plan samples.

Therefore, effective algorithms for establishing valid estimates before committing to an action are a subject of our research. Algorithms that efficiently generate plans that are likely to satisfy given requirements could also be useful in this context. See [our paper](https://arxiv.org/pdf/1702.08726.pdf) on the subject, with [code on github](https://github.com/lenzbelzner/stb). Another difficulty that agents have to treat in this setting is uncertainty about models that are learned from limited data, being particularly important in the verification setting. For more details, see our [paper on arXiv](https://arxiv.org/pdf/1702.08725.pdf), and grab the accompanying [code on github](https://github.com/lenzbelzner/bv).

## Risk and QoS-Awareness

Another topic is the study of the effects of modeling or learning a value distribution rather than a value function, and using this distribution in different ways to achieve particular agent behavior. For example, we studied the effect of using [expected shortfall](https://en.wikipedia.org/wiki/Expected_shortfall) (or conditional value-at-risk) as optimization objective (rather than expectation) in order to achieve risk-aware agent policies. See [Kyrill's thesis](http://public.mobile.ifi.lmu.de/public/theses/ba-thesis-kyrill-schmid.pdf) for more details on risk-aware online planning. We also investigate the effect of QoS-based optimization, where the goal is to find a policy that satisfies a certain required level of quality, rather than requiring an agent to always search for an optimal policy. Intuitively, we allow agents to build sufficient policies w.r.t. requirements. See [our paper](http://public.mobile.ifi.lmu.de/public/papers/qats_draft.pdf) for more details on QoS-aware decision making.

## Temporal Abstraction and Uncertainty

A key challenge in current research on model-based control is scalability of methods for learning predictive models from data. In particular, the following properties of learned models could be useful for effective control:

1. Learned predictive models should be able to predict domains dynamics and interaction consequences at different time scales. This yields the challenge to capture, augment and prepare training data and model architectures so that they are able to work at different temporal scales. Also, automatic inference of informative and relevant time scales from data w.r.t. a given task distribution is an interesting venue and subject of our current research. Another motivation for temporal abstraction in predictive models is the effectiveness of online planning with action durations. In [our research](http://public.mobile.ifi.lmu.de/public/papers/tace_draft.pdf), we showed that statistical online planning with optimization of action durations can result in better sample efficiency, requiring less resources for simulation and increasing overall control quality. For this approach to work, predictive models that can efficiently be queried at different time scales are a key premise.
2. Learned predictive models should be able to quantify predictive uncertainty, and to distinguish between aleatoric uncertainty due to perceptual spatial and temporal abstraction, and epistemic uncertainty arising from limited data and resources used for learning. This uncertainty information is crucial for systems that are required to make informed decisions w.r.t. specified requirements and goals.

We think that combining ideas from temporal abstraction (e.g. 1D convolutions, recurrent and/or hierarchical architectures), [intuitive physics](http://phys.csail.mit.edu/) and [uncertainty calibration](http://bayesiandeeplearning.org/) provides an interesting ground for useful and fascinating research.

## Diverse Optimization

Typically, a control algorithm has a particular optimization objective. For example, such an objective could be to maximize the expected sum of observed rewards, or to minimize the probability of violating a given requirement. Usually, optimization is focused on a single extremum of a function (e.g. a value function). However, in many application scenarios the target optimization function can change in the course of decision making and planning due to unexpected but observable events. In our group, we study the effect of diversity in optimization on the robustness and effectiveness of statistical planning algorithms.

## General Video Game Playing

One application area and an interesting testbed for DARTS is general video game playing. The GVGAI competition provides an accessible, challenging and competitive environment for trying out ideas for single- and multi-agent statistical planning. Also, the GVGAI competition poses a major challenge to efficiency of online decision making: An agent has to decide on an action in a fraction of a second. There is also an interesting level generation challenge. By the way: Flo achieved state-of-the-art results in the two player GVGAI competition. Watch out for Number 27 in [the GVGAI scoreboards](http://gvgai.net/gvg_rankings_conf_2p.php?rg=2004).

## Evolutionary Computation and Neuroevolution

We are also interested in applications of evolutionary computation. Flo's GVGAI player Number 27 is based on genetic planning. Here, different plans are encoded as genomes, and evolutionary optimization is used to increase the reward of plans under consideration by the planning agent. We are also investigating a particular notion of genealogic diversity, with applications to robust online planning and test suite optimization. And Alex investigated [scalable](http://people.idsia.ch/~tino/papers/koutnik.gecco10.pdf) [neuroevolution](http://people.idsia.ch/~juergen/gomez08a.pdf) of penalty kick policies in [robocup 2D](https://en.wikipedia.org/wiki/RoboCup_2D_Soccer_Simulation_League).

## People

The DARTS group is located at LMU Munich. We are, not ordered in any particular way:

Lisbeth Claessens,
Alexander Neitz,
Alexander Isenko,
Tobias Duemmling,
Florian Kirchgeßner,
Patrick Haller von Hallerstein,
Thomy Phan,
[Kyrill Schmid](http://www.mobile.ifi.lmu.de/team/kyrill-schmid/),
[Thomas Gabor](http://www.mobile.ifi.lmu.de/team/thomas-gabor/),
[Lenz Belzner](http://www.mobile.ifi.lmu.de/team/lenz-belzner/)

## Publications

1. Belzner, Lenz, and Thomas Gabor. "Scalable Multiagent Coordination with Distributed Online Open Loop Planning." arXiv preprint arXiv:1702.07544 (2017).
1. Belzner, Lenz, and Thomas Gabor. "Stacked Thompson Bandits." arXiv preprint arXiv:1702.08726 (2017).
1. Belzner, Lenz, and Thomas Gabor. "Bayesian Verification under Model Uncertainty." arXiv preprint arXiv:1702.08725 (2017).
1. Belzner, Lenz. "Simulation-Based Autonomous Systems in Discrete and Continuous Domains." PhD Thesis, LMU Munich, 2016.
1. Gabor, Thomas, et al. "A Simulation-Based Architecture for Smart Cyber-Physical Systems." Autonomic Computing (ICAC), 2016 IEEE International Conference on. IEEE, 2016.
1. Belzner, Lenz. "Time-adaptive cross entropy planning." Proceedings of the 31st Annual ACM Symposium on Applied Computing. ACM, 2016.
1. Belzner, Lenz, and Thomas Gabor. "QoS-Aware Multi-armed Bandits." Foundations and Applications of Self* Systems, IEEE International Workshops on. IEEE, 2016.
1. Belzner, Lenz, et al. "Software engineering for distributed autonomous real-time systems." Proceedings of the 2nd International Workshop on Software Engineering for Smart Cyber-Physical Systems. ACM, 2016.
1. Belzner, Lenz, et al. "Collective Autonomic Systems: Towards Engineering Principles and their Foundations." Transactions on Foundations for Mastering Change I. Springer International Publishing, 2016. 180-200.
1. Belzner, Lenz, Rolf Hennicker, and Martin Wirsing. "OnPlan: A framework for simulation-based online planning." International Workshop on Formal Aspects of Component Software. Springer International Publishing, 2015.

## Theses

1. Alexander Neitz. Deep Q-Embedding for Transfer Reinforcement Learning. Master thesis, LMU Munich, 2017
1. Kyrill Schmid. Risk-Sensitive Online Planning. Bachelor thesis, LMU Munich, 2017
1. Tobias Duemmling. Temporal Abstractors. Bachelor thesis, LMU Munich, 2017
1. Alexander Isenko. Neuroevolution in RoboCup2D. Bachelor thesis, LMU Munich, 2017
1. Florian Kirchgeßner. Heuristic Online Planning with Genetic Algorithms. Bachelor thesis, LMU Munich, 2016
1. Patrick Haller von Hallerstein. Evolutionary Level Generation for General Video Game Playing. Bachelor thesis, LMU Munich, 2016