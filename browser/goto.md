# GoTo

## 概要

GoToは、ブラウザのアドレスバーに直接URLを入力して遷移させます。セッションを保ったままページ遷移させたり、URLを指定することで、サイト内の深い階層まで一気に遷移させるときなどに利用できます。

## パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| url\* | 文字列 | 遷移先URL | [https://yahoo.co.jp](https://yahoo.co.jp) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

## アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

## 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。実行前待機時間を短くして、実行後待ち時間を2秒に設定したもの。

```yaml
+go_to_1:
  action>: GoTo
  browser: +open_browser_1
  url: 'https://yahoo.co.jp'
  waitBefore: 10
  waitAfter: 2000
```

