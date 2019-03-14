# Google Spreadsheet

Google Spreadsheetを操作するアクション一覧です。

## CreateSpreadsheet

### 概要

CreateSpreadsheetは、スプレッドシートを新たに作成するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| title\* | 文字列 | スプレッドシートのタイトル | test |
| provider\* | 文字列 | コネクションより取得したGoogleSpreadsheetのプロバイダーID | gsheet_1234abcd |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Spreadsheet | スプレッドシート | 作成したスプレッドシートオブジェクト | ※使用例のアウトプット参照 |

### 使用例

```yaml
+create_spreadsheet_1:
  action>: CreateSpreadsheet
  title: test
  provider: gsheet_8e2eb635cb50f9f86eb7
# => {
#   "spreadsheetId": "1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro",
#   "properties": {
#     "title": "test",
#     "locale": "ja_JP",
#     "autoRecalc": "ON_CHANGE",
#     "timeZone": "Etc/GMT",
#     "defaultFormat": {
#       "backgroundColor": {
#         "red": 1,
#         "green": 1,
#         "blue": 1
#       },
#       "padding": {
#         "top": 2,
#         "right": 3,
#         "bottom": 2,
#         "left": 3
#       },
#       "verticalAlignment": "BOTTOM",
#       "wrapStrategy": "OVERFLOW_CELL",
#       "textFormat": {
#         "foregroundColor": {},
#         "fontFamily": "arial,sans,sans-serif",
#         "fontSize": 10,
#         "bold": false,
#         "italic": false,
#         "strikethrough": false,
#         "underline": false
#       }
#     }
#   },
#   "sheets": [
#     {
#       "properties": {
#         "sheetId": 0,
#         "title": "シート1",
#         "index": 0,
#         "sheetType": "GRID",
#         "gridProperties": {
#           "rowCount": 1000,
#           "columnCount": 26
#         }
#       }
#     }
#   ],
#   "spreadsheetUrl": "https://docs.google.com/a/tutorial.co.jp/spreadsheets/d/1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro/edit",
#   "provider": "gsheet_8e2eb635cb50f9f86eb7"
# }
```

## GetSpreadsheet

### 概要

GetSpreadsheetは、GoogleSpreadsheetオブジェクトを取得するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| provider\* | 文字列 | コネクションより取得したGoogleSpreadsheetのプロバイダーID | gsheet_1234abcd |
| spreadsheet_id\* | 文字列 | 使用するスプレッドシートID | 1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Spreadsheet | スプレッドシート | 取得したスプレッドシートオブジェクト | ※使用例のアウトプット参照 |

### 使用例

```yaml
+get_spreadsheet_1:
  action>: GetSpreadsheet
  provider: gsheet_8e2eb635cb50f9f86eb7
  spreadsheet_id: 1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro
# => {
#   "spreadsheetId": "1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro",
#   "properties": {
#     "title": "test",
#     "locale": "ja_JP",
#     "autoRecalc": "ON_CHANGE",
#     "timeZone": "Etc/GMT",
#     "defaultFormat": {
#       "backgroundColor": {
#         "red": 1,
#         "green": 1,
#         "blue": 1
#       },
#       "padding": {
#         "top": 2,
#         "right": 3,
#         "bottom": 2,
#         "left": 3
#       },
#       "verticalAlignment": "BOTTOM",
#       "wrapStrategy": "OVERFLOW_CELL",
#       "textFormat": {
#         "foregroundColor": {},
#         "fontFamily": "arial,sans,sans-serif",
#         "fontSize": 10,
#         "bold": false,
#         "italic": false,
#         "strikethrough": false,
#         "underline": false
#       }
#     }
#   },
#   "sheets": [
#     {
#       "properties": {
#         "sheetId": 0,
#         "title": "シート1",
#         "index": 0,
#         "sheetType": "GRID",
#         "gridProperties": {
#           "rowCount": 1000,
#           "columnCount": 26
#         }
#       }
#     }
#   ],
#   "spreadsheetUrl": "https://docs.google.com/a/tutorial.co.jp/spreadsheets/d/1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro/edit",
#   "provider": "gsheet_8e2eb635cb50f9f86eb7"
# }
```

## GetCells

### 概要

GetCellsは、セルの値を取得するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| spreadsheet\* | スプレッドシート、文字列、オブジェクト | 対象のスプレッドシート | +get_spreadsheet_1 |
| range\* | 文字列 | 取得する値のセルの範囲(A1記法) | !A1:D4 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Array | 配列 | 取得したセルの値を[行][列]の二次元配列で返します。 | [['A1','B1'],['A2', 'B2']] |

### 使用例

