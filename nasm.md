# nasm



*.text*  contains the executable code.  execution starts in NASM program. like main()function

*.bss* used to declare variables without initialization

*.data* used to declare and initialize the variables in the program

```assembly
section .data
	var1: db 10
	str1: db "Hello World!"
	
section .bss
	var3: resb 1
	var4: resq 1;
```

* RESx directive is used to reserve just space in memory for a variable without giving any initial values
* Dx directive is used for declaring space in the memory for any variable and also providing the initial values at that moment

| x    | Meaning     | No:of Bytes |
| ---- | ----------- | ----------- |
| b    | BYTE        | 1           |
| w    | WORD        | 2           |
| d    | DOUBLE WORD | 4           |
| q    | QUAD WORD   | 8           |
| t    | TEN WORD    | 20          |
|      |             |             |

```assembly
var : db 10,5,8,9
string: db "Hello"
string2: db "H","e","l","l","o"
Reserves 4 bytes in memory for var and stores the values 10, 5, 8, 9 respectively in that 

```



[] 之前可以有BYTE,WORD,DWORD,QWORD,TWORD

```assembly
mov dword[ebx],1
inc byte[label]
add eax,dword[label]

mov eax,[label];value stored in the address location will be copied to eax
mov ebx,label; the address location will be copied to ebx reg
```

* mov
* movzx 无符号扩展
* add
* sub
* mul
* div



```assembly
mov eax,ebx; copy the content of ebx to eax
mov ecx,109
mov al,bl
mov byte[var1],al; copy the content of al reg to the variable var in memory

```



```assembly
add eax,ecx; eax = eax + ecx
add al, ah; al = al + ah;
sub eax,ecx; eax = eax - ecx 
```



mul src

If src is 1 byte then AX = AL * src

• If src is 1 word (2 bytes) then DX:AX = AX * src

Upper 16 bits of the result will go to DX

and the lower 16 bits will go to AX)

 If src
is 2 words long(32 bit) then EDX:EAX = EAX * src
Upper 32 bits of the result will

go to EDX and the lower 32 bits will go to EAX) 



div src 

•If src is 1 byte then AX will be divide by src, remainder will go to AH and quotient will go to AL 

•If src is 1 word (2 bytes) then DX:AX will be divide by src, remainder will go to DX
and quotient will go to AX 

•If src is 2 words long(32 bit) then EDX:EAX will be divide by src, remainder will go to EDX and quotient will go to EAX 



条件分支指令

* JMP
* CMP



label: 

​	JMP label



​	JMP exit



exit:





CMP op1,op2;

affect the CPU FLAGS

| Instruction | Working                      |
| ----------- | ---------------------------- |
| JZ          | jump if zero flag is set     |
| JNZ         | jump if zero flag is unset   |
| JC          | Carry flag is set            |
| JNC         |                              |
| JP          | Parity Flag is Set(奇偶标志) |
| JNP         |                              |
| JO          | overflow flag is Set         |
| JNO         |                              |

| instruction   | working    |
| ------------- | ---------- |
| JE            | op1==op2   |
| JNE           | op1 != op2 |
| JA (if above) | op1 > op2  |
| JNA           | op1 <= op2 |
| JB（if below) | op1 < op2  |
| JNB           | op1 >= op2 |
| JG (Greater)  |            |
| JL(Less)      |            |
|               |            |

loop

通过jmp 条件跳转

位运算

* AND  	`AND op1,op2 ; op1 = op1 and op2`
* OR
* XOR
* NOT
* TEST
* SHL  shift left左移 op2 must be immediate value
* SHR
* ROL 循环左移
* ROR
* RCL
* RCR



栈操作

* push 
* pop
* pusha
* popa

pusha,popa 用于将所有通用寄存器压栈出栈，当你使用函数调用





push ; push decreases the value of ESP and copies the value of a reg/constant into the system stack

push ax; esp -2

push eax; esp - 4



pop bx; esp = esp + 2

pop ebx ; esp = esp + 4



系统调用

mov eax, 1; system call number

mov ebx, 0; parameter

int 80h; triggering OS interrupt

将系统调用号放在eax寄存器里然后参数放在其他通用寄存器里，然后使用int指令



**Write System Call**

```assembly
mov eax,4; system call number
 
mov ebx,1; standard output device

mov ecx,msg1; pointer to outputstring
 
mov edx,size1; number of characters

int 80h;triggering interrupt


```

**Read System Call**

```assembly
mov eax,3 ; system call number for read
mov ebx,0 ; source keyboard
mov ecx,var; pointer to memory location
mov edx,dword[size]; size of the string
int 80h ; triggering OS interrupt
```



## 8086/8088寻址方式和指令系统

* 立即寻址

mov ax,1234H

* 寄存器寻址

mov si,ax

mov al,dh

* 直接寻址

mov ax,[1234H]

mov es:[5678H],BL

* 寄存器间接寻址

  mov ax,[si]

