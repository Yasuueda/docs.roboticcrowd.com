# Marketing

マーケティングに関するアクション一覧です。

## GetGAReport

### 概要

GetGAReportは、レポートを取得するアクションです。パラメーターを設定することで、カスタマイズされたレポートを作成することができます。レポートの対象期間は、startDate、endDateで設定します。取得したい値は、metricsで選択します。ページ別、ブラウザ別などの分析軸を設定したい場合は、dimensionsで指定します。リクエストで返されるディメンションまたは指標を制限したい場合は、filtersで指定します。返却されるレスポンスはデフォルトで最大1000行です。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| provider\* | 文字列 | google analyticsからデータを取得するのに必要なプロバイダーID | ga\_e7502c3b8b8147410ce2 |
| viewId\* | 文字列 | ユーザーID | 12345678 |
| startDate\* | 文字列 | リクエスト期間の開始日付 | 2019-04-01 |
| endDate\* | 文字列 | リクエスト期間の終了日付 | 2019-04-30 |
| metrics | 文字列 | 指標\(定量化されたデータ\)。カンマ区切りで10個まで指定可能。デフォルト ga:visits | ga:users, ga:sessions |
| dimensions | 文字列 | ディメンション\(データの属性\)。カンマ区切りで7個まで指定可能 | ga:browser |
| filters | 文字列 | リクエストで返されるデータを制限するディメンションまたは指標のフィルタ | ga:browser==Chrome |

#### 補足: 入力フォーマット

すべての指標がすべてのディメンションと組み合わせることができるわけではありません。ディメンションと指標は、同じ階層のもの同士を組み合わせる必要があります。たとえば、「セッション」はセッションの指標なので、同じセッションレベルの「参照元」や「市区町村」などのディメンションと組み合わせます。「セッション」を「ページ」などのヒットレベルのディメンションと組み合わせても意味はありません。ディメンションと指標の有効な組み合わせについては、下記に記載したディメンションと指標の組み合わせの具体例を参照してください。

**①新規ユーザーのセッション数を計測したい場合**

```text
action>: GetGAReport
  provider: ga_xxxxxxx
  viewId: 11110000
  metrics: ga:sessions
  dimensions: ga:userType
  filters: ga:userType==New Visitor
```

**②任意の市町村区における平均セッション時間を計測したい場合**

```text
action>: GetGAReport
  provider: ga_xxxxxx
  viewId: 11110000
  metrics: ga:sessions
  dimensions: ga:city
  filters: ga:city==cityName
```

