### タスク概要

Yahoo!オークションの検索URLを、検索キーワードから動的に生成するクラス `UrlBuilder` を作成してください。
検索キーワードは日本語を想定しており、URLエンコードしたものをURLに挿入してURLを構築して返せるようにする

※URL構造の参考
https://auctions.yahoo.co.jp/closedsearch/closedsearch?p={encoded_keyword}&va={encoded_keyword}&b=1&n=50
	•	p=, va=：検索ワード
	•	b=1：ページ番号（1ページ目固定）
	•	n=50：表示件数（最大）

---

### 対象ファイル
`installer/src/flow/base/url_builder.py`

---

### 実装方針

- 使用ライブラリ：`urllib.parse`
- クラス名：`UrlBuilder`

---

### 要件（チェックリスト）
- [ ] UrlBuilder クラスが src/flow/base/url_builder.py に定義されている
- [ ] メソッドを実行して、キーワードをURLエンコードし「検索ワードを含んだ落札相場を調べるためURL」を返している
- [ ] スプレッドシートから取得した DataFrame をもとに、検索ワードを順に取り出してURL生成できる
- [ ] URLテンプレートにエンコードされたキーワードを挿入している
- [ ] 例外に対応できるように、try-except で補足し logger.error() にてエラー内容を出力する
- [ ] 異常発生時は raise により処理を停止させる仕様
- [ ] main.py から呼び出して、URL生成 → loggerできることを確認できる
