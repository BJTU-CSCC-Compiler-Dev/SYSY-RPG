# Intro

在测试编译器时，一般会使用随机程序生成器（下称RPG，Random Program Generator的简称），并交给待测编译器编译，并根据编译出来的程序的运行结果判断编译器是否有错误。

RPG有一些设计目标：

* RPG生成的程序不应该具有层面的undefined behavior（下称UB）和unspecified behavior（下称UP）行为。
* RPG生成的程序应该尽可能增加被测编译器的表达能力，比如触发尽可能多的优化、使用尽可能多的语法特性。也因此，RPG生成的程序应该具有足够的多样性。
* RPG生成的程序应该能在合理的时间内结束。比如，如果生成了死循环程序，在不考虑UB的情况下，编译出来的程序不可结束，也就不可能通过编译出来的程序的运行结果判断编译器是否有错误。

目前比较有名的C语言RPG有[Csmith](https://embed.cs.utah.edu/csmith/)和[YarpGen](https://github.com/intel/yarpgen)，我们会总结两者的特性，进而开发一个新的、适合CSCC编译设计赛道的RPG。



# Csmith和YarpGen的分析

无论是Csmith还是YarpGen，都是采用Top-down的方式生成语法树和代码。

对于UB的规避：

* Csmith采用在代码中添加类似`assert`语句的方式，将生成出来的有UB的程序剔除。

* YarpGen则采用生成时动态检查，来避免UB的生成。

  比如如果YarpGen发现`c = a + b`会发生补码overflow（C语言中是UB），就会替换这个语句为`c = a - b`，他们证明了这样可以规避UB。

对于触发更多的编译优化的方法：

* YarpGen采用了一些Generation Policies，来尽可能多地触发优化。
* Csmith则可以生成CFG更复杂的程序，以触发更多的特性。



# SYSY-RPG介绍

## 生成程序特性

SYSY-PRG产生的程序具有以下特性：

* 不存在UB、UP。

* 可以通过配置文件更改程序中各个特殊情况出现的概率。

  比如可以通过配置，让程序更多地产生if语句。

* 生成的程序可以通过GCC编译，并且编译出来的程序执行时间不会超过一个配置限制。



## 实现细节









# 引用

关于Csmith和YarpGen的资料：

* PLCT实验室的学生做过一个Report，介绍了Csmith和YarpGen并做了对比，视频地址是[CSmith vs YARPGen - 陈小欧 - 20210113 - PLCT实验](https://www.bilibili.com/video/BV1rt4y1z7h4/?share_source=copy_web&vd_source=e50db9609ddbd947fa843b4929bddcf3)，报告地址是[PLCT-Open-Reports/20210113-Comparison-Between-Csmith-and-YarpGen-ChenXiaoou.pdf](https://github.com/plctlab/PLCT-Open-Reports/blob/master/20210113-Comparison-Between-Csmith-and-YarpGen-ChenXiaoou.pdf)。
* Csmith的论文地址：[https://users.cs.utah.edu/~regehr/papers/pldi11-preprint.pdf](https://users.cs.utah.edu/~regehr/papers/pldi11-preprint.pdf)。
* YarpGen的论文地址：[https://dl.acm.org/doi/10.1145/3428264](https://dl.acm.org/doi/10.1145/3428264)。





