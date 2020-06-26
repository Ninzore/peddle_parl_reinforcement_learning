# peddle_parl_reinforcement_learning
Turotials and examples for Baidu Paddle and Parl  
百度AI Studio 深度强化学习Tutorial

### 先说结论
#### 方便！！！
百度这个Parl强化学习框架真的是异常简单，  
已经把常用的算法都封装好了开箱即插即用，只要前期稍微有深度/强化学习基础应该都可以立刻上手  
对比Tensorflow入门简直天差地别，初学者用这个应该会感觉很舒适，或者快速开发小型demo  
如果能把入门教程做好应该是唯一指定强化学习入门库  


### 缺点：  
现在有个很大的问题就是社区环境不如TF和Torch，开发者和相关文章都太少了，短期应该不太能解决  
因为是基于PaddlePaddle做的，所以总是会有一些小毛病，报错信息给的太少了有时候无法定位出错点到底是哪里  
环境配置不太友好，因为Paddle迭代很快有时候会出现两个版本不兼容的问题，还有就是有的CUDA版本不兼容？！  
这些不友好的地方能改善能加分  

### 封装过好也有问题  
由于很多算法已经封装到了Parl，而且封的很死，巴不得你全部都import parl  
虽说对于入门很方便但是如果想要细调一些东西例如optimizer或者adaptive learning rate都是不许的  
这点就让人烦躁，最后还是得重写一次算法以达成自己想要的效果，说真的留个口子让人可以指定有这么难？  
（吐槽：Parl源码大量使用Adam optimizer，几乎全是，砍得出来他们真的很爱这个）  
