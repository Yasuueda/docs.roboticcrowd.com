# HumanIntelligence

ロボットが人間からの入力を取得したりします。

## GetHumanInput

### 概要

GetHumanInputは、人が入力した値を取得するアクションです。入力依頼は、assistantパラメーターで設定したメールアドレスに送られます。assistantパラメータには、コラボレーターに設定されているメールアドレスを指定してください。コラボレーター以外のメールアドレスに入力依頼を送信することはできません。  
５分経っても値が入力されない場合、Timeoutエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| text\* | 文字列 | 入力依頼の内容 | 画像の文字を入力してください |
| image | 文字列 | 入力依頼に添付する画像ファイル | +take\_screenshot\_1 |
| assistant\* | 文字列 | メールアドレス\(コラボレーターに設定されているもの\) | john.doe@example.com |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | 入力値 | 123456 |

### 使用例

```yaml
+get_human_input_1:
  action>: GetHumanInput
  text: '下記の画像の文字を入力してください。'
  image: +take_screenshot_1
  assistant: 'john.doe@example.com'
  # => "123456"
```

