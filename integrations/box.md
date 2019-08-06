# box

### 概要

Robotic Crowdでは、Box APIと連携する事で、「SaveFile」と「GetFile」アクションで、Boxからのファイル取得やBoxへのファイル保存が可能になります。

###  Boxとのコネクション作成

最初にRobotic Crowdの左側のサイドバーの「コネクション」をクリックします。

![](../.gitbook/assets/connection_click.png)

「コネクション」をクリックすると、APIとのコネクション一覧画面に移動します。右上の「アプリケーションを追加」をクリックします。

![](../.gitbook/assets/connection_ui.png)

右上の「アプリケーション追加」をクリックすると連携可能なアプリケーションのリストが表示されるので、その中から「Box」を選択します。

![](../.gitbook/assets/connection_list_box.png)

「Box」をクリックすると、Boxへのログイン画面が表示されます。コネクションに利用するアカウントを入力してください。

![](../.gitbook/assets/box_account.png)

ログインすると「Robotic Crowd」はユーザー様の代わりに、ユーザー様のBoxアカウントで管理している全てのフォルダとファイルに対する読み書きを行う権限を要求します。このアクセス権限を「Robotic Crowd」に与える事に、同意した上で「許可」をクリックしてください。

![](../.gitbook/assets/box_integration.png)

「許可」をクリックするとRobotic Crowdのコネクション画面にリダイレクトされます。「Box」とのコネクションが作成されていれば成功です。

![](../.gitbook/assets/set_box.png)