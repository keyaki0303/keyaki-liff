# keyaki-liff

## STATUS: CORE / 現役・最重要

- 使用頻度: 高
- コード重要度: 最重要
- 扱い: 現役。削除・アーカイブしない
- 理由: LINEから予約システムへ入る際のユーザー情報受け渡しを担うため

## このリポジトリの役割

`keyaki-liff` は、けやき鍼灸整骨院の **LINE公式アカウントと予約システム（keyaki-yoyaku）をつなぐ入口・橋渡し用のLIFFページ** です。

予約システム本体ではありません。

## なぜ作ったのか

当初、GASのWebアプリとLINEを直接連携させようとしましたが、GAS側だけではLINEのユーザーIDを期待どおり取得・受け渡しできず、LINE連携がうまく動きませんでした。

そのため、LINEのLIFFを入口として使い、LINE側でユーザー情報を取得してから予約GASへ渡す構成にしました。

つまり、このリポジトリは **GASとLINEの間をつなぐために追加した中継役** です。

## 処理の流れ

```text
患者さん
  ↓
LINE公式アカウントの予約メニュー
  ↓
keyaki-liff
  ↓
LIFF初期化・LINEログイン確認
  ↓
LINE userId / displayName を取得
  ↓
keyaki-yoyaku のGAS Webアプリへ渡す
  ↓
予約フォームを表示
```

## keyaki-yoyaku との違い

### keyaki-liff

- LINEから予約システムへ入るための入口
- LIFFの初期化
- LINEログイン確認
- LINEユーザー情報の取得
- 取得した情報を予約GASへ渡す

### keyaki-yoyaku

- 予約システム本体
- 予約受付
- 空き時間判定
- 患者情報処理
- Googleカレンダー連携
- 問診
- LINE通知など

## 重要な注意

- `keyaki-liff` を削除・停止すると、LINEから予約システムへ入れなくなる可能性があります。
- GitHub PagesやLIFFのEndpoint URLを変更する場合は、LINE Developers側の設定との整合確認が必要です。
- LIFF IDや予約GASのURLを変更する場合は、接続先を必ず確認してから変更します。
- このリポジトリには予約本体の重要ロジックを増やさず、原則として「LINE情報取得と予約システムへの橋渡し」に役割を限定します。
- このリポジトリは公開される可能性があるため、秘密情報・認証情報・患者情報は保存しません。

## 一言で覚える

**keyaki-liff = LINEからkeyaki-yoyakuへLINEユーザー情報を渡すための橋渡しページ**
