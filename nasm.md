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