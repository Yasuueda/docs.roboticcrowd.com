# Google Analytics

Google Analyticsを操作するアクション一覧です。

## GetReport

### 概要

GetReportは、レポートを作成するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| startDate | 文字列 | 対象期間の開始日付 |  |
| endDate | 文字列 | 対象期間の終了日付 |  |
| metrics\* | オブジェクト | 指標 |  |
| dimensions\* | オブジェクト | ディメンション |  |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | オブジェクト | JSONレスポンス | ※使用例のアウトプット参照 |

### 使用例
```yaml


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


<!-- 文字列が入るものが「Dimensions（ディメンション）」で、数字が入るものが「Metrics（マトリクス/指標）」 -->
<!-- 「どんなデータ（Dimensions（ディメンション））」毎に、「何を（Metrics（マトリクス/指標））」見たいかという形 -->