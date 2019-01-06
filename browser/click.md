# Click

## 概要

Clickは、ブラウザの内の指定の要素をクリックします。クリックに付随したダウンロードやダイアログの処理についてもここで設定します。ブラウザの接続先をアウトプットします。

## パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#submitBtn |
| confirm | 真理値 | ダイアログが表示されたらOKをクリックする。 | true \(default\) |
| type\_to\_confirm | 文字列 | confirmがtrueの時、ダイアログに文字を入力してから、OKをクリックする。 | null \(default\) |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitForDownload | 真理値 | このクリックでダウンロードが始まるので、ダウンロードの完了までこのアクション内で待機する。最大3分間待機する。 | false \(default\) |
| highResolution | 真理値 | ウィンドウを1280x720まで拡大してからクリックする。 | false \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

## アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

## 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。クリックで確認ダイアログが表示され、CSVダウンロードが始まることがわかっているので、そのダウンロードまで待つ。また、セレクタが見つからない場合は、エラーとして途中で終了するようにする。

```yaml
+click_1:
  action>: Click
  browser: +open_browser_1
  ingnoreError: false
  waitForDownload: true
  highResolution: true
```



