### 介绍
`guide`合约是提供给平台使用，合约内部只有保存插件（添加&修改），移除插件两个函数，这些操作会影响所有的组织。	

### 初始化数据示例

Organization basic data
```sh
cleos push action ContractName saveplugin '{"pcode":"organization",
					"pname":"Organization",
					"version":"1.0.0",
					"des_cid":"","autonomous_acts":["changename","changedescid","changeperm","addplugin","approvetrx","approvenft"],
					"is_basic":true}' -p ContractName
```

Voting plugin data
```sh
cleos push action ContractName saveplugin '{"pcode":"voting",
					"pname":"Voting",
					"version":"1.0.0",
					"des_cid":"",
					"autonomous_acts":["changesr","changemaq","changevts","newvote"],
					"is_basic":false}' -p ContractName
```

Token plugin data
```sh
cleos push action ContractName saveplugin '{"pcode":"token",
					"pname":"Token",
					"version":"1.0.0",
					"des_cid":"",
					"autonomous_acts":["mint","retire"],
					"is_basic":false}' -p ContractName
```


Mining plugin data
```sh
cleos push action ContractName saveplugin '{"pcode":"mining",
					"pname":"Mining",
					"version":"1.0.0",
					"des_cid":"",
					"autonomous_acts":["changeconf","addexin","rmexin"],
					"is_basic":false}' -p ContractName
```

### remove

```sh
cleos push action ContractName removeplugin '{"pcode":"plugin.name"}' -p ContractName

```
