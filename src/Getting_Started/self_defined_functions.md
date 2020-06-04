
本設では、Anonifyにて独自ロジックを実装する方法について説明します。


## Enclave内のメモリを定義

`impl_memory`マクロによって、Enclave内に確保されるメモリを定義します。  
例えば、[ERC20のチュートリアル](https://layerxcom.github.io/anonify-book/Tutorials/ERC20/)では、以下のような4つを定義しています。

```rust
impl_memory! {
    (0, "Balance", U64),
    (1, "Approved", Approved),
    (2, "TotalSupply", U64),
    (3, "Owner", UserAddress)
}
```

第1引数にEnclave上のID、第2引数に名前、そして第3引数に型を指定します。

## 独自関数の定義

`impl_runtime`マクロによって、関数を定義することが可能です。  
以下は、[ERC20のチュートリアル](https://layerxcom.github.io/anonify-book/Tutorials/ERC20/transfer/)で利用する`transfer`の実装例です。


```rust
impl_runtime!{
    #[fn_id=1]
    pub fn transfer(
        self,
        sender: UserAddress,
        recipient: UserAddress,
        amount: U64
    ) {
        let sender_balance = self.get_map::<U64>(sender, "Balance")?;
        let recipient_balance = self.get_map::<U64>(recipient, "Balance")?;

        ensure!(sender_balance > amount, "transfer amount exceeds balance.");

        let sender_update = update!(sender, "Balance", sender_balance - amount);
        let recipient_update = update!(recipient, "Balance", recipient_balance + amount);

        insert![sender_update, recipient_update]
    }
}
```

`update`マクロと`insert`マクロを組み合わせて、状態遷移を実現できます。