# Slack APPの設定

### 概要

Robotic Crowdでは、Slackと連携させる事により、アクション内でロボット(bot)に自動でメッセージを送信させたり、エラーをSlackに通知させる事が出来ます。
Robotic CrowdでSlack関連の機能を使用する為に、事前にSlack APIでアプリを作成し、幾つか設定をしておく必要があります。

### アプリの作成

最初に、SlackAPIでアプリを作成します。https://api.slack.com/apps
「your app」をクリックし、アプリの名前とアプリを使用したいワークスペースを選択してください。

### クライアントIDとクライアントシークレットの取得

アプリを作成すると、クライアントIDとクライアントシークレットが発行されます。このクライアントIDとクライアントシークレットを、Robotic-Crowdでコネクションを追加する際に使用します。

### リダイレクトURLの設定

続いて、OAuth & Permissionsの項目をクリックし、Redirect URLsの箇所に![](http://localhost:3000/connections/slack/callback)を入力してください。




