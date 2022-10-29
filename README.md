# scalable-computing
review and make some note about scalable computing
![gpu](https://s6.jpg.cm/2022/10/29/PtKduC.png)

Performance/Threads：clocks,sizes,buses,cores
-----------------
1)Talking about clocks, chord sizes and buses and Memory Wall leading into the VF carbon power and power.   

2)what happens with the clocks and cores decides the bosse, is fairly self evident:If you run at a higher clock speed, you will generally manage to perform more computations more operations per cycle if you have more cores running in parallel, that gives you more available compute resource.  

3)And driving up the clock speed leads you towards this VF curve, this voltage frequency relationship which we'll come to in a second in general if you drive up the operation frequency, you're going to consume more power you're doing more operations per cycle.  

__In general, if you speed up the overall soc. So you bring the voltage up, you have more power available.__

1)Obviously, with multiple cores, you can do multiple things in parallel.  

2)四个内核为例:二加一的第二次计算可能会发生，直到一加一发生之后。我没有办法并行化它，除非我做各种类型的预测性工作，并猜测程序接下来会要求什么，这是编译器做的事情，这是CPU缓存做的事情。 


名词解释
-----------------
__cache__:  
1)So a cache is essentially a particular type of memories, particular area of memory, that has dedicated processes associated with it.And its purpose is to try to predict the data you're going to need.  
2)cache和cpu的关系：Like it is one of its purposes now. It's only when it its purpose is to try to predict the data or the information or the instructions you're going to need next that will introduce you're going to need to enable the instructions that the CPU is mostly to run next.  
3)example：Because what's happened is, you know, you have the two primary CPU, the primary core, and it's going to do one plus one. And the normal thing it does is it takes that result to add adds to the next one. So that second, the third number one, so one plus one first two ones, the third one is sitting in memory and storage waiting to be used. 
4)Caching and good cache prediction is an important thing for our CICS in particular.  
__CICS__：CICS是IBM公司的强大主机交易服务器、整合平台，在全球C、C++、COBOL等交易中间件市场上占有绝大多数客户    
如果预测错了怎么办：But essentially we're doing is in that situation, the cache is making a prediction is having a guess, if it gets it wrong, has consumed some power. There's no harm done nothing has been lost. It's just made a bad. And the overall operation slows down slightly.   

__cache hit rate__  
1）the cache hit rate as it's known is much, much higher

2）对于像缓存这样的东西如何应用于例如Netflix，例如亚马逊Prime，在将内容发送到您的电视，将手机发送到您的移动设备方面，您的想法是什么？你怎么看，或者你认为那里可能存在相似之处？有哪些相似之处和概念？任何人都可以跳进去吗？  Yeah, so I mean, people are talking about offloading content onto the edge nodes and edge cache. So CD ends.So essentially, what's happening here is and there's, it's what's known as a type of prefix Caching.-----__prefix Caching__

__cdn__:  
So what essentially happens with with some of the content distribution networks, so when people provide streaming audio, like private Netflix, is they have edge caches, they have content caches, as part of the CDN content distribution networks, they have nodes, and the purpose or the goal of the node is essentially to pull down and store content close to the person requesting it.    

__prefix Caching__：  
but essentially it's a type of prefix caching so you make your original connection your browser Netflix catalog for example.

