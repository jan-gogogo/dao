## 介绍
为了方便扩展，DAO支持功能插件化，所有对组织的操作都可以以插件的形式进行扩展，插件与插件之间也可以自由调用，目前这三个插件功能是必须的，是支持一个分布式自治组织的最小功能集合，我们成为系统插件。

系统插件之间是有依赖的，`voting`依赖`toekn`，因为只有组织会员能进行投票，而持有该组织的token才能算是组织会员，另外投票权重也是根据持有数量划分。`token`依赖`mining`，挖矿其实就是发行token的一个过程，至于什么操作导致挖矿，就是由用户自己去控制了。



## 安装部署

一、先准备三个EOS账号，将三个系统插件的智能合约编译并部署到EOS。

二、调用`organization`的`addplugin()`函数，为组织添加插件，详情查看[组织合约详情说](https://github.com/jan-gogogo/dao/tree/main/organization)。

三、每个插件都会有一个`init()`函数，在使用前一定要先执行。


## voting
投票插件合约，实现组织自治的重要工具。
在安装投票插件之前，必须先按照一个Token插件，可以将Token看作是一个成员在组织的股份，持有的Token越多权重越大。

其中投票是否通过的核心判断逻辑代码如下：

```c++
 if (_is_reach(v.yea, v.total_weight, v.support_required)) {
        return true;
    } else {
        if (_is_expire(v.expire_time)) {
            const uint64_t totol_votes = safemath::add(v.yea, v.nay);
            return _is_reach(v.yea, totol_votes, v.support_required) && _is_reach(v.yea, v.total_weight, v.min_accept_quorum);
        } else {
            return false;
        }
    }

```

#####其中有两个很重要的参数需要说明：

* `support_required` 需要的支持率
* `min_accept_quorum` 最低支持率

举个例子，`support_required`设置为51%，`min_accept_quorum`设置为20%。根据上面代码，如果支持率达到51%，直接就通过。如果直到投票时间已到，还没达到51%支持率，还是又机会通过的：首先投`YES`票的人必须占投票总数的51%，而且支持率必须达到20%，即可通过投票。

由于EOS保存小数精度问题，一般会把小数转换成大整数，这里我们会乘以一个10^12，数值表示：

```c++
//0% = 0
//1% = 10^10
//100% = 10^12
```

### 合约函数说明
| Actino | 默认执行权限 | 是否可修改 | 建议权限 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
| ----------- | ------------ | ------------ | ------------ |
|init|self|否|-|
|changesr|founder|是|voting|
|changemaq|founder|是|voting|
|changevts|founder|是|voting|
|vote|token.holder|否|-|
|newvote|founder|是|voting<br/>token.holder|
|executevote|任何人/voter|否|-|
|timeup|self|否|-|
|lognewvote|self|否|-|

Action权限说明：

* self：合约自身
* founder：组织创始人的账号
* token.holder：Token持有人
* voting：组织投票插件合约账号

## token
组织代币，该合约是基于EOS标准代币`eosio.token`修改，所以表结构基本没变，只是做了一些增量。

### 合约函数说明
| Actino | 默认执行权限 | 是否可修改 | 建议权限 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
| ----------- | ------------ | ------------ | ------------ |
|init|self|否|-|
|retire|founder|是|voting|
|transfer|任何人|否|-|
|mint|founder|是|组织指定的其他合约|

Action权限说明：

* self：合约自身
* founder：组织创始人的账号
* voting：组织投票插件合约账号

## mining
安装此插件前提：必须先按照 `token` 插件。

### 合约函数说明
| Actino | 默认执行权限 | 是否可修改 | 建议权限 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
| ----------- | ------------ | ------------ | ------------ |
|init|self|否|-|
|changeconf|founder|是|voting|
|addexin|founder|是|voting|
|rmexin|founder|是|voting|

Action权限说明：

* self：合约自身
* founder：组织创始人的账号
* voting：组织投票插件合约账号









