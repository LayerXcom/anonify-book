
Anonifyのセットアップについて説明します。

## 動作環境

- [Azure Confidential Computing](https://azure.microsoft.com/ja-jp/solutions/confidential-compute/)のようなIntel SGXをサポートするハードウェア環境


## セットアップ

dockerイメージおよびAnonifyレポジトリを取得します。

```sh
$ docker pull osuketh/anonify
$ git clone git@github.com:LayerXcom/anonify.git
$ cd anonify
```

Anonifyは、特定のブロックチェーンに依存しません。  
本例では、状態データを記録にEthereumを用いるため、スマートコントラクトをビルドします。

```sh
$ solc -o build --bin --abi --optimize --overwrite contracts/Anonify.sol
```

## サーバー起動

`docker-compose`を用いてサーバーを起動します。本サーバーがAnonifyネットワークとの接続を行います。

```sh
$ docker-compose -f docker/docker-compose-anonify.yml up -d
```

## CLIのビルド

Anonifyでサポートするコマンドを利用するため、CLIをビルドします。

```sh
$ ./scripts/build-cli.sh
```