__Netflix__:  
会员：因此，例如，您将原始连接设置为浏览器Netflix目录。而Netflix的做法略有不同。网飞不是一个很好的例子。但是，让我们以Netflix为例，因为它是一个常见的问题。让我们采取Prime，以便您浏览Netflix或Prime目录，选择一些您开始观看的东西，您开始观看的流的初始部分或多或少地来自一个更集中的服务器，本质上是一个直接连接到计费和内容管理系统的服务器，以建立例如许可证来做到这一点， 有时他们给你5或10分钟，你知道，30秒，60秒作为测试或收费之前等。因此，一般来说，您将提出请求，当您开始观看该内容时，您将被指向该内容的来源之一，因为您知道，要对它使用各种算法和方法，而不是观看它。网络想要做的一件事是将流量输送的负担从他们更集中的系统卸载，在那里他们进行计费和收费以及一些辅助系统，而辅助系统本质上是一种比你更靠近你的设备，在我们描述的某些方式中，它比中央系统更接近你。我们真的想将您与该电影流的实例联系起来，该实例在物理上或地理上更接近该实例，并且网络术语更接近于您作为中央网络资源的消耗要少得多。同样，使用缓存可以使用特定类型的前缀缓存。这里基本上是相同的原则。我们是移动所有接近的副本的人，或者我们希望将您连接到更接近的数据的副本，因为它可以更快地到达您那里。它使用较少的网络资源。它与您联系更紧密，如您所知，更低的延迟，更高的吞吐量等，中央副本是这样的，因此缓存的概念，您知道，这不是一个新的或令人兴奋的或原始的概念，您如何实现它因地而异，因为不同内容类型的不同性质，但是让东西离您更近并让它坐在那里等着您，因为我们认为您可能想要这是您将在任何高吞吐量或高输送系统上遇到的常规操作。原则上，系统在相同的基础上工作。      


Amdahl/Gustafson's law:
-----------------
**在高并发程序设计中有非常重要的两个定律，这个两个定律从不同角度诠释了**加速比**与**系统串行化程度**、**CPU核心数**之间的关系，他们使我们在做高并发程序设计的理论依据**
一、Amdahl（阿姆达尔定律）
加速比定义

加速比 = 优化前系统耗时 / 优化后系统耗时.  

所谓加速比就是优化前的耗时和优化后的耗时的比值。加速比越高，表明优化效果越明显。   

