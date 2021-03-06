# 写给后端的Hadoop初级入门教程：基本概念篇

## 前言：

Hello大家好，我是`韩数`。距离我们上一个系列[写给后端的Nginx初级入门教程](https://juejin.im/post/5dc8ede66fb9a04a5e6da815)已经过去整整25天了，中间穿插了两篇区块链相关的文章，其实吧，这二十来天我一直在憋大招，那就是这个最新的系列写给后端的Hadoop初级入门教程，由于Hadoop本身的技术细节还是很多的，`Hadoop基础环境的搭建`，`分布式伪分布式的部署`，`集群启动的准备`,`hdfs文件系统`，`MR编程模型`，以及最后的`优化`等等，整个一套写下来工作量还是蛮大的，好在我快放寒假了(开心)，这样使得我有充足的时间和精力去写这套教程，一来是为了帮助自己在写作的时候更加深入地理解这方面的知识，而来是希望可以帮助到那些刚刚准备入门大数据的朋友们去理解和使用Hadoop这门技术。毕竟大家都知道，现在网上搜到的那些技术教程，质量参差不齐，一不小心踩到坑就是：

**一电脑，一根烟，一篇教程学半天，调试半天却不对，想送作者上青天。**

好湿好湿，本篇文章作为整套Hadoop入门教程的第一篇，我们依然从最基础的概念说起，什么是大数据，大数据如何影响我们的生活？什么是Hadoop，Hadoop和其他大数据技术相比又有哪些优势？明白了这些问题，我相信再学大数据，虽然不能说有buff加成，但是至少知道自己接下来要学的这玩意儿是个啥了。

不废话，直接上东西

## 什么是大数据：

大数据 (Big Data) : 主要是指`无法在一定范围`内用常规软件工具进行捕捉，管理和处理的数据集合，是需要新处理模式才能具有更强的决策力，洞察发现力和流程优化能力的`海量，高增长率和多样化的信息资产`。

一句话解释：**大数据就是大量数据，数据多到传统方案无法处理的程度。**

当然数据的体量并不是最重要的，重要的是隐藏在这些数据中的`信息`，这些信息不论是在商业上还是在研究上都有着巨大的价值，电商通过挖掘这些数据中的信息为每个用户画像，并且推荐合适的商品给用户增加购买，当然，也可以顺便调整一下改个价格杀个熟什么的。

### 大数据的单位：

但我们毕竟是严谨的理科生啊，你说大数据大数据，多大才是大数据？为了解决这个问题，减少撕逼，科学家就制定了一系列的数据单位，从小到大依次是：

`bit` `Byte` `KB` `MB` `GB` `TB` `PB` `EB` `ZB` `YB` `BB` `NB(牛逼)` 和 `DB（呆逼）`

当然，光讲这些单位有什么意思，我怎么能知道这些单位能存多少数据？为了方便大家更加直接的感受到这些数据单位的威力，我找了一些小栗子：

- 全世界所产生的印刷材料的数据大概是200PB。
- 全世界人类总共说过的话大概是5EB。
- 国外知名网站P站2017年网站产生的总数据量为 3732PB 。
-  一百万个汉字大概所需要的内存是2MB。

刚才好像混入了什么奇怪的东西。

### 大数据的特点：

- `大量：`必须的，不大都不好意思叫大数据。
- `高速：`这么多数据肯定要快速消化掉的，处理几十年也等不起啊，今年双十一的成交额总不能算到明年双十一再公布吧。
- `多样：`不同的场景会产生不同的数据，优酷就是用户浏览数据，视频数据，QQ音乐就是音乐数据。
- `低价值密度：`这个意思是**即使数据量很大，但是我们关注的始终的特定的部分，而非整体**，就像警察叔叔调监控一样，一年前一个月前的数据通常对他来说是没什么用的，他只要那么几个关键节点的监控数据就可以了。

应用场景就不说了，哪都是应用场景。

## Hadoop是什么？

知道了什么是大数据，我们就得思考另外一个问题，弄这么多的数据我放哪啊？

`杠精：`不明摆着的么，当然放硬盘里啊，要不放哪儿，还能写纸上？
`我：`硬盘我知道，可是万一这块硬盘坏了，那数据不就没了吗？

`路人`：你系不系傻，你多放几块硬盘，分别放上去不就行了吗？

这个时候`Hadoop`来了，弟弟们都往边上靠靠，你们那种办法太笨拙，交给我，轻轻松松地给你搞定，小意思。

`Hadoop`是一个由Apache基金会所开发的分布式系统基础架构，主要用来解决大数据的存储和分析计算问题。

当然，`Hadoop`和`Spring`一样，到现在已经没法去仅仅理解为`Hadoop`这门技术了，就像你跟别人说，我这个新电商项目基于`Spring`写的，那别人肯定不会觉得你只用了`Spring`，会觉得你可能用了`Spring MVC `，`boot`，`JPA`等一系列`Spring`生态的技术。同样地，`Hadoop`也是如此，不仅仅是代表`Hadoop`本身这项技术，同时也代表围绕`Hadoop`的技术生态。

而且大家千万不要把事情想复杂，以为分布式存储什么这些概念都是多么深奥的东西，的确，官方概念确实是有点抽象晦涩了，但是我觉得，**任何一项理论都一定来源于生活，因为是生活给予了他们灵感，但是生活并不是十分复杂的，所以任何深奥复杂的理论一定可以在生活中找到一个通俗易懂的解释。**

什么是分布式存储，不跟大家吹，我初中的时候就已经在搞这个了，那时候流行看玄幻小说，那种大部头知道吧，特厚，通常一个班就只有那么一本，被教导主任没收了就完蛋了，谁都没得看，于是当时盛行把一本玄幻小说一页一页撕下来，每个同学几页，大家互相换着看，就算老师发现了也就只是没收了一部分，没办法全部歼灭。你看，分布式有了，存储有了，这不就是分布式存储吗？为了防止一本书被老师没收了导致这本书不完整，那就买三本，也这么几页几页分开存，这不就是多备份吗，没那么复杂，别老纠结那些学者写的给学者看的概念。

## Hadoop发展史：

这个也没啥好讲的，我这里就列几个关键的点，感兴趣的朋友下去可以自己搜，网上一搜一大堆。

- 一个叫Dung Cutting 没事用java写了一个全文搜索的框架 - `Lucene`
- 数据量大的时候，`Lucene`性能跟不上了就。
- 巧了，Google本身也是做全文搜索的，为啥人家性能就那么顶呢？
- 通过学习谷歌，搞了个`Nutch`
- 后来谷歌公开了部分`GFS`和`MapReduce`的细节。
- Dung Cutting 一看这答案都给自己了，于是花了两年，注意是业余时间，自己实现了`DFS`和`MapReduce`，`Nutch·性能一下字就提上去了，一个字，牛逼。
- 后来`Hadoop`作为`Lucene`子项目`Nutch`的一部分被正式引进了Apache基金会。
- 然后`Map-Reduce`和`NDFS`一块被整合进了`Hadoop`项目里面，`Hadoop`就这么诞生了。

为啥人家业余时间就能搞出来这么牛逼的东西，我业余时间王者荣耀王者都上不去，难道有中间商赚差价？

## Hadoop发行版本：

和Linux差不多，不同的公司在此基础上分别定制了自己的发行版本，`Hadoop`发行版本主要有三个，分别是：

- Apache版本：最原始（最基础）的版本，对于入门学习最好，毕竟是出生地，血统也是最正的。
- Cloudera  ：在大型互联网企业中用的较多。
- Hortonworks：文档比较全。

不用想，我们肯定选Apache，也没啥别的原因，就是因为它基础，简单，不要钱。

##  Hadoop优势是什么？

`Hadoop`为啥这么牛逼，导致我们现在一说大数据开发，就会想到Hadoop？

毕竟写程序不是谈恋爱，没什么就算你不好我也依然爱你这回事，我们坏得很，哪个好用使哪个。

`Hadoop`在江湖中能混到今天的地位主要靠以下四点：

- 高可靠性：`Hadoop`底层使用多个数据副本，即使`Hadoop`某个计算元素或存储出现故障，也不会导致数据的丢失，想想上面讲的分布式存储的例子。
- 高扩展性：在集群间分配任务数据，可以方便的扩展数以千计的节点。就是，有一天运维早上一上班，卧槽，集群存储不够了，但是问题不大，因为在集群中加入一个新的节点或者去掉一个节点都分分钟的事儿。
- 高效性：在`MapReduce`的思想下，`Hadoop`是并行工作的，以加快任务处理速度。
- 高容错性：能够将失败的任务重新分配。

你说了一堆优点，`Hadoop`就没啥缺点吗？必须有，但是这个要到后面写到`HDFS`，`MR`的时候才能说，要不现在都不知道`Hdfs`是啥，说缺点的话不形象，**就跟说人坏话一样，当着人家面儿说才有效果。**

## 下面开始技术总结：

今天这篇文章呢，作为整套`Hadoop`系列教程的第一篇，主要是按照我写博客的习惯讲了一些基本的概念，希望大家看过之后心里能够对大数据和`Hadoop`有个基本的认识，另外，我写技术文章比较口语化，废话比较多，这个欢迎大家提建议，放心，提了我也不改，但是我写小说啥的还是非常严肃的，而且废话文你读起来比那些深奥玩弄概念的文章快多了（滑稽），下一篇文章呢，我们同样也是概念篇，主要讲`HDFS`，`YARN`，`MR`这三个`Hadoop`核心概念，之后就是实打实的要和代码接触了。

非常感谢能读到这里的朋友，你们的支持和关注是我坚持高质量分享下去的动力。

相关代码已经上传至本人github。一定要点个**star**啊啊啊啊啊啊啊

**万水千山总是情，给个star行不行**

[韩数的开发笔记](https://github.com/hanshuaikang/HanShu-Note)

欢迎点赞，关注我，**有你好果子吃**（滑稽）













