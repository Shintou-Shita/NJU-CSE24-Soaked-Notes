# L06 Machine-Level Programming II: Control

Source: https://www.bilibili.com/video/BV1iW411d7hd?p=6

Four parts

1. Control: Condition Codes
2. Conditional branches
3. Loops
4. Switch Statements

## Part 1: Control: Condition Codes

条件码（condition codes）是运算时额外存储的标志位（bit flags），其作为条件指令（conditional operation）运作的基础。

特殊的寄存器：%rsp，意为 stack pointer，为栈指针。

另一个特殊的寄存器：%rip，意为 instruction pointer，为指令指针，IA32 中为 %eip，其包含的是当前正在执行指令的地址，这个寄存器你无法直接地、正常地访问。同样有 32 位的 %eip 和 16 位的 %ip，共享一个寄存器。

条件码存储在 %rflags 这个状态寄存器（status register）上：32 位版本的 %eflags 按如下方式存储：

​	

| 0: CF                                | 1: 1                               | 2: PF                               | 3: 0                                   |
| ------------------------------------ | ---------------------------------- | ----------------------------------- | -------------------------------------- |
| 4: AF                                | 5: 0                               | 6: ZF                               | 7: SF                                  |
| 8: TF                                | 9: IF                              | 10:DF                               | 11: OF                                 |
| 12-13: IOPL                          | 14: NT                             | 15: 0                               | 16: RF                                 |
| 17: VM                               | 18: AC                             | 19: VIF                             | 20: VIP                                |
| 21: ID                               | 22-31: 0                           |                                     |                                        |
| carry flag 进位标志                  | /                                  | parity flag 奇偶标志                | /                                      |
| auxiliary carry flag 辅助进位标志    | /                                  | zero flag 零标志                    | sign flag 符号标志                     |
| trap flag 跟踪标志                   | interrupt-enable flag 中断许可标志 | direction flag 方向标志             | overflow flag 溢出标志                 |
| I/O privilege level IO 特权标志      | nested task 嵌套任务标志           | /                                   | resume flag 恢复标志                   |
| virtual-8086 mode 虚拟 8086 方式标志 | alignment check 对齐检查           | virtual interrupt flag 虚拟中断标志 | virtual interrupt pending 虚拟中断等待 |
| ID flag 识别标志                     | /                                  |                                     |                                        |

四个常用的条件码：对于 `t = a + b`：假设运算位数为 $w$

- CF: carry flag (for unsigned) 【进位标志/无符号运算溢出位】：为两个无符号整数相加后第 $w$ 位（$\operatorname{floor}(?/2^w)$）。
- ZF: zero flag 【零标志】：为 1 当且仅当 `t` 为 0，也即等价为 `a == b`.
- SF: sign flag (for signed) 【符号标志】：为 1 当且仅当 `t` 小于零，其直接等于 `t` 的第 $w-1$ 位。
- OF: overflow flag (for signed) 【溢出标志/有符号运算溢出位】：为 1 当且仅当：`(a > 0 && b > 0 && t < 0) || (a < 0 && b < 0 && t >= 0)`.

指令 `cmp`（compare）接受两个参数：`cmpq src2,src1`，接下来它会计算 `src1 - src2`. 其做的事情和减法指令几乎一样，但是只进行运算不进行赋值。显然这个指令因为进行了计算，所以条件码会被设置。

指令 `test`（test）接受两个参数：`testq src2,src1`，接下来它会计算 `src1 & src2`，类似地，只进行运算不进行赋值，条件码同样会被设置。一般来说，这两个参数会设置成同一个参数，ZF 就用于判零，SF 就用于判负。

设置条件码指令（可间接获取标志标志位（））：

​	`set` 指令的作用是将当个寄存器的单个字节置值，当被改写为如下形式时，则为有条件地设置。

