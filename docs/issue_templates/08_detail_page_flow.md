### タスク概要

Yahoo!オークションの各商品詳細ページに遷移した際、件名／価格／画像URL／カラット情報の抽出などを行う処理フローを一括管理するクラスを作成してください。
このクラスは、selenium.py や number_calculator.py などの基底機能を組み合わせて使用する中間レイヤーのフロー制御用です。

---

### 対象ファイル
`installer/src/flow/detail_page_flow.py`

---

### 実装方針

- 使用ライブラリ：`logging`
- クラス名：`DetailPageFlow`

---

### 主な処理内容（ステップ）
1.	URLを受け取りサイトにアクセス
2.	各要素を取得：
  - 件名
  - 価格
  - 画像URL（1枚目のみ）
  - カラット数（件名から抽出）
  - 単価（PriceCalculatorで計算）
3.	画像を表示させるための値を修正 ※別途掲載
4. 	辞書用データに
5.	抽出結果を以下の形式で返却
```
# 抽出結果、出力イメージ
[
    {
        "date": "2025-06-27",
        "title": "ダイヤ ルース 0.500ct 鑑定書付き",
        "price": 51700,
        "ct": 0.500,
        "1ct_price": 84100,
        "image": '=IMAGE("https://auctions.c.yimg.jp/images.auctions.yahoo.co.jp/image/dr000/auc0106/user/5ec807c934150c37fea5b1cda6cdb4938dea1bcdd982696a3d9c90b59c549314/i-img1200x849-17500560233691ls9baa33.jpg", 4, 80, 80)'
    },
    {
        "date": "2025-06-28",
        "title": "ダイヤモンドルース 0.200ct 新品",
        "price": 20000,
        "ct": 0.200,
        "1ct_price": 32600,
        "image": '=IMAGE("https://auctions.c.yimg.jp/images.auctions.yahoo.co.jp/image/dr000/auc0106/user/5ec807c934150c37fea5b1cda6cdb4938dea1bcdd982696a3d9c90b59c549314/i-img1200x849-17500560233691ls9baa33.jpg", 4, 80, 80)'
    }
]
```

---

### 画像をスプシに掲載させるため　辞書のimage(key)に入れる値の加工
取得した画像URLをスプシに適正な大きさに加工するため、また表示させるために下記のFormatを利用して
imageの値に入れてください。

``` python
f' = IMAGE("{image_url}", 4, 80, 80)'
```
出力例：
        "image": '=IMAGE("https://auctions.c.yimg.jp/images.auctions.yahoo.co.jp/image/dr000/auc0106/user/5ec807c934150c37fea5b1cda6cdb4938dea1bcdd982696a3d9c90b59c549314/i-img1200x849-17500560233691ls9baa33.jpg", 4, 80, 80)'

---

### 要件（チェックリスト）
- [ ] DetailPageFlow クラスが detail_page_flow.py に定義されている
- [ ] Selenium, PriceCalculator, ImageDownloader などを利用している
- [ ] loggerにて各ステップの処理ログが記録されている
- [ ] 例外に対応できるように、try-except で補足し logger.error() にてエラー内容を出力
- [ ] 異常発生時は raise により処理を停止
- [ ] main.py でのテスト呼び出しが可能な構成になっている

---

### テスト要件
- [ ] 特定の詳細ページURLを渡し、辞書形式で期待通りの値が返るか確認
- [ ] 異常系（価格なし／件名不正など）で logger.error() が記録されるか確認
- [ ] テストURL：https://auctions.yahoo.co.jp/jp/auction/w1188987840
