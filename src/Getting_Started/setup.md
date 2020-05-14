```sh
$ git clone git@github.com:LayerXcom/anonify.git
```


```sh
$ docker pull osuketh/anonify
```

Anonifyは、特定のブロックチェーンに依存しません。
本例では、Ethereum上にスマートコントラクトをビルドし、状態データを記録します。


```sh
$ solc -o build --bin --abi --optimize --overwrite contracts/Anonify.sol
```





