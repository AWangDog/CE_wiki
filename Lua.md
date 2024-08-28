# Lua
Cheat Engine 带有一组广泛的 Lua 函数，您可以在ct表、ce和独立脚本中使用。
## 1.变量
### 全局变量
+ [TrainerOrigin](https://github.com/AWangDog/CE_wiki/blob/main/lua:TrainerOrigin.md)：一个变量，其中包含启动作弊引擎的 trainer 的路径（仅在作为 trainer 启动时设置）
+ process：一个变量，其中包含当前打开的进程的主 modulename
+ MainForm：主要的作弊引擎 gui
+ AddressList：作弊引擎主界面的地址列表
### 变量
+ 寄存器
  + EFLAGS
  + 32/64-bit: EAX, EBX, ECX, EDX, EDI, ESI, EBP, ESP, EIP
  + 64-bit only: RAX, RBX, RCX, RDX, RDI, RSI, RBP, RSP, RIP, R8, R9, R10, R11, R12, R13, R14, R15 : The value of the register
