## RISC-V Micro OS

从零实现的 RISC-V 32 位小型操作系统，使用 C 语言编写，覆盖启动、异常处理、分页、进程切换、系统调用和块设备文件读写等核心机制。以 QEMU virt 机器为运行环境。

### 功能特性

- **裸机启动**：自定义链接脚本，设置栈，清零 BSS，通过 SBI 输出控制台信息
- **异常与系统调用**：寄存器上下文保存/恢复，实现用户态 ↔ 内核态的特权级切换
- **内存管理**：基于 Sv32 页表映射，隔离内核空间与用户程序空间
- **进程模型**：简单的进程控制块（PCB），支持上下文切换和协作式调度
- **文件系统**：通过 virtio‑blk 读取 tar 格式镜像，提供简化的文件读写接口
- **用户态 Shell**：内置 `hello`、`readfile`、`writefile`、`exit` 等命令

### 构建与运行

#### 依赖

- RISC-V GCC 工具链（`riscv64-unknown-elf-*` 或 `riscv64-linux-gnu-*`）
- QEMU（`qemu-system-riscv32`）
- LLVM OBJCOPY（或对应工具链中的 objcopy）

视工具链情况，可能需要调整 `run.sh` 中的 `OBJCOPY` 路径。

#### 运行

```sh
./run.sh
```

启动后可在 QEMU 串口中输入命令：

```text
> hello
> readfile
> writefile
> exit
```