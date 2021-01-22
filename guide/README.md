### initial data

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
