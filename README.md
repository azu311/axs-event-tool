# AXS イベント登録サポートツール

VOREAS の AXS BackOffice にイベントを登録する際、登録マニュアルに沿った各項目（名称・参照ID・シーズン/イベントカテゴリー・各種日時・ETicket Format など）を自動生成し、項目ごとのコピーと Excel 出力ができる単一ページのツールです。

## 使い方

`index.html` をブラウザで開く（または GitHub Pages の公開URLにアクセスする）だけで動作します。サーバーやビルドは不要です。

1. 左側に開催情報（開催日・イベント名・シーズン区分・座席タイプ・会場・時間など）を入力
2. 右側に登録項目が自動生成される
3. 「コピー」で個別転記、「サマリーを全コピー」で一括コピー、「Excelで出力」で `.xlsx` をダウンロード

入力内容はブラウザ内でのみ処理され、外部に送信・保存されません。

## ファイル構成

```
.
├── index.html                 ツール本体
├── vendor/
│   └── xlsx.full.min.js        Excel出力用ライブラリ（SheetJS, 同梱）
└── README.md
```

外部CDNに依存しないよう、Excel出力ライブラリ（SheetJS 0.18.5）をリポジトリ内に同梱しています。オフラインでも動作します。

## GitHub Pages での公開手順

1. このリポジトリを GitHub にプッシュ
2. リポジトリの **Settings → Pages** を開く
3. **Build and deployment → Source** を「Deploy from a branch」にする
4. Branch を `main`、フォルダを `/ (root)` に設定して Save
5. 数分後、`https://<ユーザー名>.github.io/<リポジトリ名>/` で公開される

## メンテナンス

固定値（FlashSeatsオーナー、決済コード `VLEAGUE`、配信日時、注意事項など）は登録マニュアル基準で `index.html` 内に直接記述しています。運用ルールが変わった場合は該当箇所を編集してください。

- シーズン/イベントカテゴリーの判定ロジック … `index.html` 内 `categories()` 関数
- ETicket Format の生成 … `eticketText()` 関数
- 固定値・出力項目 … 各 `data-t` 付き要素および `buildRows()` 関数

## 注意

このツールには社内の登録ルールや連絡先が含まれます。GitHub Pages で公開した場合、URLを知っていれば誰でも閲覧できます。公開範囲を限定したい場合は、リポジトリを Private にしたうえで Pages のアクセス制限を利用するか、社内環境での配布を検討してください。
