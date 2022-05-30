# proj145技术报告

## 目标

ebpf in rust 目前有五个主要目标

- [x] [kprobes](./sys_design//kprobes.md)

  完成内核空间指令的动态插桩，对内核函数/合法指令进行跟踪。

- [x] [uprobes](./sys_design/uprobes.md)

  完成用户空间指令的动态插桩，对用户态程序中的函数/合法指令进行跟踪。

- [ ] function parameter probing in probes。

  完成probes对函数参数的获取

- [ ] async in probes

  完成probes对rust async 函数的跟踪支持。

- [ ] ebpf

  根据ebpf原理实现一个简单的ebpf。

