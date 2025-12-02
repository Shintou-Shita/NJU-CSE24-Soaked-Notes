# L07 Machine-Level Programming III: Procedures

Source: https://www.bilibili.com/video/BV1iW411d7hd/?p=7

过程（procedure）：在不同语言中可能称为函数（function）、过程（procedure）、以及 OOP 中的方法（method）

应用程序二进制接口（ABI, application binary interface），L07 就重在讲 ABI. Windows ABI 和 Linux ABI 不完全相同，苹果的 OSX 也有自己的 ABI，甚至 FreeBSD（Unix 操作系统的另一种变体）也有自己的 ABI，它们都很类似但在细节上不同。

## 过程的机制（mechanisms in procedures）

```
P(...) {
    ...
    y = Q(x)
    print（y）
    ...
}
int Q(int i) {
    int t = 3 * i;
    int v[10];
    ...
    return v[t]; 
}
```

- 传递控制权 passing control
  - 调用另一个过程 to beginning of procedure code
  - 调用结束后返回调用位置 back to return point
- 传递数据 passing data
  - 传递参数 procedure arguments
  - 返回返回值 return value
- 内存管理 memory management
  - 函数执行时分配空间 allocate during procedure execution
  - 函数返回时释放空间 deallocate upon return 
- mechanism  all implemented with machine instructions
- x86-64 implementation of a procedure uses only those mechanisms required

今天：过程

- 栈结构 stack structure
- 调用惯例 calling conventions
  - passing control
  - passing data
  - managing local data
- 刻画递归 illustration of recursion

## x86-64 栈

```
---------------------  地址增加  【栈底】
|                   |    ↑
---------------------
|       ......      |
---------------------
|                   |    ↓
---------------------  栈往下
|                   |
---------------------  <- 栈指针 %rsp  【栈顶】
```

程序用栈来管理过程调用与返回的状态，我们有 `push` 和 `pop` 这两个明确的指令来对栈进行操作。

`push src` ：1. 获取操作数 `src` （可以来自立即数、寄存器、内存） 2. 栈指针减去 8 3. 入栈了，被 `%rsp` 指向。

`pop dest`：1. 获取栈顶（`%rsp` 指向的数据）2. 栈指针加上 8 3. 将获取的栈顶赋值给 `dest`，`dest` 必须是寄存器。

为什么是 8？数据都是 64 比特即 8 字节的。下面是一个例子：

```c
long mult2(long a, long b) {
    long s = a * b;
    return s;
}
void multstore(long x, long y, long *dest) {
    long t = mult2(x, y);
    *dest = t;
}
```

```assembly
0000000000400540 <multstore>:
  400540:  push   %rbx       # save %rbx
  400541:  mov    %rdx, %rbx # save dest
  400544:  callq  400550 <mult2> # mult2(x, y)
  400549:  mov    %rax, (%rbx)   # save at dest
  50054c:  pop    %rbx       # restore %rbx
  40054d:  retq              # return
0000000000400550 <mult2>:
  400550:  mov    %rdi, %rax # a
  400553:  imul   %rsi, %rax # a
  400557:  retq              # Return
```

## 过程的控制流（procedure control flow）

- 使用栈来帮助过程调用和返回
- 过程调用：`call label`
  - 将返回地址入栈
  - 跳转到 `label` 处
- 返回地址
  - 调用后的下一条指令地址 address of the next instruction right after call
  - 反汇编得到的例子（如上） 
- 过程返回：`ret`
  - 弹栈得到地址
  - 跳转这个地址

```
400544:  callq  400550 <mult2> # mult2(x, y)
400549:  mov    %rax, (%rbx)   # save at dest
  
400550:  mov    %rdi, %rax # a
    
400557:  retq              # Return
```

## 过程的数据流（procedure data flow）

