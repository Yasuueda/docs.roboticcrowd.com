# Google Analytics

Google Analyticsを操作するアクション一覧です。

## GetReport

### 概要

GetReportは、レポートを作成するアクションです。パラメーターを設定することで、カスタマイズされたレポートを作成することができます。レポートの対象期間は、startDate、endDateで設定します。取得したい値は、metricsで指定します。ページ別、ブラウザ別などの分析軸を設定したい場合は、dimensionsを入力してください。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| startDate\* | 文字列 | リクエスト期間の開始日付 | 2019-04-01 |
| endDate\* | 文字列 | リクエスト期間の終了日付 | 2019-04-30 |
| metrics\* | 文字列 | 指標(定量化されたデータ) | ga:users, ga:sessions |
| dimensions | 文字列 | ディメンション(データの属性) | ga:browser |

#### 補足: 入力フォーマット

```
すべての指標がすべてのディメンションと組み合わせることができるわけではありません。ディメンションと指標は、同じ階層のもの同士を組み合わせる必要があります。たとえば、「セッション」はセッションの指標なので、同じセッションレベルの「参照元」や「市区町村」などのディメンションと組み合わせます。「セッション」を「ページ」などのヒットレベルのディメンションと組み合わせても意味はありません。ディメンションと指標の有効な組み合わせについては、下記に記載したディメンションと指標の組み合わせの具体例を参照してください。

-①新規ユーザー数を計測したい場合
metrics   : ga:newUsers
dimensions: ga:userType

-②任意の市町村区における平均セッション時間を計測したい場合
metrics   : ga:session
dimensions: ga:city

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
# => {
#     "reports": [
#         {
#             "columnHeader": {
#                 "metricHeader": {
#                     "metricHeaderEntries": [
#                         {
#                             "name": "ga:users",
#                             "type": "INTEGER"
#                         }
#                     ]
#                 }
#             },
#             "data": {
#                 "isDataGolden": true,
#                 "maximums": [
#                     {
#                         "values": [
#                             "98"
#                         ]
#                     }
#                 ],
#                 "minimums": [
#                     {
#                         "values": [
#                             "98"
#                         ]
#                     }
#                 ],
#                 "rowCount": 1,
#                 "rows": [
#                     {
#                         "metrics": [
#                             {
#                                 "values": [
#                                     "98"
#                                 ]
#                             }
#                         ]
#                     }
#                 ],
#                 "totals": [
#                     {
#                         "values": [
#                             "98"
#                         ]
#                     }
#                 ]
#             }
#         }
#     ]
# }
```