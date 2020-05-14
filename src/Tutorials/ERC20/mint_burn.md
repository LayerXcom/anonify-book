
本節では、`mint`、`burn`について述べます。

## 事前状態

`init_state`で初期化を行います。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify init_state -t 100
```

Alice、Bob、Charlieの３人のアドレスを作成します。
`wallet password`および`account name`を設定してください。

```sh
$ ./target/debug/anonify-cli wallet init
$ ./target/debug/anonify-cli wallet add-account
$ ./target/debug/anonify-cli wallet add-account
```

`list`コマンドで作成したaccountを確認できます。

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

## mint

Bobに`50`をmintします。
`init_state`を実行したAliceの権限で実行する必要があります。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify mint -a 50 -t SyQwvGjGQmA4OG1ZV2zMNn4GXpA=
Transaction Receipt: "c05dc918cde8caa83e4233bff236285efc7197f554a844e590619d1c24d41b8d"
```

## mint後の状態

`mint`後のAlice、Bob、Charlieの残高を確認します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 100

$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 50

$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 2
Current State: 0
```

`mint`された`50`がBobに付与されていることがわかります。

## burn

Aliceから`30`を`burn`します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify burn -i 0 -a 30
Transaction Receipt: "917576ddb5bdd68f01d2bb98f3ae4dcafec28c385bdb1033ed9b2b51529c4c22"
```

## burn後の状態

`burn`後のAlice、Bob、Charlieの残高を確認します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 70

$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 50

$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 2
Current State: 0
```

Aliceの残高が`100`から`30`減り、`70`となっていることが確認できました。

## オーナー以外のユーザーによるburn

`burn`はオーナー以外でも実行が可能です。
Bobから`10`を`burn`してみましょう。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify burn -i 1 -a 10
Transaction Receipt: "59d139d1ea29ddd008ecb7947b55677d9013b24f5b7de3ea2b70badfcfe3c848"
```

## オーナー以外のユーザーによるburn後の状態

`burn`後のAlice、Bob、Charlieの残高を確認します。

```sh
$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 0
Current State: 70

$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 1
Current State: 40

$ ANONIFY_URL=http://172.28.1.1:8080 ./target/debug/anonify-cli anonify balance_of -i 2
Current State: 0
```

Bobの残高が`50`から`10`減り、`40`となっていることが確認できました。
なお、他の所有者の残高に変化はありません。