# Tools

## Interaction tools

Interact with your MultiChain nodes using [JSON-RPC API](https://www.multichain.com/developers/json-rpc-api/).

Use [curl](https://curl.haxx.se) or [Postman](https://www.getpostman.com) to invoke [MultiChain API methods](https://www.multichain.com/developers/json-rpc-api/).

Example below demonstrates how to get basic network information:

``` sh
$ curl -H "Content-Type: application/json" \
  -u amazing-crier:puppy-amino-volhard-dash-baggie-marrow
  -d '{"method":"getinfo","params":[],"id":1,"chain_name":"nw-123-456-7"}' \
  https://nd-123-456-789.p2pify.com:8545

{"result":{"version":"2.0","nodeversion":20000901,"protocolversion":20004,"chainname":"nw-123-456-7", ...}
```

## Development tools

### JavaScript

Work with MultiChain from your JavaScript application.

1. Install [multinodejs](https://github.com/sdec-brasil/multinodejs).

2. Configure the client to use `host` of the node RPC endpoint and the corresponding RPC `user` and `pass`:

``` js
let multichain = require("multinodejs")({
    host: "nd-123-456-789.p2pify.com",
    protocol: "https",
    user: "amazing-crier",
    pass: "puppy-amino-volhard-dash-baggie-marrow"
});
```

3. Invoke any methods from the [MultiChain API specification](http://www.multichain.com/developers/json-rpc-api/):

``` js
multichain.getInfo((err, info) => {
    if (err) {
        throw err;
    }
    console.log(info);
});
```

The example code above should output basic network information:

``` js
{ version: '2.0',
  nodeversion: 20000901,
  protocolversion: 20004,
  chainname: 'nw-123-456-7',
  ... }
```

### Python

Work with MultiChain from your Python application.

1. Install [multichaincli](https://github.com/chainstack/multichaincli).

2. Configure the client to use `host` and `port` of the node RPC endpoint, the corresponding RPC `username` and `password` and network `chainname`:

``` python
from multichaincli import Multichain

host = "nd-123-456-789.p2pify.com"
port = "80"
username = "amazing-crier"
password = "puppy-amino-volhard-dash-baggie-marrow"
chainname = "nw-123-456-7"

multichain = Multichain(username, password, host, port, chainname)
```

3. Invoke any methods from the [MultiChain API specification](http://www.multichain.com/developers/json-rpc-api/):

``` python
info = multichain.getinfo()
print(info)
```

The example code above should output basic network information:

``` python
{'version': '2.0', 'nodeversion': 20000901, 'protocolversion': 20004, 'chainname': 'nw-123-456-7', ... }
```

::: tip See also

* [Decentralized reputation on MultiChain](/tutorials/decentralized-reputation-on-multichain)

:::
