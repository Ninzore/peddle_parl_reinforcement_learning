# peddle_parl_reinforcement_learning
Turotials and examples for Baidu Paddle and Parl  
百度AI Studio 深度强化学习Tutorial

### 先说结论
#### 方便！！！
百度这个Parl强化学习框架真的是异常简单，  
已经把常用的算法都封装好了开箱即插即用，只要前期稍微有深度/强化学习基础应该都可以立刻上手  
对比Tensorflow入门简直天差地别，初学者用这个应该会感觉很舒适，或者快速开发小型demo  
现在有个很大的问题就是社区环境不如TF和Torch，开发者和相关文章都太少了，短期应该不太能解决  
如果能把入门教程和环境做好应该是唯一指定强化学习入门库  

### 缺点：  
因为是基于PaddlePaddle做的，所以总是会有一些小毛病，报错信息给的太少了有时候无法定位出错点到底是哪里  
环境配置不太友好，因为Paddle迭代很快有时候会出现两个版本不兼容的问题，还有就是有的CUDA版本不兼容？！  
这些不友好的地方能改善能加分  


### 关于Optimizer
看一下Parl的算法源码例如DDPG，可以发现Optimizer是这么写的  
```python
class DDPG(Algorithm):
    def __init__(self,
                 model,
                 gamma=None,
                 tau=None,
                 actor_lr=None,
                 critic_lr=None):
# ...
# ...
optimizer = fluid.optimizer.AdamOptimizer(self.actor_lr)
``` 
（Parl大量使用Adam optimizer，几乎全是，看得出来他们真的很爱这个） 
那么看起来除非自己写要不然是不让改的了，这里optimizer可以换成SGD或者Lookahead（Lookahead真的很香）  
paddle的[optimizer]挺全的(https://www.paddlepaddle.org.cn/documentation/api/en/0.15.0/optimizer.html)用就是了  

### 关于学习率
还是找DDPG做例子  
```python
class DDPG(Algorithm):
# ...
    assert isinstance(actor_lr, float)
    assert isinstance(critic_lr, float)
``` 
看来是必须得进float了，然而如果想要用可变学习率这地方必须得改，而且可变学习率在各个方面都是很有必要的，  
明明paddle的[学习率调度器](https://www.paddlepaddle.org.cn/documentation/api/en/0.15.0/layers.html#learning-rate-scheduler)都做好了为什么不直接塞进去呢？  
例如picewise_decay直接在optimizer那个地方后面改成  
```
optimizer = fluid.optimizer.AdamOptimizer(
  fluid.layers.piecewise_decay([10000, 20000],
  [2*self.actor_lr, self.actor_lr, 0.5*self.actor_lr]
  )
)
```

### 封装过好也有问题  
由于很多算法已经封装到了Parl，而且封的很死，巴不得你全部都import parl  
虽说对于入门很方便但是如果想要像上面一样细调一些东西例如optimizer或者adaptive learning rate都是不许的  
这点就让人烦躁，最后还是得重写一次算法以达成自己想要的效果，说真的留个口子让人可以指定有这么难？  
