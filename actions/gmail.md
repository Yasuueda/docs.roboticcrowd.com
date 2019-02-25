# Gmail

Gmailを使ってメールを送受信します。

## GmailSend

### 概要

GmailSendは、GmailのAPIによりメールを送信します。この機能により、利用者は、自分のGmailアカウントからメールそ送信することができます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| to\* | 文字列 | メールの送信先アドレス | john.doe@example.com |
| subject\* | 文字列 | 送信するメールの件名 | Hello! John! |
| body\* | 文字列 | 送信するメールの本文 | Hi John, I'm very happy to send this mail to you. |
| provider\* | 文字列 | 送信に使うGmail ConnectionのProvider ID | gmail\_e7502c3b8b8147410ce2 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Boolean | 真理値 | APIのリクエストが、200で返却されたときにtrue | true |

### 使用例

```yaml
+gmail_send:
  action>: GmailSend
  to: 'john.doe@example.com'
  subject: 'Hello! John!'
  body: 'Hi John, I\'m very happy to send this mail to you.'
  provider: 'gmail_e7502c3b8b8147410ce2'
```

## 

## GmailGet

