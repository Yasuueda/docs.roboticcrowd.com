# OpenBrowser

### 概要

OpenBrowserは、ほぼすべてのワークフローで利用されるアクションです。ブラウザ（Chromium）を起動して、指定されたウェブサイトを開きます。アウトプットは、起動したブラウザのウェブソケットアドレスになります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| url\* | 文字列 | 最初に開くウェブサイトのURL | https://yahoo.co.jp |
| lang | 文字列 | ブラウザの言語設定、ISO 639言語コード。 | en \(default\) |
| timeZone | 文字列 | ブラウザの場所設定、タイムゾーン。 | Etc/GMT \(default\) |
| userAgent | 文字列 | ブラウザのユーザーエージェント設定。 | HeadlessChrome \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

```yaml
+open_browser_1:
  action>: OpenBrowser
  url: 'https://yahoo.co.jp'
  lang: 'ja-JP'
  timeZone: 'Asia/Tokyo'
  userAgent: 'Robotic Crowd Agent'
```

