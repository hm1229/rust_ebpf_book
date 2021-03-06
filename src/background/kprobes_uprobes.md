# Linux中的kprobes与uprobes

## kprobes

开发人员在内核或者模块的调试过程中，往往会需要要知道其中的一些函数有无被调用、何时被调用、执行是否正确以及函数的入参和返回值是什么等等。比较简单的做法是在内核代码对应的函数中添加日志打印信息，但这种方式往往需要重新编译内核或模块，重新启动设备之类的，操作较为复杂甚至可能会破坏原有的代码执行过程。

而利用kprobes技术，用户可以定义自己的回调函数，然后在内核或者模块中几乎所有的函数中（有些函数是不可探测的，例如kprobes自身的相关实现函数，后文会有详细说明）动态的插入探测点，当内核执行流程执行到指定的探测函数时，会调用该回调函数，用户即可收集所需的信息了，同时内核最后还会回到原本的正常执行流程。如果用户已经收集足够的信息，不再需要继续探测，则同样可以动态地移除探测点。因此kprobes技术具有对内核执行流程影响小和操作方便的优点。

## uprobes

uprobes 是Linux提供用户态的动态探针，合并于2012年7月发布的 Linux 3.5 内核中。uprobes 和 kprobes 十分相似，只不过用在用户态而已。 uprobes 可以检测到用户态函数入口和出口的位置。uprobes 工作原理和 kprobes 差不多，它会在目标位置插入一个断点，这样当程序执行流执行到这个地方会去执行我们设置的 uprobe handle。当我们不再不需探测和收集信息时候，可以移除断点恢复原状。