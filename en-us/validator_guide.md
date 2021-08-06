# Run

## Hardware

```
CPU: 16Core
RAM: 32GB
HDD: SSD 1TB
```

## Initialize

Refer to [Run a Node](/en-us/node_run.md)

## Create Validator Address

You need to create an account that represents a validator's consensus key for block signatures. Use the following command to create a new account and set a password for that account:

```
cetd account new --datadir /path/your-data-localtion-folder
```

## Start Validator Node

Save keyfile password of validator account in file

```
echo "your password" > password.txt
```

Start mining
```
cetd --datadir /path/your-data-localtion-folder -unlock "your validator address" --password /path/your-keyfile-folder/password.txt  --mine  --allow-insecure-unlock
```