* 寄存器相对寻址

mov ax,[dl+1223H]

mov ax,[si+3]

mov ax,3[si]

* 基址加变址寻址

;ds = 5000h,bx=1223h,di=54h

mov ax,[bx+di]

mov ax,es:[bx+si]



mov ax,[bx+di]

mov ax, \[di ][bx]

* 相对地址加变址寻址



ax累加寄存器 用于运算 I/0指令使用该寄存器传递数据

bx基址寄存器，地址索引 存储器指针

cx 计数寄存器 计数 保存计算值

dx 数据寄存器 数据传递

16位



sp

bp

si

di



mov dst,src

lea地址传送 lea reg,oprd把操作数oprd的有效地址传送到操作数REG

操作数oprd必须是一个存储器操作数

lea ax,buffer;buffer变量名

lea dx,[bx+3]

lea si,[bp+di+4]

push src

pop dst



主程序和子程序参数传递

* 利用寄存器传送 参数放到约定的寄存器 寄存器个数有限 传递参数较少的情况
* 约定的内存变量来传递参数
* 利用堆栈
* 利用call后续区



#GDT (Global Descriptor Table)



intel 8086. 16位CPU 16位寄存器 16位数据总线 20位地址总线 1MB的寻址能力，一个地址由段和偏移两部分组成

物理地址 （Physical Address) = 段值 Segment * 16 + 偏移 Offset

通过改变段寄存器的值，可以随心所欲访问内存任何一个单元，而丝毫不受限制

实模式下，段值是地址的一部分，段值为xxxxh表示以xxxx0h开始的一段内存，而保护模式下，虽然段值仍然由原来16位的cs,ds等寄存器表示，但是此时16位的cs,ds仅仅变成了一个索引，这个索引指向了一个数据结构的一个表项，表项中详细定义了段的起始地址、界限、属性等内容。数据结构就是GDT(还可能是LDT) GDT中表项专门的名字，描述符Descriptor

GDT 提供段式存储机制，这种机制是通过段寄存器和GDT中的描述符共同提供的。



保护模式

当一条访问内存指令发出一个内存地址时，cpu的如何归纳出应该放在数据总址的地址

1. 根据指令的性质来确定使用哪个段寄存器，例如 取数据的指令中的地址在数据段
2. 根据段寄存器的内容，找到相应的描述符
3. 从描述符中得到基地址
4. 将指令中发出的地址作为位移，与描述符中界限相比，是否越界
5. 将指令的性质与描述符中的访问权限来确定是否越权 
6. 将指令中发出的地址作为位移，与基地址相加得出实际的“物理地址”



GDT，Global Descriptor Table, 存放Descriptor的表，可在全局内访问，所有进程想要访问全局可见的段时，从GDT查询，有且只有一个，进程从GDTR寄存器中获得GDT的位置

LDT(Local)与GDT相同，但是不是全局的，对于某个进程，只知道自己的LDT,访问自己的段时从LDT差询，进程从LDTR寄存器中获得LDT的位置，向它发起查询。



Descriptor

保护模式下引入描述符描述各种数据段，描述符均为8字节（0-7）由第5个字节说明描述符的类型，类型不同，描述符的结构也略有不同。

若干个描述符集中在一起组成描述符表，而描述符表本身也是一种数据段，也使用描述符进行描述，而描述符表本身也是一种数据段，也使用描述符进行描述。从现在起，“地址转换”由描述符表来完成。  In this sense,描述符表是一张地址转换函数表。

 

Selector 选择子

```assembly
mov ax,SelectorVideo
mov gs,ax
```

如何通过段寄存器找到对应的描述符

段寄存器gs的值变成了SelectorVideo



选择子，2字节的数，16位，最低2位表示RPL(请求特权等级)，第三位表示查表是利用GDT还是LDT进行，最高十三位给出了所需的描述符在描述符表中的地址。13位正好足够寻址8K项。

各段寄存器仍然给出一个段值，只是这个假段值到真正的段地址的转换不再是左移4位而是利用描述符表完成。



GDTR

表示GDT在内存中的段地址和段限（表大小），GDTR48位寄存器，32位表示短地址，16位表示段限，最大64k，每个描述符8字节，故最多有64k/8=8k个描述符。

selctor的高13位表示的就是描述符中的位置

LDT

LDTR用于表示LDT在内存中的位置，但是因为LDT本身也是一种数据段，它必须有一个描述符，且该描述符必须放在GDT中，因此LDTR使用了ds,es,cs等相同的机制，其中只存放一个选择子，通过查GDT表获得LDT的真正内存地址



除了选择子的Bit3一个为0一个为1用于区分该描述符是在GDT中还是在LDT中外，描述符本身的结构完全一样。

* 为啥LDT是在GDT中而不是一个专门的寄存器。
  * GDT表只有一个，是固定的。而LDT表每个任务就可以有一个。因此有多个，并且由于任务的个数在不断变化其数量也不断变化
  * 如果只有一个LDTR寄存器，显然不能满足多个LDT的要求。



