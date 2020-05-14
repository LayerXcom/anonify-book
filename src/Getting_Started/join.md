



```sh
$ ./target/debug/anonify-cli wallet init
$ ./target/debug/anonify-cli wallet add-account
```

```sh
$ ANONIFY_URL=http://172.18.0.3:8080 ./target/debug/anonify-cli anonify deploy
```

```sh
$ export CONTRACT_ADDR=6d68b0a618ab5a08be3600957f768c15c9b04baa
```

```sh
$ ANONIFY_URL=http://172.18.0.4:8080 ./target/debug/anonify-cli anonify set_contract_addr 
```


```sh
$ ANONIFY_URL=http://172.18.0.3:8080 ./target/debug/anonify-cli anonify start_polling
$ ANONIFY_URL=http://172.18.0.4:8080 ./target/debug/anonify-cli anonify start_polling
```




```sh
$ ANONIFY_URL=http://172.18.0.4:8080 ./target/debug/anonify-cli anonify register
```


cliのビルド

```sh
$ cd anonify
$ ./scripts/build-cli.sh
```
