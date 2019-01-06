# CloseBrowser

## 概要

CloseBrowserは、ブラウザを閉じます。ブラウザを閉じてセッションも切っておきたいときに使います。

## パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

## アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Boolean | 真理値 | 完了するとtrueとなる（エラーがなければ、常にtrue） | true |

## 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。実行前待機時間を短くして、実行後待ち時間を2秒に設定したもの。

```yaml
+close_browser_1:
  action>: CloseBrowser
  browser: +open_browser_1
  waitBefore: 10
  waitAfter: 2000
```

