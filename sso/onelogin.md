# OneLogin

このセクションでは、OneLoginを使って、Robotic Crowd に SSO する方法を説明いたします。**設定には、管理者権限が必要**ですので、情報システム部門の担当者に依頼してください。

### この作業のゴールと手順

#### 手順

OneLogin側で、以下の項目を設定します。

1. 新規 SAML アプリケーションの登録
2. 弊社担当者から指定されたACSの登録
3. 弊社担当者より指定された ACS URL Validator の登録
4. 証明書とログインURLのコピー

#### ゴール

上記手順を実際に行って以下の情報を取得して、弊社担当者までご連絡ください。

* X.509 Certificate
* SAML 2.0 Endpoint \(URL\)

では一つずつ手順を説明します。

### 新規 SAML アプリケーションの登録

管理者権限でログインして、管理画面に入ります。そこで、Add Apps を選択してください。

![&#x3000;](../.gitbook/assets/sukurnshotto2019-05-2481233.png)

続いて、アプリケーションを検索するところから、SAML Test を検索します。このSAML Testというアプリケーションを編集して Robotic Crowd 用のSAMLアプリケーションを作成します。

検索結果から、SAML Test Connector という物を選択してクリックします。

![](../.gitbook/assets/sukurnshotto2019-05-2474217.png)

すると、アプリケーション名や説明を記入する画面になるので、Display Name に Robotic Crowd、Rectangular icon / Square icon に次の画像をそれぞれ指定してください。Descriptionの部分には、社内向けの説明を記入してください。記入したら Save してください。

![Rectangular Icon](../.gitbook/assets/rclogo_rec_tcolor_1024.png)

![Square Icon](../.gitbook/assets/rclogocat_squ_tcolor_1024.png)

![&#x30A2;&#x30D7;&#x30EA;&#x60C5;&#x5831;&#x306E;&#x8A2D;&#x5B9A;](../.gitbook/assets/screen_shot_2019-07-03_at_14_57_47%20%281%29.png)

### ACSとACS URL Validatorを登録

Configurationタブをクリックして設定画面を開きます。ここで、ACSとACS URL Validatorを登録します。それぞれフォーマットは以下のようになっています。

| 項目 | 値 |
| :--- | :--- |
| Audience | https://console.roboticcrowd.com/ |
| Recipient | https://console.roboticcrowd.com/users/auth/saml/callback?domain=tutorial.co.jp |
| ACS | https://console.roboticcrowd.com/users/auth/saml/callback?domain=tutorial.co.jp |
| ACS URL Validator | ^https:\/\/console\.roboticcrowd\.com\/users\/auth\/saml\?domain=tutorial\.co\.jp$ |

![&#x5404;&#x7A2E;&#x8A2D;&#x5B9A;&#x9805;&#x76EE;](../.gitbook/assets/screen_shot_2019-07-03_at_14_57_54-2.png)

値は、営業担当より連絡いたします。tutorial.co.jpというドメインのところを、貴社組織ドメインに読み替えて設定してSaveしてください。

### 証明書とログインURLのコピー

この状態でSSOタブを開くと、各種値を取得することができます。まずは、SAML 2.0 Endpointをコピーしてください。

![](../.gitbook/assets/screen_shot_2019-07-03_at_14_58_07.png)

続いて、X.509 Certificateというところの下の "View Details" をクリックして証明書の詳細を開いてください。

![](../.gitbook/assets/screen_shot_2019-07-03_at_14_58_07%20%281%29.png)

クリック後に表示される画面から、証明書をコピーしてください。

![](../.gitbook/assets/screen_shot_2019-07-03_at_14_58_21.png)

上で取得した以下の情報を弊社担当者までおしらせください。データは、テキストで大丈夫です。

* SAML 2.0 Endpoint
* X.509 Certificate

