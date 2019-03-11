Performance Optimization
---

## Optimization Principle

Programmers waste enormous amounts of time thinking about, or worrying about, the speed of noncritical parts of their programs, and these attempts at efficiency actually have a strong negative impact when debugging and maintenance are considered. `We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%`

97% 的时间里, 我们不应该考虑蝇头小利的效率提升: 过早优化是万恶之源, 它可能会危及程序的正确性, 可维护性. 据称这一观点来自 C.A.R. Hoare.


<div class="alert alert-info">
在早期的设计过程中, 要确保基本的系统结构具有足够的效率
</div>

## [Amdahl 定律](https://en.wikipedia.org/wiki/Amdahl%27s_law)

Gene Amdahl, 计算机领域的早期先锋之一, 对提升系统某一部分性能所带来的效果进行量化, 给出了数学描述, 称为 Amdahl 定律.

<div class="alert alert-info">
<p>Amdahl 描述了改善任何过程的一般原则.</p>
<hr>
<p>
该定律的主要思想是, 对系统的某个部分加速时, 其对系统整体性能的影响取决于该部分的重要程度和加速程度.
</p>
</div>

性能提升最好的表示方式就是用比例的形式 `T(old) / T(new)`, 其中 `T(old)` 是修改前系统所需时间, `T(new)` 是修改后系统所需时间. 如果有所改进, 则比值应大于 1. 我们用后缀 `X` 来表示比例, 因此 `3X` 读作 `3 倍`.



## [Profile 性能剖析](https://docs.python.org/2/library/debug.html)

通常程序的大多数时间都花在少量热点位置上; 根据 Amdahl 定律, 在这些热点上进行优化, 可以期望获得较大的加速比; 为了找出系统的热点, 我们首先需要借助一些工具进行性能剖析.

Profilers are handy for small programs, but indispensable for working on large software.


[cProfile](https://docs.python.org/2/library/profile.html#module-cProfile) and [profile](https://docs.python.org/2/library/profile.html#module-profile) provide deterministic profiling of Python programs.


## 改善程序运行时间的策略

当我们明确了优化的时机和位置后,

* _假如只需要少许加速, 请研究最好的层次;_ 考虑所有可能的层次, 选择能够获得最大加速比而所需精力又最少的层次.

* _如果需要大的加速, 那么要深入研究问题的各个方面;_ 取得突破需要花费大量精力, 惊人的加速是通过在若干不同层次上的努力得到的.


### Application level

* Concurrent (multi-threading, multi-process, coroutine)

* Proper Algorithm and Data Structure

* Cache answers to expensive computations, rather than doing them over

* Use hints to speed up normal execution

* Use batch processing if possible

* Pipeline

* Data Locality

    most input data is read locally and consumes no network bandwidth


### Language level

惯用法

* [Performance Tips](https://wiki.python.org/moin/PythonSpeed/PerformanceTips)


### OS level

1. 尽量减少系统调用或者选择高效的系统调用

2. 操作系统级别的参数调优


### Hardware level

运行速度更快的硬件可以提供性能