ABI 约定：开头的六个参数固定由 `%rdi`、`%rsi`、`%rdx`、`%rcx`、`%rcx`、`%r8` 和 `%r9` 传递，之后的参数倒序压入栈中，返回值固定由 `%rax` 传递。

IA32 所有的参数都在栈中传递。

```
  400541:  mov    %rdx, %rbx #
  400544:  callq  400550 <mult2> #
  400549:  mov    %rax, (%rbx)   #

  400550:  mov    %rdi, %rax #
  400553:  imul   %rsi, %rax #
  400557:  retq              #
```

## 管理本地数据（manage local data）

单线程：每时每刻只有一个过程在运行，调用相当于冻结调用前过程。

因为单线程，所以我们可以为当前运行的过程分配无限的内存而不必担心和其他过程冲突，当这个过程返回时，之前用到的数据全部可以不保留。

stack frame：栈帧，用于特定调用的每个内存块。调用链（call chain）【28:30】

```
Stack-Based Language
	Languages that support recursion
		e.g. C, Pascal, Java
		Code must be "Reentrant"
			Multiple simultaneous instantiations of single procedure
		Need some place to store state of each instantiation
			Arguments
			Local variables
			Return pointer
	Stack discipline
		state for given procedure needed for limited time
			From when called to when return
		Callee returns before caller does
	Stack allocated in FRAMES
		state for single procedure instatiation
```

栈帧，包含

- 返回信息 return information
- 本体存储（如果需要）local storage (if needed)
- 临时空间（如果需要）temporary space (if neede)

```
--------------------
|                  |
| previous frame   |
|                  |
-------------------- <- frame pointer %rbp (optional)
|                  |
| frame for proc   |
|                  |
-------------------- <- stack pointer %rsp
     STACK TOP
```

管理

​	当进入过程的时候分配的空间

​		「启动」代码

​		包括 `push` 指令，这被包含在 `call` 指令中。

​	当返回的时候释放

​		「结束」代码

​		包括 `pop` 指令，这被包含在 `ret` 指令中。

大多数系统会限制栈的深度，目的是为了防止无限递归。

### x86-64/Linux 栈帧

```
--------------------
|                  |
|      ......      |
|                  |
--------------------
|                  |
| Arguments 7+     |
|                  |
--------------------    ^
| Return Address   |    |  caller frame
-------------------- -------
| Old %rbp (Op)    | <- %rbp (Optional) 
--------------------
|                  |
| Save Registers   |
|        +         |
| Local Variables  |
|                  |
--------------------
|                  |
| Argument Build   |
| (Optional)       |
|                  |
-------------------- <- %rsp
     STACK TOP
```

​	当前栈帧（从顶到底）： 

​		参数构建：用于调用的过程

​		本地变量：不能保存在寄存器中

​		保存的寄存器上下文

​		旧栈帧（可选）

​	调用者栈帧：

​		返回地址，这被 `call` 指令压入栈中

​		这次调用的各个参数。

下面为一个例子

```c
long incr(long *p, long val) {
    long x = *p;
    long y = x + val;
    *p = y;
    return x;
}
/*
%rdi  参数 p
%rsi  参数 val 和 y
%rax  参数 x 和返回值
*/
```

```assembly
incr:
    movq    (%rdi), %rax
    addq    %rax, %rsi
    movq    %rsi, (%rdi)
    ret
```

```c
long call_incr() {
    long v1 = 15213;
    long v2 = incr(&v1, 3000);
    return v1 + v2;
}
```

```assembly
call_incr:
    subq    $16, %rsp        # 
    movq    $15213, 8(%rsp)  # 此两条为强制，为了避免其中数据丢失
    movl    $3000, %esi      # 这里用 movl 是因为其指令短一些，少用一些空间（这也省...）
    leaq    8(%rsp), %rdi
    call    incr
    addq    8(%rsp), %rax
    addq    $16, %rsp
    ret 
```

```
--------------------
|                  |
|      ......      |
|                  |
--------------------
| Return Address   |
--------------------
| 15213            | <- %rsp + 8 
--------------------
| Unused           | <- %rsp
--------------------
         | Updated Stack Structure
         v
--------------------
|                  |
|      ......      |
|                  |
--------------------
| Return Address   | <- %rsp
--------------------     
```

寄存器可以进行临时存储吗？

​	可以，但是可能会被覆写，因此会存一遍。

我们有两种方法可以管理寄存器，一种称为调用者保存（caller saved）：调用者在调用之前将临时值保存在它的栈帧中；另一种称为被调用者保存（callee saved）：被调用者在使用之前将临时值保存在它的栈帧中，被调用者在返回之前恢复这些临时值。显然选择哪种方式由 ABI 这个约定规定。

x86-64 Linux 寄存器使用（书P173）
	%rax：返回值，调用者保存，可能被过程修改

​	%rdi, ..., %r9：参数，调用者保存，可能被过程修改

​	%r10, %r11：调用者保存，可能被过程修改，用于调用者保存的临时值（caller-saved temporaries）。

​	%rbx, %r12, %r13, %r14：被调用者保存，被调用者**必须**保存且恢复。

​	%rbp：被调用者保存，被调用者**必须**保存且恢复，**可能**被用作基指针（frame pointer），可以混合、匹配（mix & match）

​	%rsp：被调用者保存的特殊形式，退出过程前恢复原值。

```c
long call_incr2(long x) {
    long v1 = 15213;
    long v2 = incr(&v1, 3000);
    return x + v2;
}
```

```assembly
call_incr2:
    pushq   %rbx
    subq    $16, %rsp
    movq    %rdi, %rbx
    movq    $15213, 8(%rsp)
    movl    $3000, %esi
    leaq    8(%rsp), %rdi
    call    incr
    addq    %rbx, %rax
    popq    %rbx
    ret
```

```
--------------------
|                  |
|      ......      |
|                  |
--------------------
| Return Address   | <- %rsp
--------------------
         |
         v
--------------------
|                  |
|      ......      |
|                  |
--------------------
| Return Address   | 
--------------------      
| Saved %rbx       |
--------------------
| 15213            | <- %rsp + 8 
--------------------
| Unused           | <- %rsp
--------------------
         | Updated Stack Structure
         v
--------------------
|                  |
|      ......      |
|                  |
--------------------
| Return Address   | <- %rsp
--------------------     
```

## 递归

如上所述，因为栈帧机制和（被）调用者保存，调用自己没什么特殊的。

下面是一个例子：

```c
/* Recursive popcount */
long pcount_r(unsigned long x) {
    if (x == 0)
        return 0;
    else 
        return (x & 1) + pcount_r(x >> 1);
}
```

```assembly
pcount_r:
    movl    $0, %eax
    testq   %rdi, %rdi
    je      .L6
    pushq   %rbx
    movq    %rdi, %rbx
    andl    $1, %ebx
    shrq    %rdi
    call    pcount_r
    addq    %rbx, %rax
    popq    %rbx
.L6:
    rep; ret
```

```
Observations About Recursion
	Handled without special consideration
		Satck frames mean that each function call has private storage
			saved registers & local variables
			saved return pointer
		Registers saving conventions prevent one function call from corrupting another's data
			Unless the C code explicitly does so (e.g. buffer overflow in L09)
		Stack discipline follows call/return pattern
			If P calls Q, then Q returns before P
			Last-In, First-Out
	Also works for mutual recursion
		P calls Q; Q calls P
x86-64 Procedure Summary
	Important Points
		Stack is the right data structure for procedure call/return
			If P calls Q, then Q returns before P
	Recursion (& mutual recursion) handled by normal calling conventions
		Can safely store values in local stack frame and in callee-saved registers
		Put function arguments at top of stack
		Result return in %rax
	Pointers are addresses of values
		On stack or global
```





