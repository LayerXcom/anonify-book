# Anonify

Anonifyはプライバシを保護した上で、ブロックチェーンを改ざん不可能なデータ共有基盤として用いることを可能にするシステムです。TEE (Trusted Execution Environment) を用いることにより、分散台帳の参加者間で明らかにしたくないデータを保護しながら高い可用性と柔軟なビジネスロジックの実行を可能にします。加えて,特定の主体に対しては分散台帳上のデータを読み取ることが可能な監査機能も提供しています。

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/81777586-203a1b00-952c-11ea-9757-705fd2ca6995.png" width="800px">
</div>

通常のブロックチェーンのように、状態遷移の履歴を平文のまま記録していくのではなく、AnonifyではTEEで暗号化された状態データをブロックチェーンに記録していきます。TEEの隔離保護領域内で状態遷移の計算を行い、その結果を暗号化しブロックチェーンに記録します。つまり,ブロックチェーンには全ての状態遷移の履歴を暗号文として記録し,TEEは最新の状態を平文として記録しています。保護領域内のデータはハードウェアレベルで外部から保護され、TEEを運営している管理者自身やOSなどのシステムソフトウェアもアクセスできないように保護されています。

## 参考リンク

- [ホワイトペーパー](https://layerx.co.jp/wp-content/uploads/2020/06/anonify.pdf)
- [ソースコード](https://github.com/LayerXcom/anonify)
- [スライド](https://speakerdeck.com/layerx/anonify)