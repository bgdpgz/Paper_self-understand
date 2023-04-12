# Continuous control with deep reinforcement learning

![](C:\Users\我的电脑\AppData\Roaming\Typora\typora-user-images\image-20230412211938984.png)

#### 模型如上图所示。

DDPG共有四个全连接网络，即Actor Net, Critic Net, Actor Target Net, Critic Target Net。

#### Actor Net:

通过输入当前状态值s，进入网络后得到行为a。

#### Critic Net:

通过输入当前状态值s和行为a，进入网络后得到对应的分数（可以将该分数认为是从当前时间当一个特定时间的奖励的和）。

#### Actor Targe Net 和 Critic Target Net 同上。

### 计算过程

从状态池中取出一些状态{s,ai,r,s'}（注意，这里的ai是实际的动作，不是通过Actor得到的）。首先根据当前状态s利用Actor计算出a，然后利用s和a通过Critic网络计算出当前动作的分数Q，得到一个loss，即 Loss=-Critic[s,a],然后利用s和ai通过Critic网络计算出当前分数Q(ai)，并利用Actor Target网络计算出下一步s'的动作a’，并利用Critic Target网络计算出下一步的分数Q(a')，最后r、Q(ai)和Q(a')形成第二个loss，即$ Loss=-(r+Q(a')-Q(ai)) $
 
大致过程如上述所示，具体步骤见
https://github.com/ghliu/pytorch-ddpg
