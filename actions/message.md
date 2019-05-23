# Message

メールやメッセージを送受信します。

## GmailSend

### 概要

GmailSendは、GmailのAPIによりメールを送信します。この機能により、利用者は、自分のGmailアカウントからメールを送信することができます。

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

## GmailGet

### 概要

GmailGetは、Gmailのアカウントからメールを取得するアクションです。この機能により、利用者は、自分のGmailアカウントからメールを取得することができます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| query\* | 文字列 | 検索条件 | from:john.doe@example.com<br>(検索条件の詳細については[こちら](https://support.google.com/mail/answer/7190?hl=ja)参照してください。) |
| provider\* | 文字列 | 送信に使うGmail ConnectionのProvider ID | gmail_1234aaa |
| limit | 文字列 | 取得するメールの上限値 | 10(default) |

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

## SendSlackMessage

### 概要

SendSlackMessageは、SlackのAPIによりメッセージを送信するアクションです。この機能により、任意のチャンネルに、botからメッセージを送信することができます。

### アクション実行前の準備

このアクションを実行する為に、事前にSlack APIでアプリを作成しておく必要があります。
詳しくは、こちら（[Slack APPの設定](../integrations/slack.md)）の記事をご覧ください。


### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| provider\* | 文字列 | 送信に使うSlack ConnectionのProvider ID | slack\_******************** |
| channel\* | 文字列 | メッセージの送信先チャンネル | #general |
| text\* | 文字列 | 送信するメッセージ | Hello,World! |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | オブジェクト | JSONレスポンス | ※使用例のアウトプット参照 |

### 使用例

```yaml
+send_slack_message:
  action>: SendSlackMessage
  provider: slack_********************
  channel: '#general'
  text: 'Hello, World!'
#   {
#   "ok": true,
#   "channel": "CJJ0FHDTM",
#   "ts": "1558588475.001100",
#   "message": {
#     "type": "message",
#     "subtype": "bot_message",
#     "text": "Hello, World!",
#     "ts": "1558588475.001100",
#     "username": "tutorial-test",
#     "bot_id": "BJVC9SCN9"
#   },
#   "response_metadata": {
#     "scopes": [
#       "bot",
#       "users.profile:read",
#       "chat:write:bot"
#     ],
#     "acceptedScopes": [
#       "chat:write:bot"
#     ]
#   }
# }
```