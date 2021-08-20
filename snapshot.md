# 快照

* [Latest Snapshot](https://github.com/coinex-smart-chain/csc-snapshots)

## 场景

`CSC` 定期快照链数据并提供其压缩文件的下载链接。快照数据主要用于两个场景：

1. 修复被卡住或崩溃的节点；
2. 快速启动一个新的节点，避免为同步等待很长时间。

## 使用

**步骤 1: 准备工作**

- 确保你的硬件配置满足要求
- 有足够的磁盘存储空间，至少是快照数据大小的两倍

**步骤 2: 下载并解压**

- 拷贝快照下载链接
- 下载：`wget -O csc.zip "{paste snapshot URL here}"` 。下载需要花费一些时间，你可以在后台进行：`nohup wget -O csc.zip "{paste snapshot URL here}" &`
- 解压: `unzip csc.zip`。解压需要花费一些时间，你可以在后台进行： `nohup unzip csc.zip &`
- 你可以通过运行一个脚本来完成以上步骤：

```
wget -O csc.zip "{paste snapshot URL here}"
unzip csc.zip
```

**步骤 3: 替换数据**

- 首先，如果你有一个正在运行的 `CSC ` 客户端，通过 `kill {pid}` 命令将它停止，并确保它已被停止。

- 考虑备份原始数据：

  ```
  mv ${CSC_DataDir}/cetd/chaindata ${CSC_DataDir}/cetd/chaindata_backup
  mv ${CSC_DataDir}/cetd/triecache ${CSC_DataDir}/cetd/triecache_backup
  ```

- 替换数据：

  ```
  mv data/cetd/chaindata ${CSC_DataDir}/cetd/chaindata
  mv data/cetd/triecache ${CSC_DataDir}/cetd/triecache
  ```

- 再次启动 `CSC` 客户端并检查日志