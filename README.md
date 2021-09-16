# tendermint-kvstore-builtin
An example of creating a built-in Tendermint Core application acting as a distributed key-value store.

### Version
- [Go](https://golang.org/): 1.17
- [Tendermint](https://tendermint.com/): 0.34.13
- [Badger](https://dgraph.io/badger): 1.6.2

### Installation
Install Go.
```
brew install golang
```

Install Tendermint.
```
brew install tendermint
```

### Build
```
go build
```

### Configuration
Clean the generated files (optional).
```
rm -rf ./tmp/kvstore
```

Create a default configuration, nodeKey and private validator files.
```
TMHOME="./tmp/kvstore" tendermint init
```

Edit the configuration file `./tmp/kvstore/config/config.toml`.
- Change the value of `max_batch_bytes` to for example `10485760` so that it is greater than `max_tx_bytes`. Otherwise, it might throw `config is invalid: error in [mempool] section: max_batch_bytes can't be less or equal to max_tx_bytes`.

- Change the value of `addr_book_file` to `"tmp/kvstore/config/addrbook.json"`.

### Get Started
```
./kvstore -config "./tmp/kvstore/config/config.toml"
```

### Testing
Send a transaction to insert a key-value pair.
```
curl -s 'localhost:26657/broadcast_tx_commit?tx="tendermint=rocks"'
```

Query the value with the key. The `key` and `value` in the response are base64-encoded.
```
curl -s 'localhost:26657/abci_query?data="tendermint"'
```

### Reference
https://docs.tendermint.com/v0.34/tutorials/go-built-in.html