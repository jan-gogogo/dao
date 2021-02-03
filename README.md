## DAO?
DAO(Decentralized Autonomous Organizations，去中心化自治组织)，任何人都可以在这里创建组织，他们使用共同制定的规则为了同一个使命共同努力贡献，他们可以是完全不认识的，也可以不信任彼此，组织没有所谓的管理员。

例如：A发行了一种代币，他想让令代币具有更高的价值，于是他创建了一个组织，持有代币的人都可以加入组织，所有与这个组织相关的操作都可以通过投票决定，而投票的规则是他们共同制定的，例如：一个成员觉得为代币搭建一个网站很有必要，因为创建网站需要资金，他可以发起一个创建网站的投票，如果通过，资
金会自动转账。

整个系统基于EOS智能合约开发。

## 目录

```
guide			//向导合约模板，保存全局数据，平台唯一
lib			//公共库文件
├──assets.hpp		//资产，提供对合约账号Token操作的函数
├──auths.hpp		//权限，准入权限的控制
├──consts.hpp		//常量，全局常量
├──safemath.hpp		//计算，无符号整形数字运算
├──structs.hpp		//结构表
├──trxs.hpp		//交易执行
organization		//组织合约模板，组织内唯一
plugins			//插件
├──mining		//挖矿合约模板
├──token		//代币合约模板
├──voting		//投票合约模板
```

## 安装部署
> 首先至少需要准备好四个EOS账号：用于部署guide、organization、token、voting。

*	首先部署向导合约`guide`，详情查看[guide合约模板介绍](https://github.com/jan-gogogo/dao/tree/main/guide)
* 部署`organization`，	详情查看[organization合约模板介绍](https://github.com/jan-gogogo/dao/tree/main/organization) 安装部署部分
* 安装插件,详情查看[plugin合约介绍](https://github.com/jan-gogogo/dao/tree/main/plugins)


