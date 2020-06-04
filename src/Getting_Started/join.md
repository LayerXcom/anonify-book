
## スマートコントラクトのデプロイ

スマートコントラクトのデプロイを行います。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify deploy
6d68b0a618ab5a08be3600957f768c15c9b04baa
```

デプロイすると上記のように、コントラクトのアドレスが出力されます。このアドレスを環境変数`CONTRACT_ADDR`に設定します。

```sh
$ export CONTRACT_ADDR=6d68b0a618ab5a08be3600957f768c15c9b04baa
```

環境変数を設定した状態で、`set_contract_addr`を実行することで、Anonify上にコントラクトアドレスを設定できます。

```sh
$ ANONIFY_URL=http://172.28.1.2:8080 ./target/debug/anonify-cli anonify set_contract_addr 
```

さらに、Anonifyネットワークの状態遷移を監視するため、`start_polling`を実行します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify start_polling
$ ANONIFY_URL=http://172.28.1.2:8080 ./target/debug/anonify-cli anonify start_polling
```

## ネットワークへの参加

Anonifyネットワークに参加するため、`register`を実行します。
Attested Computingのための検証(REPORT提出）とグループ鍵の共有（Add Handshake）が実行されます。

```sh
$ ANONIFY_URL=http://172.28.1.2:8080 ./target/debug/anonify-cli anonify register
```

これでAnonifyネットワークへの参加が完了です。  
次節で述べるよう独自関数を実装することが可能です。[ERC20のチュートリアル](https://layerxcom.github.io/anonify-book/Tutorials/ERC20/transfer/)も実行できます。
