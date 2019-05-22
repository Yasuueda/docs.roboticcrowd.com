# Slack

## SendSlackMessage

### 概要

SendSlackMessageは、SlackのAPIによりメッセージを送信するアクションです。この機能により、利用者は、自分のSlackアカウントから任意のチャンネルに、メッセージを送信することができます。

### アクション実行前の準備
```
このアクションを実行する為に、事前にSlack APIでアプリを作成しておく必要があります。

-アプリを作成
 Slack APIからアプリを作成します。その際に、通知したワークスペースとアプリの名前を指定します。

-API認証の追加
　アプリの管理画面のBasic Information にある features & functionality を設定します。Incoming Webhooks をONにしてください。
　次に、OAuth & Permissions のメニューからスコープ(使用できるAPIの機能)を設定します。今回は、Select Permission Scopes のところで chat:write:bot を追加します。
　このスコープを追加することにより、ワークスペースにbotがメッセージを送信する事を許可します。

-アプリのインストール
　アプリ管理画面の左カラムのメニューから Settings > Install App を選択し、ワークスペースにアプリをインストールします。
```

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
# 　{
#     "ok": true,
#     "channel": "CJHNQRXS6",
#     "ts": "1558414377.000400",
#     "message": {
#         "bot_id": "BJV6A9L48",
#         "type": "message",
#         "text": "\u3053\u3093\u306b\u3061\u306f",
#         "user": "UJV4T94GM",
#         "ts": "1558414377.000400"
#     }
# 　}
```
