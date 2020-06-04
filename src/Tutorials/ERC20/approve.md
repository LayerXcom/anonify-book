
本節では、`approve`、`transfer_from`について述べます。

## 事前状態

`init_state`で初期化を行います。

```sh
ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify init_state -t 100
```

Alice、Bob、Charlieの３人のアドレスです。  
アドレスを作成していない場合は、[mint/burnの手順](https://layerxcom.github.io/anonify-book/Tutorials/ERC20/mint_burn/)を参考にしてください。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli wallet list
Alice: JeMocNNkNqABAEqBEurffNHIr0Y=
Bob: SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
Charlie: On1lVfkMUGm6+lT3OetO8A2HR4M=
```

それぞれの残高は以下のようになっています。

```sh
# Aliceの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 100

# Bobの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 0

# Charlieの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 2
Current State: 0
```

## approve

AliceからBobに`30`を`approve`します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify approve -a 30 -t SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
Transaction Receipt: "2cdda1f698c359e8eef6d94793c2713049eb8b3a2053fe2d744ad187253cf6ec"
```

`allowance`でBobに`approve`した量を確認してみましょう。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify allowance -i 0 -t SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
Current State: 30
```

## transfer_from

次に、`transfer_from`を用いて、BobからCharlieに`10`を送金します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify transfer_from -a 10 -i 1 -f JeMocNNkNqABAEqBEurffNHIr0Y= -t On1lVfkMUGm6+lT3OetO8A2HR4M=
Transaction Receipt: "2a3732f73ed4ae0ca59ec758097f882d49348bbfd61a6cb156739a211fe807b0"
```

##  事後状態

Alice、Bob、Charlieの最終的な残高を確認します。

```sh
# Aliceの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 90

# Bobの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 0

# Charlieの残高
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 2
Current State: 10
```

AliceからCharlieへ`10`だけ送金されたことが確認できます。  
また、Bobの`approve`された残額を確認します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify allowance -i 0 -t SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
Current State: 20
```

`approve`された`30`のうち、`10`を送金したため、残りが`20`となっていることが確認できました。