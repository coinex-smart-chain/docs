# 启动验证节点

## 硬件要求

```
cpu: 16core
内存: 32g
硬盘: ssd 1T
```
## 初始化节点

参考[启动节点](/node_run.md)

## 创建验证节点地址

你需要创建验证节点的地址及秘钥，以便出块签名。使用下面命令创建新账号：

```
cetd account new --datadir /path/your-data-localtion-folder
```

## 启动验证节点

将验证节点的keyfile密码保存文件中

```
echo "your password" > password.txt
```

启动挖矿
```
cetd --datadir /path/your-data-localtion-folder -unlock "your validator address" --password /path/your-keystore-folder/password.txt  --mine  --allow-insecure-unlock
```

