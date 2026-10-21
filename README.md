# Tools Personal

個人向けのシンプルなWebツールをまとめるサイトです。トップページから各ツールへ移動できます。

## 公開ページ

- ツール一覧: https://teruluce.github.io/duck-address-generator/
- Duckアドレス生成ツール: https://teruluce.github.io/duck-address-generator/duckmail/

## Duckアドレス生成ツール

DuckDuckGo Email ProtectionのDuckアドレスから、自分でメールを送るときに使う宛先形式をブラウザ内で作成する非公式ツールです。

1. 送信先（相手）のメールアドレスを入力します（例：`hoge@gmail.com`）。
2. 自分のDuckアドレスを入力します（例：`my-duck` または `my-duck@duck.com`）。
3. 「アドレスを生成」を押します。
4. 生成された宛先をコピーするか、Gmailまたは端末の標準メールアプリを開きます。

例：`hoge@gmail.com` + `my-duck` → `hoge_at_gmail.com_my-duck@duck.com`

## プライバシーと技術的な方針

- 入力内容を外部サーバーへ送信しません。
- 入力内容を `localStorage`、Cookie、その他のブラウザ保存領域に保存しません。
- アクセス解析、外部ライブラリ、CDN、外部フォントを使用しません。
- Content Security Policy（CSP）で外部接続を制限しています。
- Gmailやメールアプリを開く操作を実行した場合、生成された宛先は選択されたサービス／アプリに渡されます。
- このツールはメールそのものを送信しません。送信内容の作成と送信は利用者がメールアプリで行います。

## 確認状況

コード上の静的確認と、公開後の実機確認は区別します。公開後はページ表示時に外部通信がないことをブラウザの開発者ツールで確認し、PC・iPhone・Androidでコピーおよびメールアプリ起動をテストしてください。
