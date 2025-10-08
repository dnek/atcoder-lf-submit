# atcoder-lf-submit

## 概要
[AtCoder](https://atcoder.jp/)でCRLF (`\r\n`) ではなくLF (`\n`) で改行したソースコードを提出するボタンを追加します。
また、LFで改行した場合のコード長（Byte単位）をソースコードエディタの下に表示します。

## 詳細
AtCoderのソースコードエディタは改行をLFとして処理する実装になっています。
しかし、ジャッジサーバーにソースコードを送信する過程で、ウェブブラウザが[HTMLの仕様](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#converting-an-entry-list-to-a-list-of-name-value-pairs)に従ってLFをCRLFに正規化してしまいます。
これを回避するには、ソースコード文字列のURLエンコード処理をJavaScriptで代替する必要があります。

2018年にこれを実現する[AtCoder dos2unix UserScript](https://github.com/kmyk/atcoder-dos2unix-userscript)が作られましたが、2025年に[AtCoderがソースコード提出時の認証を導入した](https://atcoder.jp/posts/1456)影響で動作しなくなりました。

dos2unixは既に開発が終了していたため、代わりにこのatcoder-lf-submitを作りました。
より現代的かつシンプルな実装を目指して一から作り直し、コード長表示も追加しましたが、根本的なアイデアは同じです。
これまで利用させていただいたことと合わせて感謝申し上げます。

なお、AtCoderが導入した認証手段は[Cloudflare Turnstile](https://www.cloudflare.com/ja-jp/application-services/products/turnstile/)というものです。
atcoder-lf-submitは、ブラウザ上で正規に取得したTurnstileのトークンを含むフォームの内容をそのまま送信しています。
特にAtCoder運営の意に反する挙動はしていないと思いますが、各々自己責任でご利用ください。

また、コード長表示は提出ページ及びコードテストページに適用していますが、コードテストは元々JavaScriptで送信される実装になっておりCRLF正規化が行われないため、LF用ボタンは提出ページのみに追加しています。

## ソース
- https://github.com/dnek/atcoder-lf-submit/raw/main/atcoder-lf-submit.user.js