下图是该公式的推导过程：其中n表示处理器个数，T表示时间，T1表示优化前耗时(也就是一个CPU耗时),Tn表示使用n个处理器优化后的耗时。F是程序中只能串行执行的比例。  
![gpu](https://img-blog.csdnimg.cn/20200719174156411.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwNDU0Mzc=,size_16,color_FFFFFF,t_70). 

二、Gustafson（古斯塔夫森定律）

该定律也试图说明处理器个数，串行化比例和加速比之间的关系，但是和阿姆达定律的角度不同，加速比的定义仍然被定义为优化前的系统耗时除以 优化后的系统耗时。
![gpu](https://img-blog.csdnimg.cn/20200719194012622.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwNDU0Mzc=,size_16,color_FFFFFF,t_70). 


从上面的公式我们可以看出两个公式截然不同，Gustafson定律中，我们可以更容易的发现，如果串行化比例很小，并行化比例很大，那么加速比就是处理器个数，只要不断的累加处理器数，就能获得更快的速度。

三、是否矛盾

两个定律的结论不同，这是不是说两个定律中有一个是错误的呢，其实不然，两者的差异其实是因为这两个定律对一个客观事实从不同角度去审视的后果，他们的侧重点不同。

Amdahl强调，当串行化比例一定时，加速比是有上限的，不管你堆叠多少个CPU参与计算，都不能突破上限。

而Gustafson 定律的出发点不同，对Gustafson定律来说，如果可被并行化的代码所占比例足够大，那么加速比就能随着CPU的数量线性增长。

所以这两者并不矛盾，从极端的角度来说，如果系统中没有可以被并行化的代码，那么对于两个定律，其 加速比是1，反之，如果系统中可被并行化的代码比例100%，那么两个定律得到的加速比都是处理器个数。



Die size and constraints(die Size =chip size + Scrible line 及限制)：
-----------------
The notion that as demand increases, you can spin up more instances that you can have those instances located geographically closer to you, you know, in the cloud data centers, etc.   

面积举例：So that brings us nicely on to win size we talked about before in terms of the die sizes and stuff like that. So the far a given real estate area, a chip generally has an integrated circuit generally has a given real estate area, Tara has a certain size. 

物理角度的问题 ：因此，如果我有一定的尺寸或一定的最大尺寸，我的集成电路将无法超越。为了超越这一点，我对可以放在它上面的一定大小的电路数量施加了物理限制。因此，如果我有一英寸见方的东西，我可以在14纳米工艺上放置多少个晶体管？这就是计算，它可以在芯片设计软件上完成非常非常快，进入一个布局的事情，你如何处理热量，以最小化你的连接长度和你的互连？所有这些东西都成了一个问题。因此，尺寸是这些限制之一，无论是在物理方面，还是在我们有一个典型的芯片尺寸封装，适合我们进行冷却，你知道，对于芯片支架和载体以及类似的东西。

但与物理相关的是，实际集成电路的尺寸是电路本身的大小之一。所以说实际的制造技术尺寸，是14米还是10米，都是我们的14纳米。10纳米7纳米。一般来说，量子变化的变化是否会在制造过程中的增量变化的重大变化将在5到7到10年之间，仅仅是因为芯片制造商在建造新晶圆厂设施时所涉及的持续时间召回，如你所知， 英特尔在leixlip中有一些，并且正在谈论建立一个新的和目标，但通常需要五到七年的时间来建立工厂。   
所以，如果我们看你知道，14或1211 10 Seven现在谈论，近10年，十年前，当新一代或近十年前，你将真正看到这一点并制造。这就是采取这些步骤所涉及的那种提前期。下。因此，从物理学的角度来看，我们所在的技术公司非常接近于我们所能做的实际极限。因此，随着芯片尺寸变得越来越小，并且您知道精确到1412 10纳米尺度，物理影响电子的实际物理效果如何和不泄漏电流等，开始变得更加显着。 

问题出现：泄漏电流   
他们确定问题是什么，识别出泄漏来自哪里，他们重新设计一个电路。但是，尽管需要意识到这一点，但这并不是一件容易的事。当您扩展某些内容时，请纵向扩展或缩减。您将开始遇到这些外部第三方约束。一旦您在手机上编程，这些约束不仅会进入您的计算机。   



内存墙（memory wall）
-----------------
在过去的20多年中,处理器的性能以每年大约55%速度快速提升，而内存性能的提升速度则只有每年10%左右。长期累积下来，不均衡的发展速度造成了当前内存的存取速度严重滞后于处理器的计算速度，内存瓶颈导致高性能处理器难以发挥出应有的功效，这对日益增长的高性能计算(High Performance Computing,HPC)形成了极大的制约。事实上，早在1994年就有科学家分析和预测了这一问题，并将这种严重阻碍处理器性能发挥的内存瓶颈命名为"内存墙"(Memory Wall)      

简单来说就是内存的性能提升太慢，导致计算机的计算能力提升达到一定的瓶颈      
即使再增加处理器的核数，也无法提高综合计算能力（实际上超过16核，就已经不会对性能有多大提升了）     

一般来说，CPU速度已经超过了构成的内容。如果您喜欢RAM，这就是为什么你以不同的方式开始缓存，等等。但是GPU非常特别，因为很多GPU，在从事内存密集型活动时，从中提取大量的数据文件并将其推出数据回内存进行包装。因此，这是GPU的一个约束，它一直是导致CPU或GPU速度的原因之一。时钟速度保持在低位，但它是激励还是优势。超速不是线性的，因为您正在围绕内存吞吐量等各种问题遇到各种问题。  
__RAM__: 
RAM，是指随机存取存储器（random access memory，RAM）又称作“随机存储器”，是与CPU直接交换数据的内部存储器，也叫主存(内存)。它可以随时读写，而且速度很快，通常作为操作系统或其他正在运行中的程序的短时间临时数据存储媒介。计算机首先从存储盘将用户请求的程序或文档加载到内存，然后从内存中访问每条信息。由于许多操作均依赖于内存，因此RAM 容量在系统性能方面起着至关重要的作用。     

In GPUs you'll often see them aiming for maybe 25 to 50 the throughput. Totally, I have an memory give me 50. But then we touched on earlier in terms of what's happening with CPUs, GPUs in particular is they're now able to work and operate and process data at a speed that simply faster than they did to design characteristic of the actual memory chips can keep up with. So if you buy a memory CAP, you'll see there are various numbers of like CAS and latency and stuff like that. And they're related to the number of cycles number of instruction cycles number of Read, write operations required to read or write from that you know it okay, it's not meant to be a hit circus.


__CAP__:  
分布式系统正变得越来越重要，大型网站几乎都是分布式的。分布式系统的最大难点，就是各个节点的状态如何同步。CAP 定理是这方面的基本定理，也是理解分布式系统的起点。
本文介绍该定理。它其实很好懂，而且是显而易见的。下面的内容主要参考了 Michael Whittaker 的文章。https://www.ruanyifeng.com/blog/2018/07/cap.html  

![gpu](https://www.wangbase.com/blogimg/asset/201807/bg2018071607.jpg)

1998年，加州大学的计算机科学家 Eric Brewer 提出，分布式系统有三个指标。   
Consistency.  
Availability.  
Partition tolerance.  
它们的第一个字母分别是 C、A、P.  
Eric Brewer 说，这三个指标不可能同时做到。这个结论就叫做 CAP 定理。无法同时做到一致性和可用性。系统设计时只能选择一个目标。如果追求一致性，那么无法保证所有节点的可用性；如果追求所有节点的可用性，那就没法做到一致性。   
举例来说，发布一张网页到 CDN，多个服务器有这张网页的副本。后来发现一个错误，需要更新网页，这时只能每个服务器都更新一遍。
一般来说，网页的更新不是特别强调一致性。短时期内，一些用户拿到老版本，另一些用户拿到新版本，问题不会特别大。当然，所有人最终都会看到新版本。所以，这个场合就是可用性高于一致性。  

bus----->IPC（Inter-Process Communication，进程间通信）。进程间通信是指两个进程的数据之间产生交互：
----------------- 
有不同类型的总线，将数据移入和移出外部存储设备，移入和移出内存，通常是在他们的CPU内和在他们自己非常高吞吐量的主干中。     

IPC(Inter-Process Communication)进程间通信，提供了各种进程间通信的方法。在Linux C编程中有几种方法.  
(1) 半双工Unix管道.  
(2) FIFOs(命名管道).  
(3) 消息队列.   
(4) 信号量. 
(5) 共享内存. 
(6) 网络Socket. 


CAS：
-----------------
CAS是compare and swap的缩写，就是比较并替换的意思。   

1.CAS（比较并替换）如何保障数据一致性的？
我们设想一下，假如有2个线程。同时要操作计算机内存中的数据X=10，并将X进行加1操作。
比如线程I获取X，线程II获取X，线程II进行加1操作。此时线程I获取的X的值为10，加1之后变为11，而线程II已经将X的值变为11，因此两个线程对X的加一操作并没有达到理想中的12，而是变成了11。所以数据的一致性就得不到保障。那么面对这种情况，该如何保障数据的最终一致性？CAS的处理方式是在给X设置值得之前获取X的值，然后比较在设置值得的时候的时间段内获取到的值是否与内存中的值相同，如果相同的话，就表示X的值没有被其他线程修改，如果内存中的值与之前获取到的值不一致就表示该值已经被其他线程修改，所以该线程就抛弃之前获取到的内存中的值，并将新值作为标志。如此循环，直到计算前后从内存中获取的数据没有变化，就将其计算的结果放置到内存中。所以说CAS其实就是通过比较计算前后，所操作的数据是否发生变化来进行高并发情况下数据的一致性的。如果没有发生变化就说明当前线程的操作是安全的，否则就轮循直到所操作的数据不再变化再进行计算和赋值操作。    
在此可能有人会说，那么在比较确认数据没有被其他线程修改之后设置值得时候被其他线程修改了数据怎么办？这里要注意一下CAS最终设置值得时候采用的计算机指令是原子性的，也就是说会一步走到结束。

2.CAS机制的优势和劣势是什么？
轮循导致的CPU消耗   
上边说到如果所操作的数据在当下线程操作的空隙已经发生了变化，就需要不断的去轮询，直到其不再发生变化了之后才进行下一步操作。但是轮询非常消耗CPU。   
只能保障数据的原子性，无法保障代码块的原子性   
当多个线程操作相同的数据时，使用CAS策略能够保证该数据的原子性，但是无法保障代码块的原子性。要想实现代码块中的数据不被其他线程修改（不与预期值发生偏差），则必须使用synchronized来进行代码块级别锁了   

1）大多数这些事件的物理特征，实际的重写方式，都可以操作。因此，您可以大大加快它们的速度。您必须重新设计它们，每次都使用不同的内存技术来执行此操作。  


冷却
-----------------
Most of those events physical characteristic, how the actual rewrites are, can operate. So you can significantly speed them up. You have to redesign them every use a different memory technology to do so. So in general CPU speeds have been exceeding what constitutes.  

__voltage and frequency__:  
Most modern CPUs, particularly Cisco devices, have this capacity to dynamically scale their voltage and frequency requirements or demands.   

因此，如果我有一个CPU或微处理器，并且它的作用很小，你知道，一些内核处于睡眠模式，我可能会运行略低的电压。如果我能自己运行略低的电压，我消耗的功率就会更少。因此，消耗更少的功率，我产生的热量更少，因此我需要更少的冷却和一切。   
On the other hand, if I have, you know, a heavy workload, being able to increase ultimate sort of my maximum design voltage and run at a higher frequency, means I'd get through the workload more quickly, but at the cost of producing more heat, and you would be surprised at quite, you know, how much power you can save by simply dynamically adjusting the voltage and frequency. So if you look over here at this table, this is sort of showing you the power consumption for well power consumption performance for a particular technology, depending on relatively small changes. So I think 14 plus plus one（交流电？） allowed far better dynamic voltage and frequency scaling than the straight（直流） 14 did.    

Most desktop CPUs, you know, the sort of KCC sitting under a desk in the lab or something had worked were reasonably happily on sort of 100 watt power supplies for a long time.  
而且，最近，特别是一些较新的CPU和多个GPU的存在发生了变化，并且已经增加了。所以当时，如果我买了一张GPU卡，在插入GPU之前，我必须更换台式机和机器中的CPU电源单元，或者没有足够的CPU电源。我通常必须添加一些从100瓦260或200瓦开始的东西。因此，当时高端GPU，向机器添加GPU可能会增加100瓦的消耗，这并不像100瓦灯泡那样小，当你每天24小时运行它时，它并不小。如今，如果您想添加高端GPU或GPU卡，也许是具有多个CUDA内核的卡，您可能会看到该卡需要O 400 500瓦的功率，仅用于GPU卡。  

__CUDA__：是流处理器是直接将多媒体的图形数据流映射到流处理器上进行处理的.  


晶体
-----------------

__photomask or photorag Radical radical drive__：  
因此，这在很大程度上归因于制造过程和更大需求的结合，消费者需求来自你和我对比特币矿工的需求，每个GPU的每张卡具有更大的处理能力范式区域，因此像Nvidia这样的制造商已经做出了某种反应，生产不同的屏蔽胶带。它的不同之处在于它被称为光掩模或光撕裂激进的激进驱动器，所以我是一个问题。这基本上是他们今天用来传输魔术图案的图案装置。因此，他们一直在努力解决这些问题，并改进您可以想象的那些。我想这样做的一个结果是，你现在可以在给定的CPU或GPU上做并执行更多的操作，部分原因是我们有更多的晶体管，我们有更多的流水线架构，因为更精细的分辨率，更精细的光掩模粒度，但也因为我们只是简单地添加更多，所以它也需要一个给定的需求，我们像人工智能一样思考， 您现在可以购买专用的GPU，这些GPU具有称为AI内核的张量内核，该张量内核实现了您在TensorFlow中找到的一些功能。

__光掩模__：  
在制作集成电路的过程中，利用光刻蚀技术，在半导体上形成图型，为将图型复制于晶圆上，必须透过光掩模作用的原理[1]。比如冲洗照片时，利用底片将影像复制至相片上。  

__A FinFET Field Effect Transistor process__：  
It's an 18 point 6 billion transistors on the on the device with DDR D DDR six memory for speed, and 50 Gig bandwidth 25 or 25 or 25 and 25 hours, but 18 point 6 billion transistors on a die or a GPU. So the scale of what's going on now is enormous, but each of those 18 point 6 billion transistors needs to be powered, hmm constitutes a switching operation.So the scale of what we're talking about here is enormous. 
鳍式场效应晶体管( FinFET ) 是一种多栅极器件，一种MOSFET（金属氧化物半导体场效应晶体管），构建在基板上，栅极位于通道的两个、三个或四个侧面或环绕沟道，形成双栅甚至多栅结构。这些器件被赋予通用名称“FinFET”，因为源/漏区在硅表面上形成鳍。与平面CMOS（互补金属氧化物半导体）技术相比，FinFET 器件具有明显更快的开关时间和更高的电流密度。  
FinFET 是一种非平面晶体管，或“3D”晶体管。它是现代纳米电子 半导体器件制造的基础。使用 FinFET 栅极的微芯片在 2010 年代上半年首次商业化，并成为14 nm、10 nm和7 nm工艺节点的主要栅极设计。   

Dennard Scaling
-----------------
Dennard Scaling，其大致意思是，虽然晶体管尺寸在每一代产品中会变小，但它们的功率密度保持不变。因此功耗与电路面积成正比关系；电压和电流则均按晶体管尺寸长度降低。

当我们使用数十亿个晶体管时，我们会遇到各种缩放问题，但一般来说，随着晶体管变得越来越小，功率密度也会增加。因为从本质上讲，功耗特性不会随尺寸线性缩放。如果我有晶体管的大小，它没有功耗。所以你没有线性来使一切都变小。你放上去的越多，它们越聪明，消耗更少的电力。但这不是如果你有尺寸，它消耗一半的功率，你有这种1.401 R方形的例程几乎一直在进行。收缩所做的是，它确实允许你提高时钟速度，因为互连更短，并且将数据编码切换到晶体管电路的实际物理特性更快，因为它更小。但是你随后用一定的漏电流漏电来解决这个问题，随着你越来越严格，漏电会成为一个更大的问题，越来越接近。  

一旦你进入更高的泄漏电流，你可以停止你的芯片熔化，因为你有VI关系的功率。因此，如果降低电压，那么将降低功率，在这种情况下，将使用产生的泥热。因此，对任何东西的缩放都有一个合理的实用限制。  
__Tensor Cores__就是一种专为深度学习而设计的计算核心，与FP32的训练相比，可以提供效率更高的训练性能和推理性能。在这样超强的运算效率基础上，能够让计算机视觉、自然语言处理、语音识别与文字转换、个性化推荐等过去CPU难以实现的功能也得以高速完成计算！

一般来说，如果你去更高的频率，这意味着更多的功率。如果你去更高的电压意味着更多的功率，更多的功率意味着更高的温度，所以你通常需要冷却，因为我们把更多的晶体管放在一个芯片上意味着更多的功率。电力表现为热量。这就是为什么你有电压调节，频率调节等。还有该中心的正常解决方案。当您迁移到数据中心时，云的冷却将成为一个巨大的挑战。这也是为什么如此多的数据中心建在更温和的地区的原因之一。因此，与其将它们建在沙漠中，依靠大量的电力，大量的深奥冷却剂并卸载昂贵的电路，不如将它们放在更凉爽的地方，让环境来做。温暖气氛。这基本上就是为什么我们最终在爱尔兰拥有大量数据中心的原因，我们有一个更温和的气候。有些时候，像爱尔兰这样的灾难性温带气候，通常约为成本的三分之一，一半的成本用于冷却。。如果你把自己带到一个更温暖的环境，沙漠环境或美国的部分地区，你会看到70%到80%的成本用于冷却。因此，能够定位在像爱尔兰这样的温带气候中，提供导电性，可以节省大量资金。























