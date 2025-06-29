### タスク概要

Yahoo!オークションで取得した商品の情報を、以下の列に沿ってGoogleスプレッドシートへ書き込む処理を実装してください。

---

### 対象ファイル
`installer/src/flow/base/spreadsheet_writer.py`

---


###  実装方針

- 使用ライブラリ：`logging`, `gspread`
- クラス名：`SpreadsheetWriter`
- 処理は 1レコードずつ行単位で挿入


---


### 書き込み内容（列構成）
1. `date`：商品終了日付（`datetime.date` 型で記録）
2. `title`：商品タイトル（文字列）
3. `price`：落札価格（数値）
4. `ct`：商品名に含まれる「ct」から抽出された数値
5. `1ct_price`：単価（`price ÷ ct` の計算結果）
6. `image`：商品画像（URLリンク or スプレッドシートへの画像貼付け）

---

### 要件（チェックリスト）
- [ ] SpreadsheetWriter クラスがspreadsheet_writer.pyに定義されている
- [ ] 一度現在のスプシを読み込みNoneになっているA列（日付）セルを確認してから書き込む仕様
- [ ] worksheet.update(start_cell, list_of_lists)のようにリストを渡してスタートとなるセルを指定してupdateメソッドで書き込む
- [ ] `image` 列は、スプレッドシート上で実際に画像が見えるようにする（テキストURLではなく `=IMAGE("...")`）
- [ ] 例外に対応できるように、try-except で補足し logger.error() にてエラー内容を出力
- [ ] 異常発生時は raise により処理を停止
- [ ] main.py でのテスト呼び出しが可能な構成になっている

---

### テスト要件
- [ ] 特定の詳細ページURLを渡し、辞書形式で期待通りの値が返るか確認
- [ ] 異常系（価格なし／件名不正など）で logger.error() が記録されるか確認
- [ ] テストURL：https://auctions.yahoo.co.jp/jp/auction/w1188987840

### テスト用データ
- [ ] test_dataを書込用のデータリストへ変換してupdateを行う。（辞書の値をリストへ）

変換例：
[
"2025-06-27",
"ダイヤ ルース 0.500ct 鑑定書付き",
51700,
0.500,
84100,
"https://auctions.c.yimg.jp/images.auctions.yahoo.co.jp/image/dr000/auc0106/user/5ec807c934150c37fea5b1cda6cdb4938dea1bcdd982696a3d9c90b59c549314/i-img1200x849-17500560233691ls9baa33.jpg"
]

test_data = [
    {
        "date": "2025-06-27",
        "title": "ダイヤ ルース 0.500ct 鑑定書付き",
        "price": 51700,
        "ct": 0.500,
        "1ct_price": 84100,
        "image": "https://auctions.c.yimg.jp/images.auctions.yahoo.co.jp/image/dr000/auc0106/user/5ec807c934150c37fea5b1cda6cdb4938dea1bcdd982696a3d9c90b59c549314/i-img1200x849-17500560233691ls9baa33.jpg"
    },
    {
        "date": "2025-06-28",
        "title": "ダイヤモンドルース 0.200ct 新品",
        "price": 20000,
        "ct": 0.200,
        "1ct_price": 32600,
        "image": "https://auctions.c.yimg.jp/images.auctions.yahoo.co.jp/image/dr000/auc0106/user/5ec807c934150c37fea5b1cda6cdb4938dea1bcdd982696a3d9c90b59c549314/i-img1200x849-17500560233691ls9baa33.jpg"
    }
]
