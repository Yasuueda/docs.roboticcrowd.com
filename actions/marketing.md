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

## GetSearchAnalytics

### 概要

GetSearchAnalyticsは、Google Search Consoleで管理しているプロパティの検索パフォーマンスデータを取得するアクションです。返却されるレスポンスはデフォルトで最大1000行です。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| provider\* | 文字列 | 利用するコネクション（Search Console）のプロバイダーID | searchconsole\_e7502c3b8b8147410ce2 |
| siteUrl\* | 文字列 | Google Search Consoleに登録しているプロパティのURLまたはドメイン名 | roboticcrowd.com |
| startDate\* | 文字列 | リクエスト期間の開始日付 | 2019-06-01 |
| endDate\* | 文字列 | リクエスト期間の終了日付 | 2019-06-07 |
| dimensions | 配列 | 取得するデータの種類 | ['query', 'page'] |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | オブジェクト | JSONレスポンス | ※使用例のアウトプット参照 |

### 使用例

```yaml
action>: GetSearchAnalytics
  provider: searchconsole_********************
  siteUrl: 'roboticcrowd.com'
  startDate: '2019-06-01'
  endDate: '2019-06-07'
  dimensions: ['query', 'page']
# => {
#  "rows": [
#   {
#    "keys": [
#     "robotic crowd",
#     "https://roboticcrowd.com/"
#    ],
#    "clicks": 109.0,
#    "impressions": 181.0,
#    "ctr": 0.6022099447513812,
#    "position": 1.0055248618784531
#   },
#   {
#    "keys": [
#     "ロボティッククラウド",
#     "https://roboticcrowd.com/"
#    ],
#    "clicks": 32.0,
#    "impressions": 44.0,
#    "ctr": 0.7272727272727273,
#    "position": 1.0
#   },
#  ],
#  ...
#  "responseAggregationType": "byPage"
# }

```