dimensionsとmetrixに関する詳細情報は下記のURLを参考にしてください。 [https://developers.google.com/analytics/devguides/reporting/core/dimsmets](https://developers.google.com/analytics/devguides/reporting/core/dimsmets)

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | オブジェクト | JSONレスポンス | ※使用例のアウトプット参照 |

### 使用例

```yaml
action>: GetGAReport
  provider: ga_xxxxxxxx
  viewId: 1234567890
  startDate: '2019-04-01'
  endDate: '2019-04-30'
  metrics: 'ga:users,ga:sessions'
  dimensions: 'ga:browser'
# => {
# "reports": [
#    {
#      "columnHeader": {
#        "dimensions": [
#          "ga:browser"
#        ],
#        "metricHeader": {
#          "metricHeaderEntries": [
#            {
#              "name": "ga:users",
#              "type": "INTEGER"
#            },
#            {
#              "name": "ga:sessions",
#              "type": "INTEGER"
#            }
#          ]
#        }
#      },
#      "data": {
#        "rows": [
#          {
#            "dimensions": [
#              "Chrome"
#            ],
#            "metrics": [
#              {
#                "values": [
#                  "3229",
#                  "4660"
#                ]
#              }
#            ]
#          },
#          {
#            "dimensions": [
#              "Firefox"
#            ],
#            "metrics": [
#              {
#                "values": [
#                  "360",
#                  "480"
#                ]
#              }
#            ]
#          },
#          {
#            "dimensions": [
#              "Internet Explorer"
#            ],
#            "metrics": [
#              {
#                "values": [
#                  "2402",
#                  "3149"
#                ]
#              }
#            ]
#          },
#        ],
#        "totals": [
#          {
#            "values": [
#              "7212",
#              "9981"
#            ]
#          }
#        ],
#        "rowCount": 16,
#        "minimums": [
#          {
#            "values": [
#              "1",
#              "1"
#            ]
#          }
#        ],
#        "maximums": [
#          {
#            "values": [
#              "3229",
#              "4660"
#            ]
#          }
#        ],
#        "isDataGolden": true
#      }
#    }
#  ]
# }
```

## GetAdReport

### 概要

GetAdReportアクションは、Google広告からレポートを取得するアクションです。広告キャンペーン全体の掲載結果データのレポートを取得したり、広告が表示されるきっかけとなった検索語句などに絞ってデータを取得する事が出来ます。レポートを取得する為に、Google広告アカウントの「お客様ID」が必要になります。またコネクション作成時に、クライアントセンター(MCC)アカウントで連携した場合は、クライアントセンター(MCC)アカウントの「お客様ID」を入力する必要があります。「お客様ID」は下記の場所に記載されています。
取得したいデータの指定は、「Google Ads Query Language」という形式で入力する必要があります。セクション毎に取得したいデータを設定する事で様々な組み合わせのデータが取得可能です。

![](../.gitbook/assets/customerID.png)

### Google広告アカウントの階層構造


### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| customer_id\* | 文字列 | Google Adsからデータを取得するのに必要なお客様ID | 123456789 |
| manager_id | 文字列 | MCCアカウントでアクションを利用する場合、このパラメーターにMCCアカウントのお客様IDを入力します。 | 123456780 |
| query\* | 文字列 | 取得したいレポートを「Google Ads Query Language」で入力します。 | ※使用例の入力例を参照 |

#### 補足: Google Ads Query Languageパラメーターの入力フォーマット

```
-SELECT(必須)
取得したいデータ項目を入力してください。このパラメーターでは、Segment/Metrics/Customerなどフィールド毎に取得したいデータ項目を指定します。
設定可能な全てのフィールドから、取得したいデータを入力し全てにリクエストを送る事も可能です。

(例)
Resource fields
-campaign.name
-campaign.status

Segment fields
-ad_group.name

Metrics fields
-metrics.impressions

-FROM(必須)
SELECTで指定したデータを取得するリソースを選択します。一つのリソースしか選択する事が出来ません。

(例)
campaign
customer
ad_group

-WHERE(オプション)
条件を指定する事で取得したいデータをフィルタリングする事が可能です。複数の条件を指定する事も可能です。

(例)
segments.device = MOBILE
segments.date DURING LAST_30_DAYS
metrics.impressions > 0

-ORDER_BY(オプション)
返却されるデータの順番を、指定した条件で並び替える事が出来ます。取得したデータ毎に条件を指定し、各データ毎に表示する順番を指定する事が出来ます。

(例)
metrics.clicks ASC
metrics.impressions DESC

-LIMIT(オプション)
APIから返却されるデータの数を、数値で直接指定する事が出来ます。

(例)
LIMIT 100

-PARAMETERS(オプション)
この項目では管理しているGoogle広告のメタパラメータを指定する事が出来ます。
現在APIで使用できるメタパラメータは「include_drafts」の一つだけとなっており、デフォルトでは「False」になっています。
管理しているGoogle広告アカウントに下書き状態の広告が存在する場合、「True」に設定する事で下書き状態の広告に関するデータを取得する事が出来ます。

(例)
include_drafts=true
```

このアクションで使用できるパラメーターに関する詳細情報は下記のURLを参考にしてください。
[https://developers.google.com/google-ads/api/docs/query/structure](https://developers.google.com/google-ads/api/docs/query/structure)

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
|  |  |  | ※使用例のアウトプット参照 |

### 使用例

```yaml
action>: GetAdReport
  customer_id: 123456789
  manager_id: 123456780
  query:  SELECT campaign.name, campaign.status, segments.device, metrics.impressions, metrics.clicks,
                 metrics.ctr, metrics.average_cpc, metrics.cost_micros
          FROM campaign
          WHERE segments.date DURING LAST_30_DAYS

```