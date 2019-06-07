# Slack APPの設定

### 概要

Robotic Crowdでは、Slackと連携させる事により、アクション内でロボット(bot)からの自動メッセージ送信や、エラー通知が可能になります。
Slack関連の機能を使用する為に、事前にSlack APIでアプリを作成し幾つか設定をしておく必要があります。

### Slack APPの作成

最初に、次のリンクからSlack APPを作成します。https://api.slack.com/

右上の「Your Apps」をクリックすると、アプリ作成画面に遷移します。

![](../.gitbook/assets/slack_1.png)

アプリ作成画面から「Create New App」をクリックします。

![](../.gitbook/assets/slack_2.png)

表示されたダイアログの「App Name」にアプリの名前、「Development Slack Workspace」に、使用したいワークスペースを選択してください。

![](../.gitbook/assets/slack_3.png)

### Client IDとClient Secretの取得

アプリを作成すると「Basic Information」が表示され、その中に、「App Credentials」と言うセクションがあります。その中の、「Client ID」と「Client Secret」を Robotic CrowdでSlackコネクションを追加する際に使用します。

![](../.gitbook/assets/slack_4.png)

### Redirect URLsの設定

次に、「OAuth & Permissions」の項目をクリックし、「Redirect URLs」の箇所に下記のURLを入力してください。
https://console.roboticcrowd.com/connections/slack/callback

![](../.gitbook/assets/slack_5.png)

## Robotic Crowdでのコネクション連携

Slack APIでの設定が完了した後は、Robotic Crowdでコネクション連携を行います。コネクション追加画面でSlackを選択します。

![](../.gitbook/assets/slack_6.png)

表示されるダイアログに、設定した「Client ID」と「Client Secret」を入力します。

![](../.gitbook/assets/slack_7.png)

「Client ID」と「Client Secret」を入力すると、 Slack APPの認証画面が表示されるので、インストールをクリックしてください。

![](../.gitbook/assets/slack_8.png)

連携が成功すると Robotic Crowd のコネクションにアプリが追加されます。これでワークフロー内で、Slackに関係するアクションが使用可能になります。

![](../.gitbook/assets/slack_9.png)
