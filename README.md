# Duckアドレス生成ツール

DuckDuckGo Email Protection の「Duckアドレスから新しいメールを送る」際に使う宛先形式を、ブラウザ内で組み立てる非公式の静的ツールです。

## 使い方

1. 送信先（相手）のメールアドレスを入力します（例：`hoge@gmail.com`）。
2. 自分のDuckアドレスを入力します（例：`my-duck` または `my-duck@duck.com`）。
3. 「アドレスを生成」を押します。
4. 生成された宛先をコピーするか、Gmailまたは端末の標準メールアプリを開きます。

例：`hoge@gmail.com` + `my-duck` → `hoge_at_gmail.com_my-duck@duck.com`

## 仕組み

- 送信先の `@` を `_at_` に置換し、`_` とDuckアドレス（`@duck.com` を含む）を連結します。
- 送信先は `^[^\s@]+@[^\s@]+\.[^\s@]+$` で検証します。
- Duckアドレスは、`@` を含む場合は `@duck.com` の形式のみ許可し、`@` がない場合は英数字と `._+-` のみ許可します。
- Gmailの作成画面には `encodeURIComponent` でエンコードした宛先を渡します。iOSではGmailアプリのURLを先に試し、約1.2秒以内にページが非表示にならなければWeb版へ移動します。
- 入力を編集すると、生成済みの結果は自動更新されます。入力が不正になった場合は結果を隠します。

## プライバシー

- 入力内容を外部サーバーへ送信しません。
- 入力内容を `localStorage`、Cookie、その他のブラウザ保存領域に保存しません。
- アクセス解析、外部ライブラリ、CDN、外部フォントを使用しません。
- CSPで `connect-src 'none'` を指定し、外部接続を行うスクリプト通信を禁止しています。ページ内での生成処理はすべてローカルで行います。
- Gmailやメールアプリを開く操作を実行した場合、宛先は選択されたメールサービス／アプリに渡されます。これはツール自体が入力内容を収集・送信することとは異なります。
- 公開後はブラウザの開発者ツール（Network）で、ページ読み込み時に外部通信がないことを確認してください。静的ホスティング事業者が通常のアクセスログを扱う場合がある点は、ホスティング事業者のポリシーに従います。

## 公式仕様の出典

DuckDuckGo Help Pages, “How do I compose a new email from my personal Duck Address?”  
https://duckduckgo.com/duckduckgo-help-pages/email-protection/duck-addresses/how-do-i-compose-a-new-email

公式ヘルプには、例として `brian_at_gmail.com_jane@duck.com` が示され、送信先の `@gmail` を `_at_gmail` に置き換え、個人Duckアドレスのユーザー名を後ろに連結する形式が説明されています。最終確認日：2026-10-20。

## 免責事項

本ツールは非公式の独立したツールであり、DuckDuckGoとは提携・関係していません。DuckDuckGo、Duckおよび関連名称は各権利者に帰属します。本ツールは宛先文字列を生成するだけで、メールの配信や送信者認証を保証しません。

## 公開方法

GitHub Pagesなどの静的ホスティングで公開できます。ビルド手順や外部依存はありません。このツールは個人サイトとは分離した専用リポジトリで管理します。

## License

MIT License。詳細は `LICENSE` を参照してください。

## 公開前の受け入れテスト

- [x] 正常系：`hoge@gmail.com` + `my-duck` から `hoge_at_gmail.com_my-duck@duck.com` を生成するロジックを確認
- [x] 異常系：`@` のない送信先、`@duck.com` 以外のDuck側ドメイン、不正文字を拒否するロジックを確認
- [x] Gmail URLの宛先が `encodeURIComponent` でエンコードされ、`@` が `%40` になることを確認
- [x] CSP、外部スクリプト／スタイル／フォント参照、保存領域、解析コードがないことを静的確認
- [ ] 公開先でDevToolsのNetworkを開き、ページ表示時に外部通信がないことを実機確認
- [ ] PC、iPhone、AndroidでGmail／標準メールアプリ／コピー動作を実機確認

上記の未チェック項目は公開先のURLと実機環境が必要なため、リリース後に確認してください。