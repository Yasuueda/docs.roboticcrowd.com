# Text

文字列を操作するアクションの一覧です。

## Text

### 概要

Textは、テキストを作成するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| text\* | 文字列 | 作成したいテキスト | こんにちは |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | 作成されたテキスト | "こんにちは" |

### 使用例

```yaml
+text_1:
  action>: Text
  text: 'こんにちは'
```

## SplitText

### 概要

SpletTextは、テキストを区切り文字で分割して配列にするアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| text\* | 文字列 | 対象のテキスト | 我輩は,猫,である |
| split\_with | 文字列 | 区切り文字 | , |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | 分割した文字列のリスト | \["我輩は","猫","である"\] |

### 使用例

```yaml
+split_text_1:
  action>: SplitText
  text: '我輩は,猫,である'
  split_with: ','
```

## ReplaceText

### 概要

ReplaceTextは、テキスト内の文字列を別の文字列で置き換えるアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| text\* | 文字列 | 対象のテキスト | 我輩は猫である |
| find\* | 文字列 | 検索文字列 | 猫 |
| use\_regex\* | 真理値 | 正規表現を使用するかどうか | true\(default\) |
| replace\_with\* | 文字列 | 新しい文字列 | 犬 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | 新しいテキスト | "我輩は犬である" |

### 使用例

```yaml
+replace_text_1:
  action>: ReplaceText
  text: '我輩は猫である'
  find: '猫'
  use_regex: false
  replace_with: '犬'
```

## MatchText

### 概要

テキストから正規表現で検索し、マッチした文字列を配列で返却します。'090-1234-1234'は、\d{3}-\d{4}-\d{4}にマッチします。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text\* | 文字列 | テキスト | 090-1234-1234 |
| Regrex\* | 正規表現 | リテラル表現（スラッシュ / で囲う）で入力してください。 | /d{3}-d{4}-d{4}/ |
|  | 真理値 | マッチした文字列全件を取得するかどうか。初期値は、trueです。 | true \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 配列 | 文字列のリスト（グループされます） | \["090-1234-1234"\] |

## EscapeRegex

### 概要

EscapeRegexは、正規表現をエスケープするアクションです。動的に正規表現を生成したい場合に使用します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| text\* | 文字列 | 対象のテキスト | この商品は"1500円"です |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | エスケープされたテキスト | "この商品は\"1500円\"です" |

### 使用例

```text
"この商品は\"1500円\"です"
```

```yaml
+escape_regex_1:
  action>: EscapeRegex
  text: 'この商品は"1500円"です'
```

## ReadText

### 概要

ReadTextは、ファイルから文字列を読み込むアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列 | 読み込むファイルのファイルパス | +get\_download\_files\_1 |
| encoding | 文字列 | 読み込むファイルの文字エンコーディング | utf-8\(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | 読み込んだテキスト | ※アウトプット例を参照 |

#### アウトプット例

```text
"\"名前\",\"性別\",\"年齢\",\"住所\"\n\"Roland Witting\",\"Male\",\"31\",\"Suite 662 23443 Horace Port, East Gaston, HI 93524\"\n\"Junita Welch\",\"Male\",\"15\",\"55451 Sunshine Causeway, Roseannabury, KS 38599\"\n\"Barry Terry\",\"Male\",\"7\",\"Suite 324 154 Abshire Center, Trantowtown, MN 79628-5905\"\n\"Kristle Purdy\",\"Male\",\"87\",\"Apt. 869 224 Kourtney Ramp, Lakeshafurt, SD 93802\"\n\"Brittanie Schmeler\",\"Male\",\"36\",\"Apt. 254 98730 Antonio Neck, Rogahnton, NV 96771\"\n"
```

### 使用例

```yaml
+read_text_1:
  action>: ReadText
  filename: +get_download_files_1
  encoding: 'utf-8'
```

## ConvertPDFToText

### 概要

ConvertPDFToTextアクションは、PDFファイルの文字情報のみを抽出して文字列として扱えるようにするアクションです。いわゆる画像から文字を認識するOCRの機能はサポートされていないため、OCRを利用する際は、TextDetectionアクションを利用することを検討してください。文字列に変換されたPDFでは、改行は残っており、枠線などがあれば、記号として残るようになっています。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| pdf\* | 文字列 | PDFファイルのファイルパスを入力します。PDFファイルはロボット側にダウンロードしておく必要があるので、ダウンロードしたファイルを利用することを想定しています。 | +get\_file\_1 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | PDFから抽出したテキスト | "吾輩は猫である。名前は、・・・" |

### 使用例

```yaml
+convert_pdf_to_text_1:
  action>: ConvertPDFToText
  pdf: '+get_file_1'
```

## GetTime

### 概要

GetTimeアクションは、指定したフォーマットとタイムゾーンから現在時刻を出力するアクションです。フォーマット及びタイムゾーンは,テキストで入力します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| format | 文字列 | 日付フォーマット | YYYY-MM-DD |
| timezone | 文字列 | タイムゾーン | Asia/Tokyo |

#### 補足: 入力フォーマット

フォーマットとタイムゾーンをテキストで入力する際の入力例。

```text
フォーマット(format)
*アクション実行が2019年4月1日の場合。

- YYYY-MM-DD(2019-04-01)
- YYYY-MM-DD HH:mm(2019-04-01 09:00)*午前9時の場合。
- YYYY/MM/DD(2019/04/01)
- MMMM Do YYYY(April 1st 2019)

タイムゾーン(timezone)
*任意のタイムゾーンを地域/都市の形式で入力。

- Asia/Tokyo
- Europe/London
- America/New_York
```

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | 指定したタイムゾーンにおける日付と現在時刻 | ※アウトプット例を参照 |

#### アウトプット例

アクション実行日時が2019年4月1日の場合。

```text
　"2019-04-01"
```

### 使用例

```yaml
+get_time_1:
  action>: GetTime
  format: 'YYYY-MM-DD'
  timezone: 'Asia/Tokyo'
```

