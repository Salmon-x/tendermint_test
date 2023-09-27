这是一个简单的tendermint应用

- badger 内嵌式数据库
- config tendermint配置文件，通过`tendermint init`获取
- data 数据库文件
- app.go 自主实现的abci应用程序

> 编译后运行 `tendermint_test.exe --config "./config/config.toml"`
> 如果运行成功并且看到持续的块生成，可以访问`http://localhost:26657/broadcast_tx_commit?tx="tendermint=rocks"`
> 这代表了一个发送的交易,(详情查看tendermint abci)
> 成功的话，您将看到：
```json
{
    "jsonrpc": "2.0",
    "id": -1,
    "result": {
        "check_tx": {
            "code": 0,
            "data": null,
            "log": "",
            "info": "",
            "gas_wanted": "0",
            "gas_used": "0",
            "events": [],
            "codespace": ""
        },
        "deliver_tx": {
            "code": 0,
            "data": null,
            "log": "",
            "info": "",
            "gas_wanted": "0",
            "gas_used": "0",
            "events": [],
            "codespace": ""
        },
        "hash": "1B3C5A1093DB952C331B1749A21DCCBB0F6C7F4E0055CD04D16346472FC60EC6",
        "height": "50"
    }
}
```
这代表了成功发送交易，并且返回了块的高度，50，可以通过访问：`http://localhost:26657/abci_query?data="tendermint"`
来验证，将看到：
```json
{
    "jsonrpc": "2.0",
    "id": -1,
    "result": {
        "response": {
            "code": 0,
            "log": "exists",
            "info": "",
            "index": "0",
            "key": "dGVuZGVybWludA==",
            "value": "cm9ja3M=",
            "proofOps": null,
            "height": "0",
            "codespace": ""
        }
    }
}
```