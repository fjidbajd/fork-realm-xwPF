

---

## 中文版

> 🚀 **Realm 端口转发智能管理脚本** - 集成原生 realm 全部功能 + 轻量化实现故障转移，保持极简本质,数字化操作界面一键指令操作,提高效率

## 📸 界面预览

<details>
<summary>点击查看界面截图</summary>

**主界面**
![主界面](https://i.mji.rip/2025/07/11/cc6e7c4a5b723a4b7d0aef1e69c34896.png)

**定时任务管理**
![定时任务](https://i.mji.rip/2025/07/11/46ad95de9117d32b444097ead36f9850.png)

**转发配置管理**
![配置管理](https://i.mji.rip/2025/07/11/0f57b375f28aa93ba6b5beaf0e9e53f8.png)

**负载均衡与故障转移**
![负载均衡+故障转移](https://i.mji.rip/2025/07/11/f44f30b5ee36841aef948e12e4f1c6b6.png)

</details>

## 🚀 快速开始（网络受限看下文）

### 一键安装

**使用 wget**
```bash
wget -qO- https://raw.githubusercontent.com/fjidbajd/fork-realm-xwPF/refs/heads/main/xwPF.sh | sudo bash -s install
```

## 🧭 离线安装（网络受限环境）

<details>
<summary>点击展开离线安装方法</summary>

适用于无法直接访问 GitHub 的服务器环境：

**下载必要文件**

在有网络的设备上下载以下文件：
- **脚本文件下载**：[xwPF.sh](https://github.com/zywe03/realm-xwPF/raw/main/xwPF.sh) (右键点击 → 另存为)
- **Realm 程序下载**（根据系统架构选择）：

| 架构 | 适用系统 | 下载链接 | 检测命令 |
|------|----------|----------|----------|
| x86_64 | 常见64位系统 | [realm-x86_64-unknown-linux-gnu.tar.gz](https://github.com/zhboner/realm/releases/download/v2.7.0/realm-x86_64-unknown-linux-gnu.tar.gz) | `uname -m` 显示 `x86_64` |
| aarch64 | ARM64系统 | [realm-aarch64-unknown-linux-gnu.tar.gz](https://github.com/zhboner/realm/releases/download/v2.7.0/realm-aarch64-unknown-linux-gnu.tar.gz) | `uname -m` 显示 `aarch64` |
| armv7 | ARM32系统（如树莓派） | [realm-armv7-unknown-linux-gnueabihf.tar.gz](https://github.com/zhboner/realm/releases/download/v2.7.0/realm-armv7-unknown-linux-gnueabihf.tar.gz) | `uname -m` 显示 `armv7l` 或 `armv6l` |

放置在同一目录,启动脚本选择**1. 安装配置**会优先自动检测**脚本同目录下的realm文件**进行安装

</details>

## ✨ 核心特性

### 🎯 核心功能
- **🚀 一键安装** - 单条命令完成所有安装和配置，支持**离线安装**
- **⚡ 原生 Realm 全功能** - 完整支持 realm 的所有原生功能
- **🔄 故障转移** - 自动故障检测
- **⚖️ 负载均衡** - 支持轮询、IP哈希等策略，可配置权重分配
- **🕳️ 搭建隧道** - 双端realm架构搭建隧道
- **📋 多规则管理** - 支持中转服务器和落地服务器的多规则配置
- **✅ 支持多种虚拟化** - 自动检测和适配

### 🛠️ 管理功能
- **📊 可视化界面** - 简洁的数字选择菜单，无需记忆复杂命令
- **📋 导出/导入配置文件** - 查看当前配置复制导出、识别同目录 JSON 配置文件导入
- **⏰ 定时任务** - 支持定时重启、维护等自动化任务
- **📁 状态管理** - 使用配置文件统一管理所有状态信息
- **🔧 智能检测** - 自动检测系统架构、依赖工具、端口冲突

### 🔒 安全与稳定
- **🛡️ 协议支持** - 支持 TCP/UDP 协议，支持 TLS，ws 加密传输
- **🔍 连通性测试** - 自动测试配置的连接可用性
- **📝 智能日志管理** - 自动限制日志大小，防止磁盘占用过大
- **🗑️ 完整卸载** - 分阶段全面清理，“轻轻的我走了，正如我轻轻的来”

## 🗺️ 示意图理解不同场景下工作原理(推荐)

<details>
<summary><strong>单realm架构只负责转发</strong></summary>

中转机realm只负责原模原样把设置端口收到的数据包进行转发,加密解密由代理工具负责

所以整个链路的加密协议由出口机代理软件决定

![4b6c044f27859f847690011589b0523a.png](https://i.mji.rip/2025/07/11/4b6c044f27859f847690011589b0523a.png)


</details>

</details>

<details>
<summary><strong>双realm架构搭建隧道</strong></summary>

在realm和realm之间多套一层realm支持的加密

所以中转机realm选择的加密,伪装域名等等,必须与落地机一致,否则无法解密

![0e1b55bbb90b59acb2c03e6acc7f0dbf.png](https://i.mji.rip/2025/07/11/0e1b55bbb90b59acb2c03e6acc7f0dbf.png)

</details>

</details>

<details>
<summary><strong>负载均衡+故障转移</strong></summary>

同一端口转发有多个出口机(规则组)

轮询 (roundrobin)

不断切换规则组里的出口机

IP哈希 (iphash)

基于源 IP 的哈希值，决定流量走向，保证同一 IP 的请求始终落到同一出口机

权重即分配概率

故障转移

检测到某个出口故障，暂时移出负载均衡列表，恢复之后会自动添加进负载均衡列表

原生realm暂不支持故障转移

脚本实现原理
```
1. systemd定时器触发 (每4秒)
   ↓
2. 执行健康检查脚本
   ↓
3. 读取规则配置文件
   ↓
4. 对每个目标执行TCP连通性检测
   ├── nc -z -w3 target port
   └── 备用: telnet target port
   ↓
5. 更新健康状态文件（原子更新）
   ├── 成功: success_count++, fail_count=0
   └── 失败: fail_count++, success_count=0
   ↓
6. 判断状态变化
   ├── 连续失败2次 → 标记为故障
   └── 连续成功2次+冷却期120秒(避免抖动频繁切换) → 标记为恢复
   ↓
7. 如有状态变化，创建更新标记文件
```

</details>

</details>

</details>

<details>
<summary><strong>端口转发 vs 链式代理(分段代理)</strong></summary>

容易搞混的两个概念

**简单理解**

端口转发只负责把某个端口的流量转发到另一个端口

而链式代理

![d4a7047e80a3530da9082c2e7a7e0968.png](https://i.mji.rip/2025/07/12/d4a7047e80a3530da9082c2e7a7e0968.png)

可以看到分成了两段代理链,所以又称为分段代理,二级代理（有机会再细讲配置）

**没有优劣之分**看使用场景

| 链式代理 (Chained Proxy) | 端口转发 (Port Forwarding) |
| :------------------- | :--------------------- |
| 配置复杂度较高              | 配置复杂度低（L4层转发）          |
| 会有每跳解包/封包开销          | 原生 TCP/UDP 透传，理论上更快    |
| 出站控制分流更精确（每跳配置出口）    | 难出站控制                  |

</details>

### 依赖工具
**Linux 原生轻量化工具**，保持系统干净轻量化

| 工具 | 用途 | 自动安装 |
|------|------|------|
| `curl` | 下载和IP获取 | ✅ |
| `wget` | 备用下载工具 | ✅ |
| `tar` | 解压缩工具 | ✅ |
| `systemctl` |总指挥协调工作 | ✅ |
| `bc` | 数值计算 | ✅ |
| `nc` | 网络连接测试 | ✅ |
| `grep`/`cut` | 文本处理识别 | ✅ |
| `inotify` | 标记文件 | ✅ |

## 📁 文件结构

安装完成后的文件组织结构：

```
📦 系统文件
├── /usr/local/bin/
│   ├── realm                    # Realm 主程序
│   ├── xwPF.sh                  # 管理脚本主体
│   └── pf                       # 快捷启动命令
│
├── /etc/realm/                  # 配置目录
│   ├── manager.conf             # 状态管理文件（核心）
│   ├── config.json              # Realm 工作配置文件
│   ├── rules/                   # 转发规则目录
│   │   ├── rule-1.conf          # 规则1配置
│   │   ├── rule-2.conf          # 规则2配置
│   │   └── ...
│   ├── cron/                    # 定时任务目录
│   │   └── tasks.conf           # 任务配置文件
│   └── health/                  # 健康检查目录（故障转移）
│       └── health_status.conf   # 健康状态文件
│
├── /etc/systemd/system/
│   ├── realm.service            # 主服务文件
│   ├── realm-health-check.service  # 健康检查服务
│   └── realm-health-check.timer    # 健康检查定时器
│
└── /var/log/
    └── realm.log                # 服务日志文件
```



