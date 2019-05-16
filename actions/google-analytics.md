# Google Analytics

Google Analyticsを操作するアクション一覧です。

## GetReport

### 概要

GetReportは、レポートを作成するアクションです。パラメーターを設定することで、カスタマイズされたレポートを作成することができます。レポートの対象期間は、startDate、endDateで設定します。取得したい値は、metricsで指定します。ページ別、ブラウザ別などの分析軸を設定したい場合は、dimensionsで指定します。。リクエストで返されるディメンションまたは指標を制限したい場合は、filterで指定します。返却されるレスポンスはデフォルトで最大1000行になっています。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| startDate\* | 文字列 | リクエスト期間の開始日付 | 2019-04-01 |
| endDate\* | 文字列 | リクエスト期間の終了日付 | 2019-04-30 |
| metrics\* | 文字列 | 指標(定量化されたデータ) | ga:users, ga:sessions |
| dimensions | 文字列 | ディメンション(データの属性) | ga:browser |
| filter | 文字列　| リクエストで返されるデータを制限するディメンションまたは指標のフィルタ | ga:browser==Chrome |

#### 補足: 入力フォーマット

```
すべての指標がすべてのディメンションと組み合わせることができるわけではありません。ディメンションと指標は、同じ階層のもの同士を組み合わせる必要があります。たとえば、「セッション」はセッションの指標なので、同じセッションレベルの「参照元」や「市区町村」などのディメンションと組み合わせます。「セッション」を「ページ」などのヒットレベルのディメンションと組み合わせても意味はありません。ディメンションと指標の有効な組み合わせについては、下記に記載したディメンションと指標の組み合わせの具体例を参照してください。

-①新規ユーザーのセッション数を計測したい場合
metrics   : ga:sessions
dimensions: ga:userType
filters : ga:userType==New Visitor

-②任意の市町村区における平均セッション時間を計測したい場合
metrics   : ga:sessions
dimensions: ga:city
filters : ga:city==cityName

dimensionsとmetrixに関する詳細情報は下記のURLを参考にしてください。
https://developers.google.com/analytics/devguides/reporting/core/dimsmets
```

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | オブジェクト | JSONレスポンス | ※使用例のアウトプット参照 |

### 使用例
```yaml
action>: GetGAReport
  startDate: 2019-04-01
  endDate: 2019-04-30
  metrics: ['ga:users', 'ga:sessions']
  dimensions: ['ga:browser']
  filters: ['ga:browser==Chrome']
# => {
#   "reports": [
#     {
#       "columnHeader": {
#         "dimensions": [
#           "ga:browser"
#         ],
#         "metricHeader": {
#           "metricHeaderEntries": [
#             {
#               "name": "ga:sessions",
#               "type": "INTEGER"
#             }
#           ]
#         }
#       },
#       "data": {
#         "rows": [
#           {
#             "dimensions": [
#               "Chrome"
#             ],
#             "metrics": [
#               {
#                 "values": [
#                   "4660"
#                 ]
#               }
#             ]
#           }
#         ],
#         "totals": [
#           {
#             "values": [
#               "4660"
#             ]
#           }
#         ],
#         "rowCount": 1,
#         "minimums": [
#           {
#             "values": [
#               "4660"
#             ]
#           }
#         ],
#         "maximums": [
#           {
#             "values": [
#               "4660"
#             ]
#           }
#         ],
#         "isDataGolden": true
#       }
#     }
#   ]
# }
```