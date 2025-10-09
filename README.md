# atcoder-lf-submit

## 概要
[AtCoder](https://atcoder.jp/)でCRLF (`\r\n`) ではなくLF (`\n`) で改行したソースコードを提出するボタンを追加します。
また、LFで改行した場合のコード長（Byte単位）をソースコードエディタの下に表示します。
特に512 KiBの提出制限を超過する場合はそのByte数を表示してボタンを押せなくします。

## 詳細
AtCoderのソースコードエディタは改行をLFとして処理する実装になっています。
しかし、ジャッジサーバーにソースコードを送信する過程で、ウェブブラウザが[HTMLの仕様](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#converting-an-entry-list-to-a-list-of-name-value-pairs)に従ってLFをCRLFに正規化してしまいます。
これは特に[コードゴルフ](https://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%BC%E3%83%89%E3%82%B4%E3%83%AB%E3%83%95)をする上で煩わしい挙動です。

この問題を解決するため、2018年に[AtCoder dos2unix UserScript](https://github.com/kmyk/atcoder-dos2unix-userscript)が作られました。
これはソースコード文字列のURLエンコード処理をJavaScriptで代替することでCRLF正規化を回避するものでした。

しかし、dos2unixは2025年に[AtCoderがソースコード提出時の認証を導入した](https://atcoder.jp/posts/1456)影響で動作しなくなりました。
既にGitHubリポジトリもアーカイブされていたため修正の見込みもありませんでした。

そこで、代わりにこのatcoder-lf-submitを作ることにしました。
より現代的かつシンプルな実装を目指して一から作り直し、コード長表示も追加しましたが、根本的なアイデアは同じです。
これまで利用させていただいたことと合わせて感謝申し上げます。

ちなみに、AtCoderのコードテストはジャッジへの提出とは異なり、元からJavaScriptで処理してLFのままテストサーバーへ送信する実装になっています。
そのため、コードテストページにLF用ボタンは追加せず、コード長表示のみとしています。

## 注意
AtCoderが導入した認証手段は[Cloudflare Turnstile](https://www.cloudflare.com/ja-jp/application-services/products/turnstile/)というものです。
atcoder-lf-submitは、ブラウザ上で正規に取得したTurnstileのトークンを含むフォームの内容をそのまま送信しています。
特にAtCoder運営の意に反する挙動はしていないと思いますが、各々自己責任でご利用ください。

## インストール
- Greasy Fork https://greasyfork.org/ja/scripts/551938-atcoder-lf-submit

## ソース
- https://github.com/dnek/atcoder-lf-submit/raw/main/atcoder-lf-submit.user.js
