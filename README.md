# scalable-computing
review and make some note about scalable computing
![gpu](https://s6.jpg.cm/2022/10/29/PtKduC.png)

GPU and CPU
-----------------
1）Talking about clocks, chord sizes and buses and Oberleutnant leading into the VF carbon power. And power.   
2）what happens with the clocks and cores decides the bosses you know, is fairly self evident:If you run at a higher clock speed, you will generally manage to perform more computations more operations per cycle if you have more cores running in parallel, that gives you more available compute resource.   
3)And driving up the clock speed leads you towards this VF curve, this voltage frequency relationship which we'll come to in a second in general if you drive up the operation frequency, you're going to consume more power you're doing more operations per cycle.  
__In general, if you speed up the overall soc. So you bring the voltage up, you have more power available.__

1)Obviously, with multiple cores, you can do multiple things in parallel.  
2)四个内核为例，那么二加一的第二次计算可能会发生，直到一加一发生之后。我没有办法并行化它，除非我做各种类型的预测性工作，并猜测程序接下来会要求什么，这是编译器做的事情，这是CPU做缓存的事情，特别是倾向于这样做。    
__cache__:  
So a cache is essentially a particular type of memories, particular area of memory, that has dedicated processes associated with it.And its purpose is to try to predict the data you're going to need.  
3)cache和cpu的关系：Like it is one of its purposes now. It's only when it its purpose is to try to predict the data or the information or the instructions you're going to need next that will introduce you're going to need to enable the instructions that the CPU is mostly to run next.  
4）example：Because what's happened is, you know, you have the two primary CPU, the primary core, and it's going to do one plus one. And the normal thing it does is it takes that result to add adds to the next one. So that second, the third number one, so one plus one first two ones, the third one is sitting in memory and storage waiting to be used.   
如果预测错了怎么办：But essentially we're doing is in that situation, the cache is making a prediction is having a guess, if it gets it wrong, has consumed some power. There's no harm done nothing has been lost. It's just made a bad. And the overall operation slows down slightly.
5）Caching and good cache prediction is an important thing for our CICS in particular.  
__CICS__：CICS是IBM公司的强大主机交易服务器、整合平台，在全球C、C++、COBOL等交易中间件市场上占有绝大多数客户  

__cache hit rate__  
1）the cache hit rate as it's known is much, much higher
2）对于像缓存这样的东西如何应用于例如Netflix，例如亚马逊Prime，在将内容发送到您的电视，将手机发送到您的移动设备方面，您的想法是什么？你怎么看，或者你认为那里可能存在相似之处？有哪些相似之处和概念？任何人都可以跳进去吗？  Yeah, so I mean, people are talking about offloading content onto the edge nodes and edge cache. So CD ends.So essentially, what's happening here is and there's, it's what's known as a type of prefix Caching.-----__prefix Caching__

__cdn__:  
So what essentially happens with with some of the content distribution networks, so when people provide streaming audio, like private Netflix, is they have edge caches, they have content caches, as part of the CDN content distribution networks, they have nodes, and the purpose or the goal of the node is essentially to pull down and store content close to the person requesting it.  

__Netflix__:












