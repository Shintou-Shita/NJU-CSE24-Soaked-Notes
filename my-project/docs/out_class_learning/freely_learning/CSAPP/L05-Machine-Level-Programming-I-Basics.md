# L05 Machine-Level Programming I: Basics

source: https://www.bilibili.com/video/BV1iW411d7hd?p=5

machine-level programming：指机器码/目标代码（object code）或者汇编代码（assembly code），二者一一对应。

Four Parts:

1. History of Intel processors and architectures
2. C, assembly, machine code 
3. Assembly Basics: Register, operands, move
4. Arithmetic & logic operations

请注意！本课程的录播是 2015 年的，十年到现在很多前沿技术已经有了巨大发展。

## Part 1

Intel x86 processors（Intel x86 处理器），因处理器系列各处理器代号为 8086、8236、8386 等以 86 结尾所以称为 x86

x86 有时也称为 CISC，1980s RISC 和 CISC 并存。Intel 使用经典的 CISC 架构。

在1985 年，Intel 32 位架构，有时也称为 IA32 几乎统治了所有的代码形式。

2004 年制造的处理器发现发热过于严重，所以 Intel 控制了频率，并从单核转向多核，其共享一个缓存。

Intel 并不是唯一玩家，它有竞争对手 AMD（Advanced Micro Devices），总是落于 Intel 之下。【2019 年 AMD 一度被认为是第一，未来也有更丰富的变化】Intel 和 AMD 两家因过去的专利纠纷和对对方的针对性，产品有相似也有差异，这是下文 AMD64 基于 Intel x86 系列被创造出来的基础。（交叉许可协议）

2001 年 Intel 尝试从 IA32 转向 IA64，但结果是失败，在市场上严重受挫。

2003 年 AMD 扩大了寄存器，推出的产品取得了成功，得到了 x86-64，现在被称作 AMD64. 

整理：IA32 就是传统的 x86，之后的是 AMD64，也称作 x86-64.

目前常用的另一大处理器是 ARM（Acorn RISC Machine），由 Acorn 公司独立于 Intel 自主研发，Acorn 公司设计了更加精简的指令集，之后被收购来收购去。

## Part 2

指令（instruction）、指令集（instruction set）、指令集架构（ISA, instruction set architecture）

这个抽象之下主要是具体硬件实现，称为微架构（microarchitecture）

指令形式：机器码（machine code）和汇编代码（assembly code）

几种 ISA：x86、IA32、Itanium、x86-64

程序计数器（PC, program counter）

寄存器（堆）（register file）

状态码（condition code）存储最近计算的结果的一些额外信息，其和条件、跳转指令相关

内存（memory）

实际上，操作系统和硬件之间存在一种协作，创造了「虚拟内存」这样的东西，使得处理器上运行的每个程序都看起来像拥有自己独立的字节数组一样，实际上最终都存储在这一块内存上。

缓存（cache），你无法直接访问缓存。

C 语言程序转换为机器码：

text -- compiler -> text -- assembler -> binary -- linker -> binary 

第一步：使用编译器（compiler）转为汇编代码；第二步，使用汇编器（汇编编译器，assembler）将其转换为实际的字节形式；第三步，使用链接器（linker）将各文件的机器码融合在一起交给中央处理器处理。

库导入一部分在 compiler 时动态导入，一部分在 linker 时导入。

examples

```bash
$ gcc -Og -S sum.c 
```

其中 `-Og` 表示优化调试体验，编译器按调试方便合理优化（即贴近源代码），一般是禁用了许多优化方式，`-S` 表示只将源文件编译成汇编代码，不进行汇编和链接。得到的结果应该是 `.s` 文件。

crud，CRUD，create, retrieve, update & drop，增删改查（增，查，改，删）

鲨鱼机（shark machine）和非鲨鱼机器（non-shark）

### 汇编代码的特性

1. 有许多不同类型的整数类型，大小包括 1,2,4,8 字节
2. 数据都以数字形式存储在计算机中，不会指明是有无符号或数字/地址/指针
3. 浮点数特别处理，大小为 4,8,10 字节等，使用特殊的寄存器组存储

检查是否是真的可能的汇编：反汇编器（disassembler）：将机器码反汇编为汇编代码。

虽然说汇编和机器码一一对应，但汇编中的变量名称汇编后就完全丢失。

```bash
$ gcc -Og sum.c -o sum 
```

反汇编

```bash
$ odjdump -d sum > sum.d
```

当然你也可以使用 gdb 调试。

## Part 3

x86-64 整数寄存器（integer registers），共十六类（个）寄存器

%r--：64 位版本，%e--：32 位版本，%--：16 位版本。e 表示 extended（相对于 16 位版本），r 表示 register.

注：以下表格在《计算机系统：基于 x86+Linux 平台》P89 页中有整合

x86-64 integer registers 注意，32 位版本就是 64 位版本的截断，实际上是共的一个寄存器。

