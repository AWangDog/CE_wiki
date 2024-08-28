# Lua
Cheat Engine 带有一组广泛的 Lua 函数，您可以在ct表、ce和独立脚本中使用。
## 变量
### 全局变量
+ [TrainerOrigin](https://github.com/AWangDog/CE_wiki/blob/main/Lua%3ATrainerOrigin.md)：一个变量，其中包含启动作弊引擎的 trainer 的路径（仅在作为 trainer 启动时设置）
+ process：一个变量，其中包含当前打开的进程的主 modulename
+ MainForm：主要的作弊引擎 gui
+ AddressList：作弊引擎主界面的地址列表
### 变量
+ 寄存器
  + EFLAGS
  + 32/64-bit: EAX, EBX, ECX, EDX, EDI, ESI, EBP, ESP, EIP
  + 64-bit only: RAX, RBX, RCX, RDX, RDI, RSI, RBP, RSP, RIP, R8, R9, R10, R11, R12, R13, R14, R15 : The value of the register
## 函数
### ct表
这些功能有助于管理作弊ct表。
+ getAddressList：返回作弊表 Addresslist 对象
+ findTableFile：返回存储在作弊表中的 TableFile
+ createTableFile：将新文件添加到备忘单
+ loadTable：加载 “.ct” 或 “.cetrainer” 文件或流
+ saveTable：保存当前表
### 修改器
+ registerEXETrainerFeature：向exe修改器的生成器窗口添加新功能，并在用户构建.exe修改器时调用您的函数
+ unregisterEXETrainerFeature：取消注册修改器功能
### 保护
+ activateProtection：阻止基本内存扫描程序打开作弊引擎进程
+ enableDRM：阻止普通内存扫描程序读取作弊引擎进程 （kernelmode）
+ encodeFunction：将给定函数转换为编码字符串，您可以将其传递给 decodeFunction
+ decodeFunction：将编码字符串转换回函数
### 扫描
这些功能控制作弊引擎的扫描。
+ AOBScan：扫描当前打开的进程，并返回包含所有结果的 StringList 对象
+ getCurrentMemscan：将当前活动的扫描会话作为 MemScan 对象返回
### 进程
+ createProcess：创建带或不带调试的进程
+ openProcess：使作弊引擎打开给定的 processname 或 id
+ onOpenProcess：由 CE 在打开进程时调用（用户定义）
+ getForegroundProcess：返回当前位于顶部的进程的进程 ID
+ getOpenedProcessID：返回当前打开的进程
+ getProcessIDFromProcessName：返回 processid
+ openFileAsProcess：使作弊引擎以内存访问权限打开文件，就像它是一个进程一样
+ saveOpenedFile：保存已打开文件的更改
+ setPointerSize：设置作弊引擎将处理指针的大小（以字节为单位）。（某些 64 位进程只能使用 32 位地址）
+ setAssemblerMode：设置汇编器的位大小模式（0=32 位，1=64 位）
+ getProcesslist：返回系统的 processlist
+ getWindowlist：返回系统的 top-window 列表
+ pause：暂停当前打开的进程
+ unpause：恢复当前打开的进程
+ targetIs64Bit：如果目标进程为 64 位，则返回 true，如果目标进程为 32 位，则返回 false
+ enumModules：返回一个表，其中包含有关当前进程中每个模块的信息或指定的进程 ID
+ closeRemoteHandle：关闭进程的句柄
### 线程
+ getCPUCount：返回 CPU 的
+ getThreadlist：使用当前打开的进程的 threadlist 填充 List 对象
+ inMainThread：如果当前代码在主线程内运行 （6.4+），则返回 true
+ synchronize：从主线程调用给定的函数。返回给定函数的返回值
+ queue：从主线程调用给定的函数。不等待结果
+ checkSynchronize：使用线程和 synchronize 调用时，从主线程中的无限循环调用此函数
### 句柄
+ getHandleList：返回包含系统中所有句柄的表
### 地址
这些函数有助于在内存地址和符号/CEAddressStrings 之间进行转换。
+ getAddress：返回 symbol 的地址。可以是 modulename 或 export
+ getAddressSafe：返回元件的地址，如果未找到，则返回 nil。类似于 errorOnLookup 为 false 时的 getAddress，但返回 nil
+ getNameFromAddress：以字符串形式返回给定地址，如果可能，则返回元件表示形式
+ registerSymbol：将指定的 symbolname 分配给地址
+ unregisterSymbol：从地址中删除名称
+ getSymbolInfo：返回由 SymbolList 类对象定义的表（模块名称、搜索键、地址、大小）
+ reinitializeSymbolhandler：重新初始化 symbolhandler。例如，当新模块已加载时
+ inModule：如果给定地址位于模块内，则返回 true
+ inSystemModule：如果给定地址位于系统模块内，则返回 true
+ getModuleSize：返回给定模块的大小（使用 getAddress 获取基址）
+ errorOnLookupFailure：设置地址查找是会引发错误，还是只返回 0。
+ registerSymbolLookupCallback：注册一个函数，以便在解析元件时调用
+ unregisterSymbolLookupCallback：删除回调
+ registerAddressLookupCallback：注册请求地址名称时要调用的函数
+ unregisterAddressLookupCallback：删除回调
+ reinitializeDotNetSymbolhandler：仅重新初始化元件列表的 DotNet 部分
### 内存
+ allocateMemory：为目标进程分配一些内存
+ deAlloc：释放分配的内存
+ allocateSharedMemory：创建给定大小的共享内存对象（如果尚不存在）
+ createSection：在内存中创建一个 'section'
+ mapViewOfSection：将部分映射到内存
+ unMapViewOfSection：从内存中取消映射部分
+ copyMemory：将内存从给定地址复制到目标地址
+ allocateKernelMemory：分配一个非分页内存块并返回地址
+ freeKernelMemory：释放给定的内存区域
+ mapMemory：将特定地址映射到从给定 PID 到给定 PID 的 usermode 上下文
+ unmapMemory：
+ createMemoryStream：

这些函数从打开的进程中读/写内存。
#### 读
+ readBytes：返回给定地址处的字节。如果 ReturnAsTable 为 true，它将返回一个表而不是多个字节
+ readSmallInteger：从指定地址读取 16 位整数。
+ readInteger：从指定地址读取 32 位整数。
+ readQword：从指定地址读取 64 位整数。
+ readPointer：在 64 位目标中，这等于 readQword，在 32 位目标 readInteger（） 中。
+ readFloat：从指定地址读取单个精度浮点值
+ readDouble：从指定地址读取双精度浮点值
+ readString：从内存中读取字符串，直到它命中 0 终止符。maxlength 只是为了让您不会冻结太久
+ readRegionFromFile：将给定文件写入特定地址
+ readBytesLocal：参见 readBytes，但随后它是针对作弊引擎的内存的
+ readSmallIntegerLocal：从 CE 内存中的指定地址读取 16 位整数
+ readIntegerLocal：从 CE 内存中的指定地址读取 32 位整数
+ readQwordLocal：从 CE 内存中的指定地址读取 64 位整数
+ readPointerLocal：ReadQwordLocal/ReadIntegerLocal，具体取决于作弊引擎版本
+ readFloatLocal：从 CE 内存中的指定地址读取单个精度浮点值
+ readDoubleLocal：从 CE 内存中的指定地址读取双精度浮点值
+ readStringLocal：从 CE 的内存中读取字符串，直到它达到 0 终止符
#### 写
+ writeBytes：将给定字节从表中写入给定地址
+ writeSmallInteger：将 16 位整数写入指定地址。成功时返回 true。
+ writeInteger：将 32 位整数写入指定地址。成功时返回 true。
+ writeQword：将 64 位整数写入指定地址。成功时返回 true。
+ writeFloat：将单精度浮点数写入指定地址。成功时返回 true。
+ writeDouble：将双精度浮点写入指定地址。成功时返回 true。
+ writeString：将字符串写入指定地址。成功时返回 true。
+ writeRegionToFile：将给定区域写入文件。返回写入的字节数。
+ writeSmallIntegerLocal：将 16 位整数写入 CE 内存中的指定地址。成功时返回 true
+ writeIntegerLocal：将 32 位整数写入 CE 内存中的指定地址。成功时返回 true
+ writeQwordLocal：将 64 位整数写入 CE 内存中的指定地址。成功时返回 true
+ writeFloatLocal：将单精度浮点写入 CE 内存中的指定地址。成功时返回 true
+ writeDoubleLocal：将双精度浮点写入 CE 内存中的指定地址。成功时返回 true
+ writeStringLocal：将字符串写入指定地址。成功时返回 true。
+ writeBytesLocal：参见 writeBytes，但随后它是针对作弊引擎的内存的
  + readSmallInteger、readInteger、readSmallIntegerLocal、readIntegerLocal 也可以有第二个布尔参数。如果为 true，则 value 将被签名。
### 转换
+ ansiToUtf8：将 ANSI 编码的字符串转换为 UTF8
+ utf8ToAnsi：将 UTF8 编码的字符串转换为 ANSI
+ stringToMD5String：从提供的字符串返回 MD5 哈希字符串
+ integerToUserData：将给定的整数转换为 userdata 变量
+ userDataToInteger：将给定的 userdata 变量转换为整数
#### 到字节表
+ wordToByteTable：将 word 转换为 bytetable
+ dwordToByteTable：将 dword 转换为 bytetable
+ qwordToByteTable：将 qword 转换为 bytetable
+ floatToByteTable：将 float 转换为 bytetable
+ doubleToByteTable：将 double 转换为 bytetable
+ stringToByteTable：将 string 转换为 bytetable
+ wideStringToByteTable：将 string 转换为 widestring 并将其转换为 bytetable
#### 从字节表
+ byteTableToWord：将 bytetable 转换为 word
+ byteTableToDword：将 bytetable 转换为 dword
+ byteTableToQword：将 bytetable 转换为 qword
+ byteTableToFloat：将 bytetable 转换为 float
+ byteTableToDouble：将 bytetable 转换为 double
+ byteTableToString：将 bytetable 转换为 string
+ byteTableToWideString：将 bytetable 转换为 widestring 并将其转换为 string
#### 二进制
+ bOr：二进制或
+ bXor：二进制异或
+ bAnd：二进制与
+ bShl：二进制逻辑左移
+ bShr：二进制逻辑右移
+ bNot：二进制非
### 设备输入
这些函数获取/设置键盘/鼠标输入。
+ getMousePos：返回鼠标的 X 和 Y 坐标
+ setMousePos： 设置鼠标位置
+ isKeyPressed：如果当前按下指定的键，则返回 true
+ keyDown：使 key 进入 down 状态
+ keyUp：使 key 上升
+ doKeyPress：模拟按键
+ mouse_event：Windows 的 API [mouse_event](https://msdn.microsoft.com/zh-cn/library/windows/desktop/ms646260(v=vs.85).aspx)。
+ setGlobalKeyPollInterval：设置全局 keypoll 间隔
+ setGlobalDelayBetweenHotkeyActivation： 设置同一 hotey 激活之间的最小延迟（以毫秒为单位）
