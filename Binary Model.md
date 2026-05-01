这是一个计算机安全领域的学术项目，目的是提升language model在汇编层次binary analysis任务上的性能。

汇编代码中跳转指令分为direct jump和indirect jump，在这个项目中，我们只关注direct jump。 Direct jump的目标一共有三类：
```
jmp 0x401234        ; 绝对地址
je  short loc_402  ; 相对偏移
call printf         ; 直接调用
```

我们的思路是通过修改模型结构，使得模型能够在处理汇编代码中跳转指令时，对跳转的目标重点关注。这个项目通过attention bias的方法实现这一点。在attention score计算时，对"跳转源→跳转目标"这对token额外加一个正的bias。从而使得模型对跳转目标分配更高的注意力权重。（类似于Graphormer的spatial encoding）