| SetX    | Condition    | Description      | SetX    | Condition   | Description            |
| ------- | ------------ | ---------------- | ------- | ----------- | ---------------------- |
| `sete`  | ZF           | Equal/Zero       | `setge` | ~(SF^OF)    | GreaterOrEqual(Signed) |
| `setne` | ~ZF          | NotEqual/NotZero | `setl`  | SF^OF       | Less(Signed)           |
| `sets`  | SF           | Negative         | `setle` | (SF^OF)\|ZF | LessOrEqual(Signed)    |
| `setns` | ~SF          | Nonnegative      | `seta`  | ~CF&ZF      | Above(Unsigned)        |
| `setg`  | ~(SF^OF)&~ZF | Greater(Signed)  | `setb`  | CF          | Below(Unsigned)        |

例如：

```c
int gt(long x, long y) {
    return x > y
}
/*
%rdi   argument x
%rsi   argument y
%rax   return value
*/
```

``` assembly
cmpq   %rsi, %rdi  # compare x:y
setg   %al         # set when >
movzbl %al, %eax   # zero rest of %rax
ret
```

这里 `movzbl` 指令总体上是 `mov` 指令，但是有一个转换：`z` 表示零扩展，`b` 和 `l` 分别表示字节（byte，8 位）和长字（long word，32 位），那么为什么不是 `movzbq` 呢？首先没有这条指令，其次 `%rax` 高位会自动清零——对低 32 位操作会清理高 32 位，这个规则对字节-双字节不适用，至于谁设计了这条长字-四字规则，只有天知道。

## Part 2: Conditional branches

jX instructions（条件跳转指令）：

之前十条 setx 改为 jx，额外加上一条无条件跳转指令：`jmp`，条件：`1`，描述：Unconditional（无条件）.

条件跳转指令（老式）

```c
long absdiff(long x, long y) {
    long result;
    if (x > y)
        result = x - y;
    else
        result = y - x;
    return result;
}
/*
%rdi   argument x
%rsi   argument y
%rax   return value
*/
```

generation:

```bash
shark> gcc -Og -S -fno-if-conversion control.c
```

```assembly
absdiff:
   cmpq    %rsi, %rdi # x:y
   jle     .L4
   movq    %rdi, %rax # branch1
   subq    %rsi, %rax # branch1
   ret                # branch1
.L4:       # x <= y
   movq    %rsi, %rax # branch2
   subq    %rdi, %rax # branch2
   ret                # branch2
```

条件跳转指令（使用 goto）

```c
long absdiff_j(long x, long y) {
    long result;
    int ntest = x <= y;
    if (ntest) goto Else;
    result = x - y;
    goto Done;
Else:
    result = y - x;
Done:
    return result;
}
```

广义条件表达式翻译，使用分支（general conditional expressions translation with branches）

```c
val = Test ? Then_Expr : Else_Expr;
// result = x > y ? x - y : y - x;
```

Goto 版本：

```c
    ntest = !Test;
    if (ntest) goto Else;
    val = Then_Expr;
    goto Done;
Else:
    val = Else_Expr;
Done:
    ...
```

使用条件移动（conditional moves）：Then 和 Else 结果同时计算，然后再根据 Test 计算决定取哪个，其中**不需要暂停处理器的执行，特别是流水线的执行**，看上去效率差，但反而更有效率，特别是计算十分简单的时候这一优点更加突出：这要得益于流水线技术，特别是其中的指令跳转预测。

普通 C 代码和前述一致，Goto 版本如下：

```c
    result = Then_Expr;
    eval = Else_Expr;
    nt = !Test;
    if (nt) result = eval;
    return result;
```

```assembly
absdiff:
    movq    %rdi, %rax  # x
    subq    %rsi, %rax  # result = x - y
    movq    %rsi, %rdx
    subq    %rdi, %rdx  # eval = y - x
    cmpq    %rsi, %rdi  # x:y
    cmovle  %rdx, %rax  # if <=, result = eval
    ret
```

条件移动很坏的情况：

1. 各分支计算花费大

```c
val = Test(x) ? Hard1(x) : Hard2(x);
```

2. 计算有风险

```c
val = p ? *p : 0;
```

解引用可以吗？这段代码逻辑上来说没问题，非空则取其指向的值，但空指针解引用爆了——计算存在风险。

