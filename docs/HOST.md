# 本机配置与解锁测试记录

采集时间：2026-11-14 13:59（UTC+8）。数据来自本机 `nvidia-smi`、Windows 设备与注册表、U 盘 `H:\RTX3090-UNLOCK\RUN03\REPORT.TXT`，以及同一次开机内的 cuBLAS GEMM。

## 主机与操作系统

| 项目 | 值 |
|---|---|
| 操作系统 | Windows 11 Pro 25H2 |
| 版本 | 10.0.26200.9711（64 位） |
| 版本号 | DisplayVersion `25H2`，CurrentBuild `26200`，UBR `9711` |
| 安装类型 | Client，Professional |
| 安装时间 | 2026-07-23 15:03 |
| 本次开机 | 2026-11-14 13:47:51 |
| 系统目录 | `C:\WINDOWS\system32` |
| 区域 | Locale `0409`（en-US），代码页 1252，时区 UTC+8 |
| Secure Boot | 关闭 |
| HypervisorPresent | True |

| 项目 | 值 |
|---|---|
| 主板 | ASUS ROG STRIX Z790-H GAMING WIFI，Rev 1.xx |
| BIOS | American Megatrends `3107`，日期 2025-11-28 |
| 处理器 | Intel Core i9-13900K（Family 6 Model 183 Stepping 1） |
| 插槽 | LGA1700 |
| 核心 / 线程 | 24 核 / 32 线程 |
| WMI 基频 | 3000 MHz |
| 内存 | 64 GB 安装（金百达 2×32 GB，DDR5-6400）；Windows 可见 63.7 GiB |

## 显卡

| 项目 | 值 |
|---|---|
| 名称 | NVIDIA GeForce RTX 3090 |
| 品牌 / 架构 | GeForce / Ampere |
| 计算能力 | 8.6 |
| PCI | `0000:01:00.0` |
| 设备 ID | `0x2204`，厂商 `0x10DE`，修订 `A1` |
| 子系统 | `0x87AF1043`（华硕） |
| PnP | `PCI\VEN_10DE&DEV_2204&SUBSYS_87AF1043&REV_A1\4&256A0AA8&0&0008` |
| GPU 零件号 | `2204-300-A1` |
| UUID | `GPU-f4b50504-5a27-6081-b6b4-c6bcbf3e0755` |
| VBIOS | `94.02.42.00.a8` |
| Board ID | `0x100` |
| Inforom | `G001.0000.03.03` |
| 显存 | 24576 MiB，保留 254 MiB；采集时已用 0 MiB |
| BAR1 | 32768 MiB（Resizable BAR 已映射整段显存） |
| 最高时钟 | 核心 / SM 2130 MHz，显存 9751 MHz（GDDR6X，约 19.5 Gbps） |
| 采集时空闲时钟 | P8：核心 / SM 210 MHz，显存 405 MHz |
| 功耗上限 | 当前 390 W，默认 390 W，允许范围 100–480 W |
| 采集时功耗 / 温度 / 风扇 | 27.99 W，31 °C，风扇 0% |
| PCIe | 设备最高 Gen4 x16；采集时 Gen1 x16（空闲降速）；主板一侧最高 Gen5 |
| 驱动模型 | WDDM |
| 计算模式 | Default |
| 显示 | 未接显示器，Display Active = Disabled |
| ECC / MIG / 虚拟化 | 均不可用（N/A 或 None） |
| GSP 固件版本 | N/A |
| 设备状态 | OK |

`nvidia-smi` 的设备名、设备 ID 和 VBIOS 在解锁前后保持不变，不能用来判断本次开机是否已解锁。

## 驱动

| 项目 | 值 |
|---|---|
| KMD / nvidia-smi / NVML | 610.88 |
| Windows 驱动版本 | 32.0.16.1088 |
| 驱动日期 | 2026-07-22 |
| INF | `oem185.inf`，厂商 NVIDIA |
| `nvcuda.dll` | 32.0.16.1088，4,714,728 字节，2026-08-18 |
| `nvapi64.dll` | 32.0.16.1088，572,368 字节，2026-08-18 |
| CUDA UMD | 13.3 |
| 附带设备 | NVIDIA High Definition Audio 1.4.5.7；NVIDIA Virtual Audio Device 4.65.0.12 |

## CUDA

当前生效的工具包是 **CUDA 13.4.1**。驱动能直接运行的 CUDA UMD 是 **13.3**。用 13.4 的默认 PTX 做 JIT 时，驱动返回 “the provided PTX was compiled with an unsupported toolchain”。指定 `-arch=sm_86`、直接生成 SASS 后可以运行。