引申 IDT （中断描述符表

80x86系列中，为中断服务提供中断/陷阱描述符，这些描述符构成了中断描述符表（IDT)，并引入一个48位的全地址寄存器。理论上IDT表可以有8k项，可是因为80k86只支持256个中断，idt实际上也只有256项



# FAT12 文件系统

文件系统

* 存储和组织计算机数据的方法
* 逻辑层 不关心用于存储文件的各个数据块的物理位置 而总是将这些数据块抽象为一个线性的、可以随机访问的、从0开始计数的数组。
  * FAT12 为例，1.44M软盘的2880个扇区虽然分布在不同的盘面和磁道上，但是FAT12文件系统只是将这些物理扇区抽象为编号从0到2879的逻辑扇区。
* 划分磁盘为若干层次以方便管理和组织
* 扇区 sector 磁盘上的最小数据单元 包含 512字节
* 簇 cluster 数据区中存储文件数据的基本单位， 包含一个或多个扇区。簇包含的扇区数总量是2的乘法
* 分区 partition 整个文件系统



FAT文件系统

* dos/Windows系列系统中常用的文件系统总称
* FAT12 最古老 采用12位文件分配表
* 仍用于软盘驱动器



数据区 长度非固定 	2879

根目录 长度非固定 需计算

FAT2  10-18

FAT1	2-9

引导扇区0-1

引导扇区的格式

| 名称           | 偏移 | 长度 | 内容                 | Orange's的值 |
| -------------- | ---- | ---- | -------------------- | ------------ |
| BPB_BytsPerSec | 11   | 2    | 每扇区字节数         | 0x200(512)   |
| BPB_SecPerClus | 13   | 1    | 每簇扇区数           | 0x1(16)      |
| BPB_RsvdSecCnt | 14   | 2    | Boot记录占用多少扇区 | 0x1          |
| BPB_BumFATs    | 16   | 1    | 共有多少PAT表        | 0x2          |
| BPB_RootEntCnt | 17   | 2    | 根目录文件数最大值   | 0xE0(224)    |
| BPB_TotSec16   | 19   | 2    | 扇区总数             | 0xB49(2880)  |
| BPB_FATSz16    | 22   | 2    | 每FAT扇区数          | 0x9          |
|                |      |      |                      |              |

根目录区

* 根目录区从第19扇区开始，所以第一字节位于偏移19*512=9728=0x2600处
* 根目录区中每一个条目为32字节，所以根目录为BPB_RootEntCnt根目录最大数 * 32字节

cont.

根目录区中的条目格式

| 名称         | 偏移 | 长度 | 描述                     |
| ------------ | ---- | ---- | ------------------------ |
| DIR_Name     | 0    | 0xB  | 文件名8字节，扩展名3字节 |
| DIR_Attr     | 0xB  | 1    | 文件属性                 |
| 保留位       | 0xC  | 10   | 保留位                   |
| DIR_WriTime  | 0x16 | 2    | 最后一次写入时间         |
| DIR_WriData  | 0x18 | 2    | 最后一次写入日期         |
| DIR_FstClus  | 0x1A | 2    | 对应条目的开始簇号       |
| DIR_FileSize | 0x1c | 4    | 文件大小                 |
|              |      |      |                          |



FAT项的值代表文件下一个簇号



数据区

* 数据区开始扇区号=根目录开始扇区号+根目录所占扇区数
* 若为目录，则格式与根目录项的格式一样



FAT（File Allocation Table）文件分配表

* FAT有两个 FAT2是FAT1的备份
* 文件分配表被划分为紧密排列的若干个表项，每个表项都与数据区中的一个簇相对应，而且表项的序号和簇号也是一一对应的
* 每12位成为一个FAT项（FATEntry），代表一个簇，所以2个FAT项会占用3个字节
* 在1.44M软盘上，FAT前三个字节的值必须是固定的，分别是0xF0,0xFF,0xFF,用于表示这是一个应用在1.44m软盘上的FAT12文件系统，本来序号为0,1的FAT表项应该对应于簇0和簇1，但是由于这两个表项被设置成了固定值，簇0 和簇1 就没有存在的意义了，所以数据区就起始于簇2。
* FAT项的值代表文件的下一个簇号
  * 值大于或等于0xFF8,表示当前簇已经是本文件的最后一个簇
  * 值为0xFF7表示是一个坏簇








BPB BIOS Parameter Block

以BPS_开头的域属于BPB，以BS\_ 开头的域不属于BPB，只是引导扇区的一部分（Boot Sector)

FAT 占用9个扇区，第二个FAT后面是根目录的第一个扇区，根目录后面是数据区



BPB_RootEntCnt 根目录文件最大值

根目录由目录条组成（Directory Entry),条目最多有BPB_RootEntCnt个

每一个条目占用32字节

