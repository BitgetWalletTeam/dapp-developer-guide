# 基于钱包实现免注册登录

## 1. 用户标识

使用钱包账号 address 作为用户 id，address 可通过钱包 API 直接获取。

## 2. 生成随机数

前端请求服务器，上报 address，获取服务器端分配的与 address 对应的 nonce。

## 3. 签署Nonce

前端接收 nonce 后调用钱包签名方法，使用签名结果 signature 和 address 进行登录。

请注意，签名方法会弹出钱包界面，需要用户授权。

## 4. 签名验证

具有随机数，钱包地址和签名后，后端可以验证用户已正确签署了随机数。验证通过则证明用户拥有钱包地址，然后视为登录成功并继续后续业务逻辑。

## 5. 更改Nonce
为了防止用户使用相同的签名再次登录（如果它被泄露），确保同一用户再次登录时需要签署一个新的 nonce。

## 6. 为什么登录流程有效
根据定义，身份验证实际上只是帐户所有权的证明。如果使用钱包地址唯一地标识用户，那么证明用户拥有该帐户就非常简单。

为了防止黑客获取某个特定邮件及其签名（但不是实际私钥），需要签名的消息满足以下条件：

1. 由后端提供
2. 定期改变