| 项目 | 值 |
|---|---|
| `CUDA_PATH` | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v13.4` |
| nvcc | 13.4.59（`cuda_13.4.r13.4/compiler.38657139_0`，2026-08-03 构建） |
| cudart | 13.4.49（`cudart64_13.dll`） |
| nvrtc | 13.4.59 |
| cuBLAS | 13.7.0.27 |
| cuFFT | 12.4.0.34 |
| cuRAND | 10.4.4.49 |
| cuSOLVER | 12.3.2.15 |
| cuSPARSE | 12.8.6.49 |
| NPP | 13.2.0.35 |
| nvJPEG | 13.2.2.35 |
| nvJitLink | 13.4.52 |
| CUPTI | 13.4.58 |
| Nsight Compute | 2026.3.0.13 |
| Nsight Systems | 2026.3.2 |
| Nsight Visual Studio Edition | 2026.3 |

磁盘上还有一个不完整的 `v13.3` 目录，里面只有 `bin\x64\nvrtc64_130_0.dll` 和 `nvrtc-builtins64_133.dll`，没有 `nvcc`。PATH 里还留着已经不存在的 `v13.0` 和 `v12.4`。

## 测试结果

结论：这次开机解锁成功，并且 Windows 会话里仍然保持解锁态。

### 解锁事务 RUN03

日志：`H:\RTX3090-UNLOCK\RUN03\REPORT.TXT`，文件时间 2026-11-14 13:47:08。Windows 本次开机时间 13:47:51，中间没有平台复位。固件默认启动项仍是 Windows Boot Manager；这次是从 U 盘上的实验 EFI 进入的。

| 项目 | 结果 |
|---|---|
| 构建 | `entryLatchedSs1Full`，实验性手动解锁 |
| 目标卡 | `0000:01:00.0`，子系统 `0x87AF1043`，设备 `0x220410DE` |
| PROM | 匹配，`9ac95be63f69488f6d9c52b6d2b81f60c8f89c4149225b9ab85c42fdba094ce5` |
| 进入时选择器 | `SS0=0x11160107`，`SS1=0x7` |
| 写入目标 | `SS0=0x88888888`，`SS1=0x8` |
| FLR 前读回 | `ss0=0x88888888`，`ss1=0x8`，与目标一致 |
| FLR 后读回 | `SS0=88888888`，`SS1=00000008`，`FLR=1` |
| 事务 | `transaction result=0`，`attempted=1`，`driver_release=1`，`clean=1` |
| 结尾 | `FINAL status=0`，`stage=transaction` |

日志横幅写明该 EFI 接受 Intel iGPU。显示检查字段打印为 `amd_physical=1`；本机处理器是 i9-13900K。

这个状态只留在当前这次开机。平台复位或重新冷启动后，选择器会回到出厂值。

### 本次 Tensor GEMM

解锁日志写完后，在同一 Windows 会话里跑了 4096×4096 cuBLAS GEMM。FP32 走 `cublasSgemm`（pedantic）；FP16 / BF16 走 `cublasGemmEx`，Tensor Core，FP32 累加。每种精度预热 1 秒，采样 10 次，取中位数。运行时 `cuda_runtime=13030`，`cuda_driver_api=13030`，`cublas=130700`。矩阵缓冲区用 `cudaMemset 0x3c` 填充，没有做全 1 参考值校验。

| 精度 | 中位耗时 | 吞吐 |
|---|---:|---:|
| FP32 pedantic | 4.881 ms | 28.16 TFLOPS |
| FP16 Tensor / FP32 累加 | 1.031 ms | 133.28 TFLOPS |
| BF16 Tensor / FP32 累加 | 1.026 ms | 133.99 TFLOPS |

### 和本机以往测量对照

以往数字来自 `repo/evidence/benchmark.json` 与 `repo/docs/RESULTS.en.md`，同一块 RTX 3090、同一规格 4096×4096 GEMM。那次使用 CUDA 12.6 / cuBLAS 12.6、驱动 617.14，每种精度预热 2 秒、采样 30 次，并做全 1 参考值校验。协议和本次短探测不同，绝对数字不能逐位对比；Tensor 吞吐的分档可以对比。

| 测量 | FP32 | FP16 Tensor | BF16 Tensor |
|---|---:|---:|---:|
| 2026-10-20 复位后（解锁状态未保留） | 24.51 TFLOPS | 70.55 TFLOPS | 70.53 TFLOPS |
| 2026-10-20 解锁后不复位进 Windows | 24.89 TFLOPS | 125.91 TFLOPS | 128.70 TFLOPS |
| 2026-10-24 headless 三次中位数 | 22.85 TFLOPS | 124.97 TFLOPS | 128.93 TFLOPS |
| 2026-11-14 本次短探测 | 28.16 TFLOPS | 133.28 TFLOPS | 133.99 TFLOPS |

本次 FP16 / BF16 约为复位后那次的 1.9 倍，落在已解锁的一档。仓库把 2026-10-20 较早的约 70.5 TFLOPS 记为解锁后执行了 BIOS Reset、状态丢失的测量，不是一次单独的未解锁冷启动对照。
