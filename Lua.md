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
#### 手柄
+ getXBox360ControllerState：获取连接的 XBox 控制器的状态
+ setXBox360ControllerVibration：设置控制器内部左右振动马达的速度
#### 剪切板
+ writeToClipboard：将给定的文本写入剪贴板
+ readFromClipboard：从剪贴板读取文本
### 屏幕
+ getScreenHeight：返回屏幕高度
+ getScreenWidth：返回屏幕宽度
+ getScreenDPI：返回屏幕 DPI
+ getWorkAreaHeight：返回工作区高度
+ getWorkAreaWidth：返回工作区宽度
+ getScreenCanvas：返回一个可用于写入屏幕的 Canvas 对象（注意：没有您想象的那么有用）
+ getPixel：返回特定屏幕坐标处像素的 RGB 值
### 声音
+ playSound：播放声音文件
+ beep：播放美妙的哔哔声/砰砰声！
+ speak：使用给定的标志朗读给定的文本[Microsoft Speech Platform SPEAKFLAGS](https://msdn.microsoft.com/zh-cn/library/speechplatform_speakflags.aspx)
+ speakEnglish：通过将给定文本包装到指定英语语音的 XML 语句中来尝试英语语音
#### XMPlayer
+ xmplayer_playXM：使用 xmplayer 播放给定的文件名
+ xmplayer_pause：暂停当前 xm 音频文件
+ xmplayer_resume：恢复当前 xm 音频文件
+ xmplayer_stop：停止当前的 xm 音频文件
+ xmplayer_isPlaying：如果当前正在播放 xm 音频文件，则返回 true
### 文本转语音
+ speak：朗读给定的文本。
+ speakEnglish：用英语语音说出给定的文本。
### 字体
+ loadFontFromStream：从内存流加载字体，并将 id（句柄）返回给字体，以便与 unloadLoadedFont 一起使用
+ unloadLoadedFont：从内存流中卸载字体
### Forms 和 Windows
+ findWindow：查找具有给定类名和/或 windowname 的窗口
+ getWindow：根据给定窗口获取特定窗口[MSDN getWindow](https://learn.microsoft.com/zh-cn/windows/win32/api/winuser/nf-winuser-getwindow)
+ getWindowCaption：返回窗口的标题
+ getWindowClassName：返回窗口的类名
+ getWindowProcessID：返回此窗口所属进程的 processid
+ getForegroundWindow：返回最顶层窗口的 windowhandle
+ sendMessage：向窗口发送消息
+ hookWndProc：hook窗口的 wndproc 过程
+ unhookWndProc：在完成 hookWndProc 的 hook 时调用
### Cheat Engine
这些功能有助于管理 Cheat Engine 本身。
+ getCEVersion：返回一个浮点值，该值指定作弊引擎的版本
+ getCheatEngineFileVersion：返回作弊引擎版本的完整版本数据。一个原始整数，以及一个包含 major、minor、release 和 build 的表
+ getFreezeTimer：返回负责冻结值的 Timer 对象
+ getUpdateTimer：返回负责更新值列表的 Timer 对象
+ getCommonModuleList：返回 commonModuleList StringList 对象
+ getCheatEngineProcessID：返回作弊引擎的 processid
+ cheatEngineIs64Bit：如果作弊引擎为 64 位，则返回 true，如果为 32 位，则返回 false
+ closeCE：关闭作弊引擎
+ getAutoAttachList：返回 AutoAttach StringList 对象
+ connectToCEServer：连接到给定的主机和端口。成功后，后续的大多数命令将由服务器处理
+ supportCheatEngine：将显示一个广告窗口，这将有助于保持 Cheat Engine 的开发。
+ fuckCheatEngine：如果广告窗口正在显示，则将其删除
+ getCheatEngineDir：返回 Cheat Engine（或 Trainer）所在的文件夹。
+ getComment：获取指定地址的用户自定义注释
+ setComment：在指定地址处设置用户定义的注释
+ getHeader：获取指定地址的 userdefined header
+ setHeader：在指定地址设置 userdefined header
+ registerBinUtil：向作弊引擎注册 binutils 工具集
+ reloadSettingsFromRegistry：这将导致作弊引擎从注册表重新加载设置并应用它们
+ loadPlugin：加载给定的插件
+ getSettings：返回一个 settings 对象
### Forms
+ getFormCount：返回分配给主 CE 应用程序的表单总数
+ getForm：返回特定索引处的表单
+ getMemoryViewForm：返回第一个 Memoryview 表单类对象
+ getMainForm：返回第一个 Mainform 类对象
+ getSettingsForm：返回主设置表单
+ getLuaEngine：返回 lua 引擎表单对象（如果需要，请创建它）
+ unhideMainCEwindow：显示主作弊引擎窗口
+ hideAllCEWindows：使所有常规作弊引擎窗口不可见（例如训练器表）
+ registerFormAddNotification：注册一个函数，当表单附加到作弊引擎的表单列表时要调用
+ unregisterFormAddNotification：取消注册 FormAddNotification 回调
### 消息
+ showMessage：显示包含给定文本的消息框
+ messageDialog：弹出一个消息框
+ outputDebugString：使用 Windows OutputDebugString 消息输出消息
+ processMessages：允许主事件处理程序处理新消息（允许新的按钮单击）
### 输入
+ inputQuery：显示一个对话框，用户可以在其中输入字符串。此函数返回给定的字符串，或在取消时返回 nil （CE6.4+）
### 快捷方式
+ shortCutToText：返回给定快捷方式值的文本表示形式 （整数） （6.4+）
+ textToShortCut：返回给定字符串表示的快捷方式整数。(6.4+)
+ convertKeyComboToString：返回给定键的字符串表示形式，就像热键处理程序一样
### 变速精灵
+ speedhack_setSpeed：如果速度黑客尚未激活，则启用它并设置给定的速度
+ speedhack_getSpeed：返回最后设置的速度
### Lua
这些功能有助于管理 Lua 本身。
+ resetLuaState：这将创建一个将使用的新 Lua 状态。
+ sleep：暂停指定的毫秒数
+ createRef： Integer - 返回可与 getRef 一起使用的整数引用
+ getRef：返回引用指出的任何内容
+ destroyRef：删除引用
### 类型
这些函数有助于将进程的内存构建为数据类型。
+ onAutoGuess：注册一个函数，每当使用 autoguess 预测变量类型时调用该函数。
+ registerCustomTypeLua：根据 Lua 函数注册自定义类型。
+ registerCustomTypeAutoAssembler：根据自动汇编器脚本注册自定义类型。
### Object-oriented
These functions determine how a Lua object fits in the class hierarchy.
+ inheritsFromObject: Returns true if given any class
+ inheritsFromComponent: Returns true if the given object inherits from the Component class
+ inheritsFromControl: Returns true if the given object inherits from the Control class
+ inheritsFromWinControl: Returns true if the given object inherits from the WinControl class
### Assembly
These functions help work with the x86 machine code as assembly.
+ autoAssemble: Runs the auto assembler with the given text
+ autoAssembleCheck: Checks the script for syntax errors. Returns true on succes, false with an error message on failure
+ disassemble: Disassembles the given address and returns a string in the format of "address - bytes - opcode extra"
+ splitDisassembledString: Returns 4 strings. The address, bytes, opcode and extra field
+ getInstructionSize: Returns the size of an instruction
+ getPreviousOpcode: Returns the address of the previous opcode (guess)
+ registerAssembler: Registers a function to be called when the single line assembler is invoked to convert an instruction to a list of bytes
+ unregisterAssembler: Unregisters the registered assembler
### Auto Assembler
+ registerAutoAssemblerCommand: Registers an auto assembler command to call the specified function
+ unregisterAutoAssemblerCommand: Unregisters an auto assembler command
+ registerAutoAssemblerPrologue: Registers a function to be called when the auto assembler is about to parse an auto assembler script
+ unregisterAutoAssemblerPrologue: Unregisters an auto assembler prologue
+ fullAccess: Changes the protection of a block of memory to writable and executable
#### Scripts
+ registerAutoAssemblerTemplate: Registers a template for the auto assembler
+ unregisterAutoAssemblerTemplate: Unregisters a template for the auto assembler
+ generateCodeInjectionScript: Adds a default code injection script to the given script
+ generateAOBInjectionScript: Adds an AOB injection script to the given script
+ generateFullInjectionScript: Adds a Full Injection script to the given script
+ generateAPIHookScript: Generates an auto assembler script which will hook the given address when executed
### Debugger
These functions manage the debugger. See Lua Debugging.
+ debug_isDebugging: Returns true if the debugger has been started
+ debug_getCurrentDebuggerInterface: Returns the current debuggerinterface used (1=windows, 2=VEH 3=Kernel, nil=no debugging active)
+ debug_canBreak: Returns true if there is a possibility the target can stop on a breakpoint. 6.4+
+ debug_isBroken: Returns true if the debugger is currently halted on a thread
+ debug_getBreakpointList: Returns a lua table containing all the breakpoint addresses
+ debugProcess: Debugs the currently attached process
+ debug_setBreakpoint: Sets a breakpoint of a specific size at the given address
+ debugger_onBreakpoint: Called by CE when a breakpoint hits (userdefined)
+ debug_removeBreakpoint: Removes a breakpoint
+ debug_continueFromBreakpoint: Continues the debugger when it's halted on a breakpoint
+ debug_setLastBranchRecording: Tells the kernelmode debugger to record the last few branches before the breakpoint got hit
+ debug_getMaxLastBranchRecord: Returns the maximum number of branch records this cpu supports
+ debug_getLastBranchRecord: Returns the value of the Last Branch Record at the given index (when handling a breakpoint)
+ debugger_onModuleLoad: Called by CE when the windows debugger interface loads a module (userdefined)
+ debug_getContext (since 6.5): Force-update the Lua variables representing the registers?
+ debug_setContext (since 6.5[1]): Force-update the registers to the Lua variables which represent them?
+ debug_updateGUI: Will refresh the userinterface to reflect the new context if the debugger was broken
+ detachIfPossible: Detaches the debugger from the target process (if it was attached)
+ debug_addThreadToNoBreakList: This will cause breakpoints on the provided thread to be ignored
+ debug_removeThreadFromNoBreakList: removed the threadid from the list
+ debug_getXMMPointer: Returns the address of the specified xmm register of the thread that is currently broken
+ debugger_onModuleLoad: This routine is called when a module is loaded. Only works for the windows debugger
### DBK
+ dbk_initialize: Loads the DBK driver into memory if possible
+ dbk_useKernelmodeOpenProcess: Switches the internal pointer of the OpenProcess api to dbk_OpenProcess
+ dbk_useKernelmodeProcessMemoryAccess: Switches the internal pointer to the ReadProcessMemory and WriteProcessMemory apis to dbk_ReadProcessMemory and dbk_WriteProcessMemory
+ dbk_useKernelmodeQueryMemoryRegions: Switches the internal pointer to the QueryVirtualMemory api to dbk_QueryVirtualMemory
+ dbk_getPEProcess: Returns the pointer of the EProcess structure of the selected processid
+ dbk_getPEThread: Gets the pointer to the EThread structure of a threadid
+ dbk_readMSR: Reads the msr using the dbk driver
+ dbk_writeMSR: Writes the msr using the dbk driver
+ dbk_executeKernelMemory: Executes a routine from kernelmode (e.g a routine written there with auto assembler)
+ dbk_getCR0: Returns Control Register 0
+ dbk_getCR3: Returns Control Register 3 of the currently opened process
+ dbk_getCR4: Returns Control Register 4
+ dbk_getPhysicalAddress: Returns the physical address of the given address
+ dbk_writesIgnoreWriteProtection: Set to true if you do not wish to initiate copy-on-write behaviour
### DBVM
+ dbvm_initialize: Initializes the dbvm functions
+ dbvm_addMemory: Adds memory to DBVM
+ dbvm_readMSR: Reads the msr using dbvm (bypasses the driver)
+ dbvm_writeMSR: Writes the msr using dbvm (bypasses the driver)
+ dbvm_getCR4: Returns the real Control Register 4 state
+ dbvm_readPhysicalMemory: Reads physical memory using DBVM
+ dbvm_writePhysicalMemory: Writes physical memory using DBVM
+ dbvm_watch_writes: Starts memory region write monitoring
+ dbvm_watch_reads: Starts memory region read monitoring
+ dbvm_watch_retrievelog: Receives the result of memory region monitoring
+ dbvm_watch_disable: Disables memory region monitoring
+ dbvm_cloak_activate: Cloak a page so changes to it will become invisible
+ dbvm_cloak_deactivate: Undo the cloak. Also undoes changes
+ dbvm_cloak_readOriginal: Read the memory that gets executed in a cloaked region
+ dbvm_cloak_writeOriginal: Writes the memory that gets executed in a cloaked region
+ dbvm_changeregonbp : Cloaks and sets a breakpoint at the given address and change registers when executed
+ dbvm_removechangeregonbp: Removes a change reg on bp breakpoint
+ dbvm_log_cr3_start : Start logging CR3 values
+ dbvm_log_cr3_stop : Stop logging CR3 values
+ dbvm_speedhack_setSpeed : sets the systemwide speedhack
+ dbvm_setTSCAdjust : Lets you specify what happens when a program tries to detect a virtual machine by calling rdtsc
### Translation
+ getTranslationFolder: Returns the path of the current translation files, empty if there is no translation going on
+ loadPOFile: Loads a ".PO" file used for translation
+ translate: Returns a translation of the string, returns the same string if it can't be found
+ translateID: Returns a translation of the string ID
### Files
+ getFileVersion: Returns the 64-bit file version,and a table that has split up the file version into major, minor, release and build
+ getFileList: Returns an indexed table with filenames
+ getDirectoryList: Returns an indexed table with directory names
### Structures
+ registerStructureDissectOverride: same as onAutoGuess, but is called by the structure dissect window when the user chooses to let cheat engine guess the structure for them
+ unregisterStructureDissectOverride: unregisters the structure dissect auto guess override
+ registerStructureNameLookup: Registers a function to be called when dissect data asks the user for the name of a new structure define
+ unregisterStructureNameLookup:
### Miscellaneous
+ injectDll: Injects a dll
+ shellExecute: Executes a given command
+ executeCode: Executes a stdcall function with 1 parameter at the given address in the target process and wait for it to return
+ executeCodeEx:
+ executeCodeLocal: Executes a stdcall function with 1 parameter at the given address in the target process
+ executeCodeLocalEx:
+ onAPIPointerChange: Registers a callback when an api pointer is changed
+ setAPIPointer: Sets the pointer of the given api to the given address
+ md5memory: Returns a md5 sum calculated from the provided memory
+ md5file: Returns a md5 sum calculated from the file
+ getSystemMetrics: Retrieves the specified system metric or system configuration setting msdn.microsoft.com/en-us/library/windows/desktop/ms724385.aspx
+ getTickCount: Returns the current tickcount since windows was started. Each tick is one millisecond
+ getUserRegistryEnvironmentVariable: Returns the environment variable stored in the user registry environment
+ setUserRegistryEnvironmentVariable: Sets the environment variable stored in the user registry environment
+ broadcastEnvironmentUpdate: Call this when you've changed the environment variables in the registry
+ getApplication: Returns the application object (the titlebar)
+ getInternet: Returns an internet class object. The string provided will be the name of the client provided
## Classes
Besides the above functions, Cheat Engine also implements some classes.
+ Addresslist: The addresslist class is a container for memory records
+ Bitmap: Bitmap based Graphic object
+ Brush: The brush class is part of the Canvas object. It's used to fill surfaces
+ Button: The button class is a visual component in the shape of a button.
+ ButtonControl: Common ancestor of several button like objects.
+ Canvas: The canvas class is a graphical class. It allows you do draw lines, pictures, and text on top of other object. Usually used in onPaint events and other graphical events
+ Calendar:
+ CEForm:
+ CheatComponent: The cheatcomponent class is the component used in Cheat Engine 5.x trainers
+ CheckBox: The Checkbox is a visual component that lets the user click it and change state between checked, unchecked, and if possible, grayed
+ Component : Base class for all components that need owner-owned functionality.
+ Control : Base class for visible controls.
+ Collection: The Collection class is an abstract class that the ListColumns class implements (And perhaps other classes as well)
+ CollectionItem: Basic object that is managed by a Collection class
+ ComboBox: The Combobox is like an edit field with a ListBox attached to it
+ CriticalSection:
+ CustomControl: Base class for windowed controls which paint themselves
+ CustomType: The custom type is an convertor of raw data, to a human readable interpretation.
+ D3DHOOK: The d3dhook functions provide a method to render graphics and text inside the game, as long as it is running in directx9, 10 or 11
+ D3DHook_FontMap: A fontmap is a texture that contains extra data regarding the characters
+ D3DHook_Texture: This class controls the texture in memory. Without a sprite to use it, it won't show
+ D3Dhook_TextContainer: A d3dhook_sprite class draws a piece of text on the screen based on the used fontmap
+ D3DHook_RenderObject: The renderobject is the abstract class used to control in what manner objects are rendered.
+ D3DHook_Sprite: A d3dhook_sprite class is a visible texture on the screen
+ Disassembler:
+ Disassemblerview: The visual disassembler used in the memory view window
+ DisassemblerviewLine:
+ DissectCode:
+ Edit: The Edit class is a visual component that lets the user type in data (Use control_getCaption to get the user input)
+ Event:
+ FileStream: The FileStream class is a Stream class that is linked to an open file on disk
+ FileDialog:
+ FindDialog:
+ Font: Class that defines a font
+ Form: Class that defines a window
+ FoundList: The foundlist is an companion class to MemScan. It opens the current memscan's result file and provides an interface for reading out the addresses
+ GenericHotkey: Lets you register hotkeys to Cheat Engine's internal hotkey handler
+ Graphic: Base class for dealing with Graphic images (Abstract)
+ GraphicControl: Class that supports simple lightweight controls that do not need the ability to accept keyboard input or contain other controls.
+ GroupBox: The groupbox class is like a Panel, but then has a header on top
+ Hexadecimal: The visual hexadecimal object used on the memory view window
+ Hexadecimalview: The visual hexadecimal object used on the memory view window
+ Icon:
+ Image: The Image class is a visual component that lets you show an image
+ Internet:
+ JpegImage:
+ Label: The Label class is a visual component that lets you display text
+ LuaPipe: Abstract class that LuaPipeServer and LuaPipeclient inherit from
+ LuaPipeClient: Class implementing a client that connects to a pipe
+ LuaPipeServer: Class launching the server side of a pipe
+ ListBox: The listbox class is a visual component with a list of selectable strings
+ ListColumn: The listcolumn class is an implemented CollectionItem class which is used by the ListColumns class of the listview class
+ ListColumns: The ListColumns class contains the Column class objects of a ListView object
+ ListItem: The ListItem class object is an entry in a ListView
+ ListItems: The listItems class is a container for the ListItem class objects of a Listview
+ Listview: The listview class lets you have a listbox like component with resizable columns
+ MainMenu: The menu at the top of a form
+ Memo: The Memo class is a multiline edit field
+ MemScan: The memscan class is the memory scanner of Cheat engine
+ Menu: Common Class ancestor for the MainMenu and PopupMenu classes
+ MenuItem: Holds the menuitems of a Menu, PopupMenu or even another MenuItem
+ MemoryRecord: The Memoryrecord class object describes a Cheat Table's Cheat Entry.
+ MemoryRecordHotkey: The memoryRecordHotkey class object is part of a MemoryRecord class. It's used as an interface to each individual hotkey inside a Cheat Table
+ MemoryStream: The memorystream class is a Stream class that is stored completely in memory. Because it's a stream there are multiple functions that can work with it
+ Memoryview: The memoryview class is the Memory view window of Cheat Engine. Use this as a basis to access the objects inside this window
+ MultiReadExclusiveWriteSynchronizer:
+ Object: Most basic class. All classes inherit from this class
+ PaintBox:
+ PageControl: This is an object that can hold multiple pages
+ Panel: The Panel class is like a form which can contain visual components.
+ Pen: The Pen class is part of the Canvas object. It's used to draw lines
+ Picture: Container for the Graphic class
+ PopupMenu: The menu that shows when rightclicking on an object
+ PortableNetworkGraphic:
+ ProgressBar: The progressbar class is a visual representation for a bar that can show the current progress on something
+ RadioGroup: The radiogroup is like a GroupBox but autopopulated using the Items(Strings object)
+ RasterImage: Base class for some graphical controls
+ RIPRelativeScanner:
+ OpenDialog: The OpenDialog class is used for selecting files to open.
+ SaveDialog: The SaveDialog class is based on the OpenDialog class but is used to select a file for saving
+ SelectDirectoryDialog:
+ Semaphore:
+ Settings: This class can be used to read out and set settings of cheat engine and of plugins, and store your own data
+ Splitter: The Splitter class is a visual component that lets the user re-size neighboring components)
+ Stringlist: Class that holds a list of strings
+ Strings: Abstract class that some text based classes make use of
+ StringStream:
+ Structure:
+ StructureElement:
+ StructureFrm:
+ structGroup:
+ SymbolList: This class can be used to look up an address to a symbolname, and a symbolname to an address
+ TabSheet: Part of a page control
+ TableFile: Tablefiles are files stored into a Cheat Table. You can access the data of such a file using this class
+ Thread:
+ Timer: The timer class is an non visual component that when active triggers an onTimer event every few milliseconds, based on the given interval
+ ToggleBox: The togglebox is like a button, but can stay down. Use with the checkbox methods
+ TrackBar: The trackbar class is a slider you can drag arround and read/set the state
+ TreeNode:
+ TreeNodes:
+ Treeview:
+ WinControl: Base class for controls which can contain other controls.
+ xmplayer:
### SQL Classes
+ CustomConnection:
+ Database:
+ SQLConnection:
+ SQLite3Connection:
+ ODBCConnection:
+ DBTransaction:
+ SQLTransaction:
+ Param:
+ Params:
+ Fields:
+ Dataset:
+ DBDataset:
+ CustomBufDataset:
+ CustomSQLQuery:
+ SQLQuery:
### Class Helper Functions
+ inheritsFromObject: Returns true if given any class
+ inheritsFromComponent: Returns true if the given object inherits from the Component class
+ inheritsFromControl: Returns true if the given object inherits from the Control class
+ inheritsFromWinControl: Returns true if the given object inherits from the WinControl class
+ createClass: Creates an object of the specified class (Assuming it's a registered class and has a default constructor)
+ createComponentClass: Creates an object of the specified component inherited class
### Undefined Class Property Functions
Not all properties of all classes have been explicitly exposed to lua, but if you know the name of a property of a specific class you can still access them (assuming they are declared as published in the pascal class declaration)
+ getPropertyList: Returns a StringList object containing all the published properties of the specified class
+ setProperty: Sets the value of a published property of a class (Won't work for method properties)
+ getProperty: Gets the value of a published property of a class (Won't work for method properties)
+ setMethodProperty: Sets the method property to the specific function
+ getMethodProperty: Returns a function you can use to call the original function