| 64 bit | 32 bit | 64 bit | 32 bit  |
| ------ | ------ | ------ | ------- |
| `%rax` | `%eax` | `%r8`  | `%r8d`  |
| `%rcx` | `%ecx` | `%r9`  | `%r9d`  |
| `%rdx` | `%edx` | `%r10` | `%r10d` |
| `%rbx` | `%ebx` | `%r11` | `%r11d` |
| `%rsi` | `%esi` | `%r12` | `%r12d` |
| `%rdi` | `%edi` | `%r13` | `%r13d` |
| `%rsp` | `%esp` | `%r14` | `%r14d` |
| `%rbp` | `%ebp` | `%r15` | `%r15d` |

IA32 registers 注意，16 位版本就是 32 位版本的截断，实际上是共的一个寄存器，8 位的两个 high-low 的寄存器就对应 16 位版本的位置，还是共的一个寄存器。

| 32 bit | 16 bit | 8 bit        |
| ------ | ------ | ------------ |
| `%eax` | `%ax`  | `%ah`、`%al` |
| `%ecx` | `%cx`  | `%ch`、`%cl` |
| `%edx` | `%dx`  | `%dh`、`%dl` |
| `%ebx` | `%bx`  | `%bh`、`%bl` |
| `%esi` | `%si`  |              |
| `%edi` | `%di`  |              |
| `%esp` | `%sp`  |              |
| `%ebp` | `%bp`  |              |

特殊用途的寄存器：`%-sp` 称为栈指针 ：stack pointer；`%-bp` 称为基指针：base pointer，也有特殊用途，但是现在通常不使用它了。

操作数（operand）。操作数有三种来源：立即数（immediate）、寄存器（register）、内存（memory）。

比如说，mov 指令是将源复制，然后赋值到某地。`movq` 指令给出五种方式：

| direction  | assembly (e.g.)     | C analog (e.g.)  |
| ---------- | ------------------- | ---------------- |
| Imm -> Reg | `movq $0x4,%rax`    | `temp = 0x4;`    |
| Imm -> Mem | `movq $-147,(%rax)` | `*p = -147;`     |
| Reg -> Reg | `movq %rax,%rdx`    | `temp2 = temp1;` |
| Reg -> Mem | `movq %rax,(%rdx)`  | `*p = temp;`     |
| Mem -> Reg | `movq (%rax),%rdx`  | `temp = *p`      |

这是容易理解的：赋值给立即数这样一个常数没有意义，另外内存到内存出于硬件设计目的被禁止了。

说明：

​	`(R)` 表示使用这个寄存器，按照地址在内存中寻找，即 `Mem[Reg[R]]`.

​	`D(R)` 表示使用的同时进行一些计算，即 `Mem[Reg[R]+D]`. 其中 D 的意思是 displacement 偏移。

​	Intel 格式中：o 指的是 oct word，代表八字（128 位）；q 指的是 quad word，代表四字（64 位）；l 指代 long word，代表长字（双字，32 位）；w 指代 word，代表字（16 位）；b 指代 byte，代表字节（8 位）。

​	更一般的寻址方式：`D(Rb,Ri,S)`，其中 `Rb` 表示基址寄存器（base register），`Ri` 表示索引（index register），`S` 表示尺度（scale），`D` 还是偏移，它指的是 `Mem[Reg[Rb]+S*Reg[Ri]+D]`. 其中集中特殊情况要么在格式上直接省略了一些参数，分别写为：`(Rb,Ri)`、`D(Rb,Ri)`、`(Rb,Ri,S)`；或者在填写处流空，例如 `0x80(,%rdx,2)`.

## Part 4

lea 指令：load effective address，和 mov 指令的区别在于赋值的是地址而不是实际值，这个指令是用来计算地址的，与 C 语言代码的对应中有时出现取地址符 `&`，用处有两种：

	1. 计算地址而不用取引用，例如 `p = &x[i];` （初始目的）
	1. 进行 `x+k*y` 的数值计算，其中 `k` 为 1, 2, 4, 8. （借用计算形式，普通调用乘法太慢）

```c
long m12(long x) {
    return x*12;
}
```

```assembly
leaq (%rdi,%rdi,2), %rax # t <- x+x*2
salq $2, %rax            # return t<<2
```

一些算术操作：

```
二元：
add   加
sub   减
imul  立即数乘法
sal   左移，等同于 shl
sar   算术右移
shr   逻辑右移
xor   按位异或
and   按位与
or    按位或
instruction source, destination
instr src, dest # dest = dest op src
一元：
inc   自加    dest <- dest + 1
dec   自减    dest <- dest - 1
neg   取负    dest <- -dest
not   按位取反 dest <- ~dest
```

## Summary (official)

- History of Intel processors and architectures
  - Evolutionary design leads to many quirks and artifacts

- C, assembly, machine code
  - New forms of visible state: program counter, registers, ...
  - Compiler must transform statements, expressions, procedures into low-level instructions sequences

- Assembly Basics: Registers. operands. move
  - The x86-64 move instructions cover wide range of data movement forms

- Arithmetic
  - C compiler will figure out different instructions combinations to carry out computation















