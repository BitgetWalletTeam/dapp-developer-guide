# DApp develop guide 

## 准备工作

安装Bitget Wallet 钱包插件 https://web3.bitget.com/en/wallet-download

1. 以桌面版 chrome 为例，也完全适用 Mobile App
2. 以evm 链为例 https://web3.bitget.com/zh-CN/docs/provider-api/evm.html 
3. Wallet API Demo https://github.com/BitgetWalletTeam/wallet-api-demo

## 基础介绍

插件钱包会在浏览器加载页面时在 `window` 挂载钱包对象（以下统一称作 `provider`），Bitget Wallet 注入的对象为 `window.bitkeep`，不同链基于  `window.bitkeep` 注册，具体细节参考官方文档 https://web3.bitget.com/zh-CN/docs/provider-api/evm.html。

比如 evm：`provider  = window.bitkeep.ethreum;` 反之也可以通过 `provider` 是否存在判断用户是否安装钱包插件。

## 与钱包通讯

在页面中直接获取 provider 后即可调用相关 API，钱包常见的 API 有

1. 链接钱包/断开链接
2. 获取钱包账号信息
3. 获取当前主网/添加主网/切换主网
4. 获取余额
5. 普通数据签名
6. 交易签名
7. 发送交易

另外钱包还会提供事件监听，方便 DApp 获取钱包中的一些操作，一般提供 2 个：

1. 监听账号切换
2. 监听主网切换

## DApp 链接钱包的基本思路

## 1. 通过 `provider` 链接钱包
> 请注意，首先一定是链接钱包。

1. 获取 Bitget Logo，开发链接界面 https://github.com/bitkeepwallet/download/ ，建议即便用户没有钱包，也通过良好的寿命引导用户安装钱包
2. 链接钱包
3. 也可以使用三房钱包链接组件：https://github.com/BitgetWalletTeam/wallet-adapter-demo
4. [基于钱包实现免注册登录](./Login-by-wallet.md)

## 2. 主网

1. 获取当前主网，判断是否为目标主网
2. 如果不是，切换至目标主网，切换失败则进行添加

## 3. 钱包账号

1. 获取账号信息
2. 获取余额

## 4. 常见业务交互

1. 支付场景，调用交易部分 API，发起支付前确保余额足够
2. 操作验证，调用签名部分 API

## 5. 与合约交互

> 请注意，new Web3 时一定要传入钱包 provider

```
import Web3 from 'web3'

const web3 = new Web3(provider);

const abi = ['abi conent'];
const contractAddress = 'xxxxxx';
const contract = new web3.eth.Contract(abi, contractAddress);
```





