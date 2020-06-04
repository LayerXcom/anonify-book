
本節では、`transfer`について述べます。

## 事前状態

`init_state`で初期化を行います。

```sh
ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify init_state -t 100
```

Alice、Bobの2人のアドレスです。  
アドレスを作成していない場合は、[mint/burnの手順](https://layerxcom.github.io/anonify-book/Tutorials/ERC20/mint_burn/)を参考にしてください。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli wallet list
Alice: JeMocNNkNqABAEqBEurffNHIr0Y=
Bob: SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
```

それぞれの残高は以下のようになっています。

```sh
# Aliceの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 100

# Bobの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 0
```

## transfer

`transfer`でAliceからBobへ`20`を送金します。

```sh
＄ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify transfer -a 20 -t SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
Transaction Receipt: "0d89b58846a0db41976c6f95c62c5bfb63a5b2d4e29a560d652b913889edfde8"
```

## 事後状態

送金後の残高を確認します。

```sh
# Aliceの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 80

# Bobの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 20
```

AliceからBobへ`20`を送金できました。
