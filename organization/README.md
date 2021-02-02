## 介绍
部署`organization`合约是创建一个组织的第一步，该合约内函数包括：
* `initorg`：初始化组织函数
* `changename`：更改组织名称函数
* `changedescid`：更改组织解决函数
* `changeperm`：更改组织内部决策权限函数
* `reg`：组织成员登记函数
* `addplugin`：为组织添加插件函数
* `approvetrx`：授权执行Token交易函数
* `approvenft`：授权执行NFT交易函数
* `mtransfer`：合约相关交易实际的执行函数

## 安装部署
* 一、首先将合约编译成WASM文件并部署到EOS
* 二、执行`initorg`函数，输入组织名称、组织创始人、组织简介。注意：这里简介是一个IPFS的CID格式。
* 三、然后是为组织安装插件，DAO把所有组织的功能都做成插件的形式，按需安装使用。调用`addplugin`进行安装，该函数的入参看注释应该能大概知道什么意思，这里说两个：第一个参数caller是调用该函数(addplugin)的EOS账号，因为是初始安装，所以只有创始人有权限；最后一个参数autonomous_acts说明一下，意思是当前安装的合约，哪些是需要进行自治的操作，例如：安装的是Token合约，那么可能代币的发行、挖矿、销毁等这些都是自治的操作。  