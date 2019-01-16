# Text

文字列を操作するアクションの一覧です。

## Text

TODO

## SplitText

## ReplaceText

## MatchText

## EscapeRegex

## ReadText

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

