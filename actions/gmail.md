# Gmail

Gmailを使ってメールを送受信します。

## GmailSend

### 概要

GmailSendは、GmailのAPIによりメールを送信します。この機能により、利用者は、自分のGmailアカウントからメールを送信することができます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| provider\* | 文字列 | 送信に使うGmail ConnectionのProvider ID | gmail\_e7502c3b8b8147410ce2 |
| to\* | 文字列 | メールの送信先アドレス | john.doe@example.com |
| subject\* | 文字列 | 送信するメールの件名 | Hello! John! |
| body\* | 文字列 | 送信するメールの本文 | Hi John, I'm very happy to send this mail to you. |
| attachments | 配列・文字列 | 添付ファイル | アクション内で取得したファイルのパスを入力(使用例のアウトプット参照) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Boolean | 真理値 | APIのリクエストが、200で返却されたときにtrue | true |

### 使用例

```yaml
+gmail_send:
  action>: GmailSend
  provider: 'gmail_e7502c3b8b8147410ce2'
  to: 'john.doe@example.com'
  subject: 'Hello! John!'
  body: 'Hi John, I\'m very happy to send this mail to you.'
  attachments: '/Users/john/robotic-workflow/tmp/fe74887f-64b3-472e-aeda-90662ed1ab19/gdrive_204374d03b504b0efc7f/sample.pdf'
```

## GmailGet

### 概要

GmailGetは、Gmailのアカウントからメールを取得するアクションです。この機能により、利用者は、自分のGmailアカウントからメールを取得することができます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| query\* | 文字列 | 検索条件 | from:john.doe@example.com \(検索条件の詳細については[こちら](https://support.google.com/mail/answer/7190?hl=ja)参照してください。\) |
| provider\* | 文字列 | 送信に使うGmail ConnectionのProvider ID | gmail\_1234aaa |
| limit | 文字列 | 取得するメールの上限値 | 10\(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | 取得したメールオブジェクトの配列 | ※使用例のアウトプット参照 |

### 使用例

```yaml
+gmail_get_1:
  action>: GmailGet
  query: 'from:chan-shiro'
  provider: gmail_********************
  limit: 10
  #=> [
#   {
#     "id": "1234567890aaaaaa",
#     "subject": "ミーティング日程調整",
#     "to": "minna <minna@gmail.com>",
#     "cc": "aaa <aaa@gmail.com>",
#     "from": "bbb <bbb@gmail.com>",
#     "date": "2019-03-14T10:41:09.000Z",
#     "body": "ミーティングはXX月XX日XX時開始にしましょう。"
#   },...
# ]
```

