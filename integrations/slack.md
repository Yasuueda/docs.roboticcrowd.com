# Slack APPの設定

### 概要

Robotic Crowdでは、Slackと連携させる事により、Slackを用いたアクションでロボット(bot)に自動でメッセージを送信させたり、エラーをSlackに送信させる事が出来ます。
実際に、Robotic CrowdでSlack関連の機能を使用する為には、Slack APIでアプリを作成し、いくつか設定をしておく必要があります。

### アプリの作成

Slack API(https://api.slack.com/apps) からアプリを作成します。その際に、使用したいワークスペースとアプリの名前を指定します。
App Nameには好きな名前を、Development Slack Workspaceには通知したいワークスペースを入力してください。

![](../.gitbook/assets/createapp.png)

### Webhooksの設定

アプリの管理画面のBasic Information にある features & functionality を設定します。Incoming Webhooks をONにしてください。

![](../.gitbook/assets/features.png)

### Scopeの設定

スコープとは、APIで使用出来る機能を指定するものです。OAuth & Permissions のメニューからスコープ(使用できるAPIの機能)を設定します。今回は、Select Permission Scopes のところで chat:write:bot を追加します。このスコープを追加することにより、ワークスペースにbotがメッセージを送信する事を許可します。

![](../.gitbook/assets/scope.png)

### アプリのインストール

アプリ管理画面の左カラムのメニューから Settings > Install App を選択し、ワークスペースにアプリをインストールします。
