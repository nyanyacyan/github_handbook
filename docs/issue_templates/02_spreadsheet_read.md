### タスク概要

Googleスプレッドシートから検索条件情報を読み込むための SpreadsheetReader クラスを作成してください。
読み込み形式は PandasのDataFrame を想定しています。

---

### 対象ファイル
`installer/src/flow/base/spreadsheet_read.py`

---

### GCP API認証について

この処理では、**Google Cloud Platform（GCP）で発行したサービスアカウントキー（JSON）を使用**してスプレッドシートにアクセスします。
認証情報（credentials.json）は `installer/config/` に配置し、`.gitignore` されています。

準備の手順はこちらを参考にしてください（閲覧権限・API有効化・キー発行まで）：
https://qiita.com/venect_qiita/items/4e0f00a70c1b57f948dd

---

### 実装方針

- 使用ライブラリ：`gspread`, `pandas`, `google-auth`
　- `pandas` は `import pandas as pd` として読み込んでください（プロジェクト全体で統一）

- クラス名：`SpreadsheetReader`

---


###  完了条件
- [ ] SpreadsheetReader クラスが src/elements/spreadsheet_reader.py に定義されている
- [ ] Google Sheets API を使ってスプレッドシートから読み込みができる
- [ ] get_search_conditions() 関数で検索条件が辞書リスト形式で取得できる
- [ ] データ取得時に pandas.DataFrame を使って取得している
- [ ] 認証情報（credentials.json）が config/ に存在し、.gitignore されている
- [ ] 例外に対応できるように、try-except で補足し logger.error() にてエラー内容を出力する
- [ ] 異常発生時は raise により処理を停止させる仕様
- [ ] main.py からインポート・呼び出して検索条件が取得できる状態になっている
