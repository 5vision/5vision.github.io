---
layout: post
title:  "Deep Attention Recurrent Q-Network"
date:   2016-07-11 11:00:06 +0300
categories:

info: Description of our paper at the first-ever Deep Reinforcement Learning Workshop at NIPS 2015 in Montréal, Canada.
---
In December 2015 our [paper][darqn] in which we proposed a way of equipping Google DeepMind's Deep Q-Network ([DQN][dqn]) with “soft” and “hard” attention mechanisms was [presented][deeprlworkshop] at Deep Reinforcement Learning Workshop conducted for the first time within NIPS Conference.

<table>
<tr>
<td rowspan="2">
{% include picture.html name="DSC_0104" alt="Spotlight talk" group="1" %}
</td>
<td>
{% include picture.html name="IMG_3273" alt="Poster presentation" group="1" %}
</td>
</tr>
<tr>
<td>
{% include picture.html name="IMG_3264" alt="We were lucky to communicate with Volodymyr Mnih (on the right)" group="1" %}
</td>
</tr>
</table>

<br />

There are several types of attention mechanisms ([Cho et al., 2015][cho]). In our work, we use so-called content-based attention that envisages computing the relevance of each spatially, temporally or spatio-temporally localized region of the input. In particular, we stick to the approach suggested by [Xu et al. (2015)][xu] for the domain of image caption generation.

![The Deep Attention Recurrent Q-Network](/assets/DARQN.png){:class="center-image" group="1"}

Architecture of the suggested Deep Attention Recurrent Q-Network (DARQN) consists of three main components depicted in the Figure above: convolutional network (CNN), attention network $$g$$, and recurrent network (in this case LSTM). CNN processes input image, producing location vectors $$v^{i}_t$$ (see Figure below), each of which is associated with a specific area of the input image.

![The convolutional network architecture in DARQN](/assets/DARQN_CNN.png){:.center-image}

Attention network takes ($$v^{i}_t$$, $$h_t$$) and determines relative importance of each corresponding area for the decision making process at the current moment of time. The resulting importance weights $$g^{i}_t$$ are used to calculate a context vector $$z_t$$ that is fed to the LSTM network. There are (at least) two ways how $$z_t$$ may be computed. In “soft” attention mechanism, $$z_t$$ is defined as a product of averaging all location vectors with $$g^{i}_t$$. In “hard” attention mechanism, $$z_t$$ is  equal to one of the $$v^{i}_t$$ with a probability defined by some $$g^{i}_t$$-parametrized probability distribution (e.g. categorical distribution).
To visualize attention regions, we create 256 subsidiary features maps 7 × 7 filled by measured importance of each location vector $$v^{i}_t$$ and then upsample these maps through CNN layers (see Picture below, “soft” attention at the top and “hard” version at the bottom, the corresponding game videos are available at our youtube [channel][darqn-youtube]).

![Visualization of attention regions](/assets/attention.png){:.center-image}

Tests of the proposed DARQN model on some Atari 2600 games demonstrate level of performance superior to that of DQN. In the table below, the best among 100 epochs average rewards per episode for four different models on five Atari games are presented. One epoch corresponds to 50,000 steps. The hard and soft attention models as well as [DRQN][drqn] are trained with 4 unroll steps. DRQN weights are updated at each step, whereas DQN and DARQN weights are updated one time per 4 steps.

|            | Breakout | Seaquest | S. Invaders | Tutankham | Gopher 
-------------|---------:|---------:|------------:|----------:|--------:
| DQN        | 241      |    1,284 |         916 |       197 |  1,976
| DRQN       | 72       |    1,421 |         571 |       181 |  3,512
| DARQN hard | 20       |    3,005 |         558 |       128 |  2,510
| DARQN soft | 11       |    7,263 |         650 |       197 |  5,356
{: .table-th-border }

<br/>

Our realization of DARQN is based on the [source code][dqn] and is available [online][darqn-github]. 


[deeprlworkshop]: http://rll.berkeley.edu/deeprlworkshop/

[cho]: http://arxiv.org/pdf/1507.01053.pdf

[xu]: http://arxiv.org/abs/1502.03044

[dqn]: https://sites.google.com/a/deepmind.com/dqn

[drqn]: http://arxiv.org/abs/1507.06527

[darqn]: https://arxiv.org/abs/1512.01693

[darqn-github]: https://github.com/5vision/DARQN

[darqn-youtube]: https://www.youtube.com/playlist?list=PLKK-nv55ZMg583wK4Ny5sZu9YoFo27NBi