# Excel

Excelファイルの操作を行うアクション一覧です。

## SelectSheet

### 概要

SelectSheetは、ワークシートを選択するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列 | 使用するExcelのファイル名 | +get\_file\_1 |
| sheetname\* | 文字列 | 使用するExcelのシート名 | Sheet1 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Worksheet | ワークシート | 選択したワークシート | ※使用例のアウトプット参照 |

### 使用例

```yaml
+select_sheet_1:
  action>: SelectSheet
  filename: +get_file_1
  sheetname: 'データ'
# => {
#  "filename": "/tmp/1decfdb0-7795-4b7c-a851-668c2b81a067/local/詳細データ集計.xlsx",
#  "sheetname": "データ",
#  "rows": 195
#}
```

## ReadCell

### 概要

ReadCelltは、セルの値を読み込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| worksheet\* | ワークシート | 対象のワークシート | +select\_sheet\_1 |
| celllabel\* | 文字列 | 読み込むセルラベル | A2 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Anything | 返却された値による | 取得したセルの値 | ※使用例のアウトプット参照 |

### 使用例

```yaml
+read_cell_1:
  action>: ReadCell
  worksheet: +select_sheet_1
  celllabel: G2
# => 157
```

## WriteCell

### 概要

WriteCellは、セルに値を書き込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| worksheet\* | ワークシート | 対象のワークシート | +select\_sheet\_1 |
| celllabel\* | 文字列 | 読み込むセルラベル | A2 |
| value\* | 文字列 | 書き込む値 | 123 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Worksheet | ワークシート | 新しいワークシート | ※使用例のアウトプット参照 |

### 使用例

```yaml
+write_cell_1:
  action>: WriteCell
  worksheet: +select_sheet_1
  celllabel: A12
  value: 'まとめ'
# => {
#  "filename": "/tmp/0495be82-5eb2-4981-b251-6c39c603a31d/local/集計表.xlsx",
#  "sheetname": "1月",
#  "rows": 12
# }
```

## ReadRange

### 概要

ReadRangeは、シートの指定した範囲の値を２次元配列に読み込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| worksheet\* | ワークシート | 対象のワークシート | +select\_sheet\_1 |
| range\* | 文字列 | 読み込むセルラベル | A1:B10 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Array | 配列 | 取得した範囲の値を\[行\]\[列\]の2次元配列として返却します。 | ※使用例のアウトプット参照 |

### 使用例

```yaml
+read_range_1:
  action>: ReadRange
  worksheet: +select_sheet_1
  range: 'A1:B10'
# => [
#  [
#    null,
#    "第１週"
#  ],
#  [
#    "林檎",
#    15
#  ],
#  [
#    "みかん",
#    54
#  ],
#  [
#    "キウイ",
#    34
#  ],
#  [
#    "桃",
#    77
#  ],
#  [
#    "八朔",
#    54
#  ],
#  [
#    "オレンジ",
#    98
#  ],
#  [
#    "グレープフルーツ",
#    53
#  ],
#  [
#    "レモン",
#    34
#  ],
#  [
#    "バナナ",
#    65
#  ]
#]
```

## WriteRange

### 概要

WriteRangeは、シートに配列を書き込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| worksheet\* | ワークシート | 対象のワークシート | +select\_sheet\_1 |
| table\* | 配列 | 書き込む値の配列 | \[\["id","name","age"\],\["1","taro","23"\]\] |
| celllabel\* | 文字列 | 書き込む位置のセルラベル | A2 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Worksheet | ワークシート | 新しいワークシート | ※使用例のアウトプット参照 |

### 使用例

```yaml
+write_range_1:
  action>: WriteRange
  worksheet: +select_sheet_1
  table: +create_list_1
  celllabel: A11
# => {
#  "filename": "/tmp/a2f288c8-aec6-4bcc-b4f9-d9858846c928/local/集計表.xlsx",
#  "sheetname": "1月",
#  "rows": 11
# }
```

## WriteCSV

### 概要

WriteCSVは、CSVファイルに値を書き込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列 | 使用するCSVファイル名 | test |
| table\* | 配列 | 書き込む値を配列で指定 | \[\["Name","Female","Age","Address"\],\["Taro Okamoto","man","67","Osaka"\],\["Jiro Okamoto","man","64","Tokyo"\]\] |
| bom | 真理値 | BOMの有り無し | true（default） |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | 作成したCSVファイル | /tmp/05dc2b55-526c-404c-998a-fcce0905f377/csv/test.csv |

### 使用例

```yaml
+write_c_s_v_1:
  action>: WriteCSV
  filename: test
  table: +create_list_1
  bom: true
# => "/tmp/05dc2b55-526c-404c-998a-fcce0905f377/csv/test.csv"
```

## ReadCSV

### 概要

ReadCSVは、セルに値を書き込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列 | 使用するCSVファイル名 | +get\_file\_1 |
| headers | 真理値 | ヘッダー行が付いているかいないかを指定します。 | true\(default\) |
| encoding | 文字列 | CSVファイルの文字コードを指定します。デフォルトでは、SHIFT\_JISとして読み込みます。サポートされているエンコーディングは表外に記載しました。 | shift\_jis\(default\) |
| delimiter | 文字列 | デリミタの種類を指定します。 デフォルトでは、commaが指定されています。 | comma\(default\), tab, semicolon |

#### サポートされているエンコーディング一覧

utf8, ucs2 / utf16-le, ascii, binary, base64, hex, utf16, utf16-be, utf-7, utf-7-imap, CP932, CP936, CP949, CP950, GB2312, GBK, GB18030, Big5, Shift\_JIS, EUC-JP

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Array | 配列 | 取得した値を二次元配列として返却します。 | ※使用例のアウトプット参照 |

### 使用例

```yaml
+read_c_s_v_1:
  action>: ReadCSV
  filename: +get_file_1
  headers: true
  encoding: utf8
  delimiter: comma
# => [
#  [
#    "名前",
#    "性別",
#    "年齢",
#    "住所"
#  ],
#  [
#    "Shane Tremblay",
#    "Male",
#    86,
#    "963 Gerlach Wall, Jeffreyborough, ND 19461"
#  ],
#  [
#    "Renato Schroeder",
#    "Female",
#    28,
#    "796 Pfeffer Points, Mariannamouth, WI 59528"
#  ]
# ]
```

## DeleteRange

### 概要

DeleteRangeは、指定範囲の値を削除するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| worksheet\* | ワークシート | 対象のワークシート | +select\_sheet\_1 |
| label\* | 文字列 | 範囲\(セルラベル\) | A2:A10 |
| recalculate | 真理値 | 再計算を実行します。範囲が大きい場合、パフォーマンスに大きく影響します。 | false\(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Worksheet | ワークシート | 新しいワークシート | ※使用例のアウトプット参照 |

### 使用例

```yaml
+delete_range_1:
  action>: DeleteRange
  worksheet: +select_sheet_1
  label: 'B10:F10'
# => {
#  "filename": "/tmp/3f7e970d-60a6-4353-8ccf-c4c255986a80/local/集計表.xlsx",
#  "sheetname": "1月",
#  "rows": 10
# }
```