```yaml
+get_cells_1:
  action>: GetCells
  spreadsheet: +get_spreadsheet_1
  range: '!A1:D4'
# => [
#   [
#     "",
#     "国語",
#     "数学",
#     "英語"
#   ],
#   [
#     "A杉",
#     "90",
#     "43",
#     "87"
#   ],
#   [
#     "B山",
#     "82",
#     "95",
#     "43"
#   ],
#   [
#     "C田",
#     "100",
#     "100",
#     "100"
#   ]
# ]
```

## UpdateCells

### 概要

UpdateCellsは、セルの値を更新するアクションです。セルの値はすぐに更新されます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| spreadsheet\* | スプレッドシート、文字列、オブジェクト | 対象のスプレッドシート | +get_spreadsheet_1 |
| range\* | 文字列 | 更新するセルの範囲(A1記法) | !A1:D4 |
| values\* | 配列 |  書き込む値　| [['A1','B1'],['A2', 'B2']]

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Spreadsheet | スプレッドシート | 更新されたスプレッドシートオブジェクト | ※使用例のアウトプット参照 |

### 使用例

```yaml
+update_cells_1:
  action>: UpdateCells
  spreadsheet: +get_spreadsheet_1
  range: 'シート1!A6:D6'
  values: [["平均","=SUM(B2:B5)","=SUM(C2:C5)","=SUM(D2:D5)"]]
# => {
#   "spreadsheetId": "1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro",
#   "properties": {
#     "title": "test",
#     "locale": "ja_JP",
#     "autoRecalc": "ON_CHANGE",
#     "timeZone": "Etc/GMT",
#     "defaultFormat": {
#       "backgroundColor": {
#         "red": 1,
#         "green": 1,
#         "blue": 1
#       },
#       "padding": {
#         "top": 2,
#         "right": 3,
#         "bottom": 2,
#         "left": 3
#       },
#       "verticalAlignment": "BOTTOM",
#       "wrapStrategy": "OVERFLOW_CELL",
#       "textFormat": {
#         "foregroundColor": {},
#         "fontFamily": "arial,sans,sans-serif",
#         "fontSize": 10,
#         "bold": false,
#         "italic": false,
#         "strikethrough": false,
#         "underline": false
#       }
#     }
#   },
#   "sheets": [
#     {
#       "properties": {
#         "sheetId": 0,
#         "title": "シート1",
#         "index": 0,
#         "sheetType": "GRID",
#         "gridProperties": {
#           "rowCount": 1000,
#           "columnCount": 26
#         }
#       }
#     }
#   ],
#   "spreadsheetUrl": "https://docs.google.com/a/tutorial.co.jp/spreadsheets/d/1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro/edit",
#   "provider": "gsheet_8e2eb635cb50f9f86eb7"
# }
```

## AppendValues

### 概要

AppendValuesは、指定した範囲の最後の行に値を追加するアクションです。シート名を指定した場合、シートの最後の空行に値を追加します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| spreadsheet\* | スプレッドシート、文字列、オブジェクト | 対象のスプレッドシート | +get_spreadsheet_1 |
| range\* | 文字列 | 指定するセルの範囲(A1記法)。指定した範囲の最後の行に値が追加されます。  | シート1 |
| values\* | 配列 |  追加する値　| [['A1','B1'],['A2', 'B2']]

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Spreadsheet | スプレッドシート | 更新されたスプレッドシートオブジェクト | ※使用例のアウトプット参照 |

### 使用例

```yaml
+append_values_1:
  action>: AppendValues
  spreadsheet: +get_spreadsheet_1
  range: 'シート1'
  values: [["E森","23","34","45"]]
# => {
#   "spreadsheetId": "1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro",
#   "properties": {
#     "title": "test",
#     "locale": "ja_JP",
#     "autoRecalc": "ON_CHANGE",
#     "timeZone": "Etc/GMT",
#     "defaultFormat": {
#       "backgroundColor": {
#         "red": 1,
#         "green": 1,
#         "blue": 1
#       },
#       "padding": {
#         "top": 2,
#         "right": 3,
#         "bottom": 2,
#         "left": 3
#       },
#       "verticalAlignment": "BOTTOM",
#       "wrapStrategy": "OVERFLOW_CELL",
#       "textFormat": {
#         "foregroundColor": {},
#         "fontFamily": "arial,sans,sans-serif",
#         "fontSize": 10,
#         "bold": false,
#         "italic": false,
#         "strikethrough": false,
#         "underline": false
#       }
#     }
#   },
#   "sheets": [
#     {
#       "properties": {
#         "sheetId": 0,
#         "title": "シート1",
#         "index": 0,
#         "sheetType": "GRID",
#         "gridProperties": {
#           "rowCount": 1000,
#           "columnCount": 26
#         }
#       }
#     }
#   ],
#   "spreadsheetUrl": "https://docs.google.com/a/tutorial.co.jp/spreadsheets/d/1zTG_XHbCnC5a5BD5k5WWxdbcYpnEDv4_FfdAPaE33ro/edit",
#   "provider": "gsheet_8e2eb635cb50f9f86eb7"
# }
```