3. 计算有副作用

```c
val = x > 0 ? x *= 7 : x += 3;
```

两个分支的计算可能产生副作用干扰。

以上三种情况，编译器不会采用条件移动优化。

## Part 3: Loops

Do-While 循环的例子：C 语言代码：

```c
long pcount_do(unsigned long x) {
    long result = 0;
    do {
        result += x & 0x1;
        x >>= 1;
    } while(x);
    return result;
}
```

goto 版本：

```c
long pcount_do(unsigned long x) {
    long result = 0;
loop:
    result += x & 0x1;
    x >>= 1;
    if (x) goto loop;
    return result;
}
```

注：以上函数用于计算数据在二进制下 1 的个数，一般称为 `popcount()` 函数。

```
do
    Body
    while (Test);
-------------------------------
loop:
    Body
    if (Test)
        goto loop;
===============================
while Test
    Body
-------------------------------
    goto test;
loop:
    Body
test:
    if (Test)
        goto loop:
done:
-------------------------------
    if (!Test)
        goto done;
loop:
    Body
    if (Test)
        goto loop;
done:
===============================
```

for 循环形式：

```
for (Init; Test; Update)
    Body
-------------------------------
Init;
while (Test) {
    Body
    Update;
}
```

显然这些循环编译过程中有很大优化空间，实际上也确实优化了很多。

## Part 4: Switch Statements

 ```c
 long switch_eg(long x, long y, long z) {
     long w = 1;
     switch(x) {
     case 1:
         w = y * x;
         break;
     case 2:
         w = y / z;
         /* Fall Through */
     case 3:
         w += z
         break;
     case 5:
     case 6:
         w -= z;
         break;
     default:
         w = 2;
     }
     return w;
 }
 ```

switch 语句转为汇编：跳转表结构（jump table structure）

```
// switch form
switch (x) {
case val_0:
    Block0
case val_1:
    Block1
    ...
case val_n-1:
    Blockn-1
}
-------------------------------
// jump table
jtab: Targ0
      Targ1
      Targ2
      ...
      Targn-1
-------------------------------
// actual
goto *JTab[x];
```

```c
long switch_eg(long x, long y, long z) {
    long w = 1;
    switch(x) {
        ...	
    }
    return w;
}
/*
%rdi  argument x
%rsi  argument y
%rdx  argument z
%rax  return value
*/
```

```assembly
.section    .rodata
    .align 8
.L4
    .quad    .L8 # x = 0
    .quad    .L3 # x = 1
    .quad    .L5 # x = 2
    .quad    .L9 # x = 3
    .quad    .L8 # x = 4
    .quad    .L7 # x = 5
    .quad    .L7 # x = 6
    
.L3 # 普通分支
    movq     %rsi, %rax # y
    imulq    %rdx, %rax # y * z
    ret
    
.L5 # 下落分支，这三个分支被编译器优化得联合起来写了
    movq     %rsi, %rax
    cqto
    idivq    %rcx       # y / z
    jmp      .L6        # goto merge
.L9
    movl     $1, %eax   # w := 1
.L6 
    addq     %rcx, %rax # w += z
    ret

.L7
    movl     $1, %eax   # w := 1
    subq     %rdx, %rax # w -= z
    ret
.L8                     # Default
    movl     $2, %eax   # w := 2
    ret
    
switch_eg:
    movq    %rdx, %rcx
    cmpq    $6, %rdi      # x:6
    ja      .L6           # Use default
    jmp     *.L4(,%rdi,8) # goto *JTab[x]
```

编译器可能将 switch 语句优化成较短的 if-else 链甚至改用二分搜索（cases 过多时）

## Summary

- C Control
  - if-then-else
  - do-while
  - while, for
  - switch

- Assembler Control
  - conditional jump
  - conditional move
  - indirect jump (via jump tables)
  - compiler generates code sequence to implement more complex control

- Standard Technique
  - Loops converted to do-while or jump-to-middle form
  - Large switch statements use jump tables
  - Sparse switch statements may use decision trees (if-elseif-elseif-else)









