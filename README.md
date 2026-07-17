# 憲法クエスト

夏休み課題「日本国憲法条文」の全288空欄を学習する、独立したオフライン対応PWAです。既存の定期テスト用`memorization_game`とは、保存キー・キャッシュ・アプリ名・データを共有しません。

## 起動

`index.html`をダブルクリックすると、そのままブラウザで起動できます。CSS・全288問のデータ・JavaScriptを`index.html`内へ埋め込んだ単一ファイル版なので、ローカルサーバーは不要です。

PWAのインストールやService Workerによるオフラインキャッシュまで確認するときだけ、`start-game.bat`を使ってください。これらのブラウザ機能は`file://`では動作せず、GitHub Pages（HTTPS）またはローカルサーバー上で有効になります。

## 収録内容

- 課題PDFの空欄: 288件
- 公式条文と照合した空欄: 280件
- 課題独自の概要空欄: 8件
- 未解決: 0件
- 章・エリア: 13

正解は、課題PDFの文字レイヤーを直接抽出し、衆議院「日本国憲法」の全文へ前後文脈を照合して復元しています。復元全文が一致しない空欄は確定しない設計です。

公式出典: https://www.shugiin.go.jp/internet/itdb_annai.nsf/html/statics/shiryo/dl-constitution.htm

## 学習モード

- 意味つなぎ（4択）
- 条文復元パズル
- 一部ヒント入力
- 見出しなしの本番入力
- 条文連続復元
- 章ボス
- 15分・30問の本番模試

間違えた空欄は3〜6問後に再出題され、弱点・XP・星・模試履歴は`constitutionQuestProgressV1`へ保存されます。

## データ再生成

Python 3と`pdfplumber`が必要です。

```powershell
py -3 tools\build_all.py
```

生成物:

- `data/*.json`: アプリ用データ
- `data/data-bundle.js`: `index.html`直開き用の結合データ
- `index.html`: CSS・データ・ロジックを埋め込んだ直開き／GitHub Pages共通版
- `reports/answer_key_review.csv`: 人間確認用正答一覧
- `reports/unresolved_blanks.csv`: 未解決一覧
- `reports/reconstruction_report.md`: 全文復元結果
- `reports/validation_report.md`: 最終検証結果

## 公開

`constitution-quest`フォルダを独立したGitHubリポジトリへ配置し、GitHub Pagesでルートを公開できます。公開時の追加ビルドや外部APIは不要です。
