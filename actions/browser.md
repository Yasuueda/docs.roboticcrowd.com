---
description: ブラウザアクションの一覧です。
---

# Browser

## OpenBrowser

### 概要

OpenBrowserは、ほぼすべてのワークフローで利用されるアクションです。ブラウザ（Chromium）を起動して、指定されたウェブサイトを開きます。アウトプットは、起動したブラウザのウェブソケットアドレスになります。

OpenBrowserは、指定したURLのDOM要素のレンダリングが開始されるまで待機します（document の load イベント発火まで待機）。30秒経過してもページが開かない場合は、Timeoutエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| url\* | 文字列 | 最初に開くウェブサイトのURL | https://yahoo.co.jp |
| lang | 文字列 | ブラウザの言語設定、ISO 639言語コード。 | en \(default\) |
| timeZone | 文字列 | ブラウザの場所設定、タイムゾーン。 | Etc/GMT \(default\) |
| userAgent | 文字列 | ブラウザのユーザーエージェント設定。 | HeadlessChrome \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

```yaml
+open_browser_1:
  action>: OpenBrowser
  url: 'https://yahoo.co.jp'
  lang: 'ja-JP'
  timeZone: 'Asia/Tokyo'
  userAgent: 'Robotic Crowd Agent'
```

## GoTo

### 概要

GoToは、ブラウザのアドレスバーに直接URLを入力して遷移させます。セッションを保ったままページ遷移させたり、URLを指定することで、サイト内の深い階層まで一気に遷移させるときなどに利用できます。

GoToは、指定したURLのDOM要素のレンダリングが開始されるまで次のアクションに進むのを待機します。30秒経過してもページが開かない場合は、Timeoutエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| url\* | 文字列 | 遷移先URL | [https://yahoo.co.jp](https://yahoo.co.jp) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。実行前待機時間を短くして、実行後待ち時間を2秒に設定したもの。

```yaml
+go_to_1:
  action>: GoTo
  browser: +open_browser_1
  url: 'https://yahoo.co.jp'
  waitBefore: 10
  waitAfter: 2000
```

## CloseBrowser

### 概要

CloseBrowserは、ブラウザを閉じます。ブラウザを閉じてセッションも切っておきたいときに使います。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Boolean | 真理値 | 完了するとtrueとなる（エラーがなければ、常にtrue） | true |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。実行前待機時間を短くして、実行後待ち時間を2秒に設定したもの。

```yaml
+close_browser_1:
  action>: CloseBrowser
  browser: +open_browser_1
  waitBefore: 10
  waitAfter: 2000
```

## Click

### 概要

Clickは、ブラウザの内の指定の要素をクリックします。クリックに付随したダウンロードやダイアログの処理についてもここで設定します。ブラウザの接続先をアウトプットします。

Clickでクリック可能な要素は、表示されているという条件が必要です。Clickは、実際のブラウザの画面上の点をクリックするようになっているので、HTML内に要素があっても見える状態（visible）でないとエラーとなります。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#submitBtn |
| confirm | 真理値 | ダイアログが表示されたらOKをクリックする。 | true \(default\) |
| type\_to\_confirm | 文字列 | confirmがtrueの時、ダイアログに文字を入力してから、OKをクリックする。 | null \(default\) |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitForDownload | 真理値 | このクリックでダウンロードが始まるので、ダウンロードの完了までこのアクション内で待機する。最大3分間待機する。 | false \(default\) |
| highResolution | 真理値 | ウィンドウを1280x720まで拡大してからクリックする。 | false \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。クリックで確認ダイアログが表示され、CSVダウンロードが始まることがわかっているので、そのダウンロードまで待つ。また、セレクタが見つからない場合は、エラーとして途中で終了するようにする。

```yaml
+click_1:
  action>: Click
  browser: +open_browser_1
  selector: 'input#download'
  ingnoreError: false
  waitForDownload: true
  highResolution: true
```

## Hover

### 概要

Hoverは、ブラウザの内の指定の要素にマウスをあわせます。Hoverで表示される要素をクリックしたり、取得したりする際に利用します。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#submitBtn |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| highResolution | 真理値 | ウィンドウを1280x720まで拡大してからクリックする。 | false \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。

```yaml
+hover_1:
  action>: Hover
  browser: +open_browser_1
  selector: 'i#hint'
  ingnoreError: true
  highResolution: true
```

## TypeText

### 概要

TypeTextは、ブラウザの内の指定の要素に文字を入力します。インプットフィールドに値をセットするのではなく、人間が入力するように一文字ずつテキストを入力していく操作となります。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#submitBtn |
| text\* | 文字列 | 入力する文字列 | ミーアキャット |
| clearValue | 真理値 | trueの時、すでに入力されている値を消去します。falseの時、追記します。 | false \(default\)  |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| delay | 整数 | 1文字ずつ入力する際のタイプ遅延（ms）。例えば、'abcd' と入力する際に20セットされていると、a \(20ms\) b \(20ms\) c \(20ms\) d と入力するので、60ms以上時間がかかる。 | 0 \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。検索フィールドにミーアキャットと入力する。事前に入力されている文字があれば消去。タイピングのスピードは、5msとする。

```yaml
+type_text_1:
  action>: TypeText
  browser: +open_browser_1
  selector: 'input#srchtxt'
  text: ミーアキャット
  clearValue: true
  ingnoreError: false
  delay: 5
```



## SelectOption

### 概要

選択肢型のUIを操作して、その値（value）または、表示名（innerText）により選択肢を選択します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#optionSelect |
| value\*\(1\) | 文字列 | 選択する値（value）で選択する | okinawa |
| text\*\(1\) | 文字列 | 選択肢の表示名（innerText）で選択する | 沖縄 |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

\(\*1\) どちらか必須 

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。選択肢で8を選択する。

```yaml
+select_option_1:
  action>: SElectOption
  browser: +open_browser_1
  selector: '#startHour'
  value: 8
  ingnoreError: false
```

## SetFileToUpload

### 概要

SetFileToUploadは、ブラウザの内のフォーム要素にファイルをセットします。ファイルをアップロードする際に利用します。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#submitBtn |
| file\* | 文字列 | fileがあるpathを指定します。指定できるpathは、実行中のロボットの一時フォルダ内に限定されます。アップロードするファイルは、事前にGetFileなどで取得する必要があるので、GetFileアクションのアウトプットを指定することが通常です。 | +get\_file\_1 |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。フォーム内のファイル要素にGetFileで事前に取得してきたファイルをセットする。

```yaml
+set_file_to_upload_1:
  action>: SetFileToUpload
  browser: +open_browser_1
  selector: 'form input[type=file]'
  file: +get_file_1
  ingnoreError: false
```

## TypePassword

### 概要

TypePasswordは、TypeTextと同じ動作をしますが、パスワードがマスクされたり、input\[type=password\] 以外要素には使えないなどのいくつかの制限があります。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ。input\[type=password\]となっている要素のみ設定可能。 | \#password |
| password\* | 文字列 | 入力するパスワード。パスワードは、ワークフロー保存時にマスクされ\*\*\*\*\*という表示になる。 | true \(default\) |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| delay | 整数 | 1文字ずつ入力する際のタイプ遅延（ms）。例えば、'abcd' と入力する際に20セットされていると、a \(20ms\) b \(20ms\) c \(20ms\) d と入力するので、60ms以上時間がかかる。 | 0 \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。パスワードにthisispasswordと入力する。

```yaml
+type_password_1:
  action>: TypePassword
  browser: +open_browser_1
  selector: 'input#password'
  password: thisispassword      # => 保存後は、 '******' となりマスクされます。
  ingnoreError: false
```

## GetText

### 概要

GetTextは、ブラウザの内の指定の要素内の文字をすべて取得します。取得した文字列をアウトプットします。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#submitBtn |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text | 文字列 | 取得した文字列 | "明日の江東区の天気は、晴れです。" |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。

```yaml
+get_text_1:
  action>: GetText
  browser: +open_browser_1
  selector: 'p#detail'
  ingnoreError: false
```

## SendKeys

### 概要

SendKeysは、キーボードを操作する低水準のアクションです。メタキーを含めて送信可能です。ロボットは、LinuxOS上で動作していることを前提にしてください。

表示確認用に、セレクターをセットすることができますが、SendKeys自体は、セレクタの指定は不要です。現在のブラウザの状態のままキーボードを押して離すことをエミュレートします。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| keys | 配列 | キーの名前を要素とした配列を入力します。使えるキーの名前一覧は、[こちら](https://github.com/GoogleChrome/puppeteer/blob/master/lib/USKeyboardLayout.js)を参照してください。 | \["ArrowLeft", "Enter"\] |
| selector | 文字列 | 操作対象のCSSセレクタ。必須ではありません。 | body \(default\) |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。左矢印とエンターキーをほぼ同時に送信する。

```yaml
+send_keys_1:
  action>: SendKeys
  browser: +open_browser_1
  keys: ["ArrowLeft", "Enter"]
```

## SubmitForm

### 概要

SubmitFormは、クリックやキーの送信ではなく、プログラム的にフォームを送信したい場合に利用します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ。 | form\#entry |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。入力フォームをプログラム的に送信する。

```yaml
+submit_form_1`:
  action>: SubmitForm
  browser: +open_browser_1
  selector: 'form#entry'
```

## TakeScreenshot

### 概要

TakeScreenshotは、ブラウザの画面を画像として保存するアクションです。画像ファイルのパスをアウトプットします。

### パラメーター <a id="paramt-9"></a>

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| full\_page | 真理値 | trueの時、スクロール可能な領域を含めて全体をスクリーンショットします。falseのときは、ウィンドウサイズのみ撮影します。 | false \(default\) |
| highResolution | 真理値 | ウィンドウを1280x720まで拡大してからクリックする。 | false \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット <a id="autoputto-9"></a>

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Image | 文字列 | 撮影した画面のpngファイルのパス。 | /tmp/fb4edcb2/screenshots/1.png |

### 使用例 <a id="shi-yong-li-9"></a>

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。高解像度モードで全ページを撮影する。

```yaml
+take_screenshot_1:
  action>: TakeScreenshot
  browser: +open_browser_1
  full_page: true
  hightResolution: true
```

## TakeElementShot

### 概要

TakeElementShotは、ブラウザに表示されている一部の要素のみ撮影します。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、エラーとなります。

### パラメーター <a id="paramt-9"></a>

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 撮影する要素のCSSセレクター | p &gt; img |
| highResolution | 真理値 | ウィンドウを1280x720まで拡大してからクリックする。 | false \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット <a id="autoputto-9"></a>

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Image | 文字列 | 撮影した画面のpngファイルのパス。 | /tmp/fb4edcb2/screenshots/1.png |

### 使用例 <a id="shi-yong-li-9"></a>

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。高解像度モードで画像要素のみ撮影する。

```yaml
+take_element_shot_1:
  action>: TakeElementShot
  browser: +open_browser_1
  selector: 'p > img'
  hightResolution: true
```

## WaitForDownload

### 概要

WaitForDownloadは、ダウンロード中のファイルのダウンロードが完了するのをまちます。このアクションが呼び出されると、ダウンロードファイルが以前のアクションの状態よりも、一つ増えるまでまちます、ダウンロード中のファイル（.crdownloadで終わるファイル）があれば完了するまでまちます。最大で3分まちます。

### パラメーター <a id="paramt-9"></a>

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| timeout | 整数 | 最大の待ち時間（ms）。 | 180000 \(default\) |

### アウトプット <a id="autoputto-9"></a>

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Boolean | 真理値 | タイムアウトせずに完了するとtrue、タイムアウトで完了した場合は、falseになります。 | true |

### 使用例 <a id="shi-yong-li-9"></a>

ブラウザの接続先は、OpenBrowserアクションのアウトプットを再利用する。

```yaml
+wait_for_download_1:
  action>: WaitForDownload
```

## GetDownloadFiles

### 概要

GetDownloadFilesは、ダウンロードフォルダ内のファイル一覧を取得します。ファイル名、または、ファイルの最終修正時刻で並び替えができます。

### パラメーター <a id="paramt-9"></a>

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| order | セレクト | 並び替えの順序。ASCだと、若い値が先にきます。DESCだと、その逆に並びます。 | ASC |
| sort_by | セレクト | 並び替えのキー。FILENAMEだと、ファイル名の辞書順、CREATEDだと、ファイルの修正時刻順になります。順序をDESC、キーをCREATEDにすることで、一番初めの値が、最新のダウンロードファイルになります。 | FILENAME |

### アウトプット <a id="autoputto-9"></a>

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | ファイルの一覧を返します。 | \["/path/to/downloads/1.png", "/path/to/downloads/2.png"\] |

### 使用例 <a id="shi-yong-li-9"></a>

ダウンロードフォルダのファイル一覧を取得します。

```yaml
+get_download_files_1:
  action>: GetDownloadFiles
  order: ASC
  sort_by: FILENAME
```

## ScrapePage

### 概要

ScrapePageは、ウェブサイトから複数の情報を取得してきます。CSSセレクタにマッチするすべての要素の文字列 （innerText）、HTML \(innerHTML\)、リンク、ボタン、画像を取得します。これらをオブジェクトにした配列を出力します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | スクレイピングする要素のCSSセレクタ。複数にマッチすることを前提としている。 | div\#title |
| text\_only | 真理値 | true のとき、要素内部のテキスト情報のみを取得し、配列として出力する。子要素のテキストもまとめて取得する。 | false\(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 30 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 30 \(default\) |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | 取得した情報の一覧 | ※アウトプット例を参考 |

### 使用例

```yaml
+scrape_page_1:
  action>: ScrapePage
  browser: +open_browser_1
  selector: 'div#title'
  text_only: true
  ignoreError: false
```

#### アウトプット例

本のタイトル一覧を取得した場合の例。

```text
[
  "決定版猫と一緒に生き残る防災BOOK",
  "牝の猫と女のネコ",
  "通い猫アルフィーの奇跡",
  "猫をよろこばせる本",
  "猫の困った行動解決ハンドブック"
]
```

## ExtractDataFromTable

### 概要

ExtractDataFromTableは、ウェブサイトにあるテーブル（表）からデータを取得します。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | table |
| waitBefore | 整数 | 実行前待機時間（ms） | 30 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 30 \(default\) |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
|  Array | 配列 | 取得したテーブルデータ | ※アウトプット例を参照 |

### 使用例

```yaml
+extract_data_from_table_1:
  action>: ExtractDataFromTable
  browser: +open_browser_1
  selector: ' table '
  ignoreError: false
```

#### アウトプット例

賃貸情報を取得した場合の例。

```text
[
  [
    "階",
    "賃料/管理費",
    "敷金/礼金",
    "間取り/専有面積",
    "お気に入り",
    " "
  ],
  [
    "4階",
    "44.5万円\n-\n",
    "89万円\n44.5万円\n",
    "2LDK\n75.67m2\n",
    "追加",
    "詳細を見る"
  ]
]
```

## InjectScript

### 概要

InjectScriptは、ページ内でJavaScriptを実行します。実行は、30秒以内にタイムアウトします。JavaScript内で計算した結果をロボットに直接渡すことはできません。ご注意ください。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +click\_1 |
| code\* | 文字列 | Javascriptのコード | ※使用例のcodeを参照 |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Browser | 文字列 | 起動したブラウザのWebSocketアドレス | ws://127.0.0.1:52582/devtools/browser/be5e7b6e-ce64-4040-a7af-15ecc7b125f0 |

### 使用例

```yaml
+inject_script_1:
  action>: InjectScript
  browser: +open_browser_1
  code: 'document.getElementById("srchbtn").value  = "開始";'
  waitBefore: 10
  waitAfter: 2000
```

## ExtractData

### 概要

ExtractDataは、ウェブサイトから複数の情報まとめて取得してきます。

マルチプルモードでは、同じページ無いの繰り返しデータを整形して取得します。マルチプルモードの場合は、二つ以上のセレクターが必要になります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| extractor\* | 文字列 | オブジェクト形式の抽出対象 | ※使用例のextractor参照 |
| format | 文字列 | json または csv を選択できます | csv |
| multiple | 真偽値 | 二つ以上のセレクタを指定する | false\(default\) |

#### 補足: extractor

取得する情報の種類と、セレクターをオブジェクト形式で設定します。マルチプルモードの場合は、二つ以上のセレクターが必要になります。

extractorは、取得するデータの名前である name キーと、そのデータの場所を指定する selectors キーを持つオブジェクトの配列です。

multiple: true のときは、selectorsに指定されたデータの場所を元に繰り返しを検出します。

multiple: false のときは、selectorsに指定されたデータの場所を順番に取得していき、最初に取得が成功したデータを取得します。別の言い方をすると、取得に失敗した時（場所が見つからなかった時）は、次の selector を使ってデータの取得を試みます。この仕組みにより、異なるフォーマットのページで同じextractorを使用できます。

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
|  Anything | 配列 | 取得した情報の一覧 | ※使用例の各アウトプット参照 |

### 使用例

#### multiple: trueの場合

```yaml
+extract_data_1:
  action>: ExtractData
  browser: +open_browser_1
  extractor:
    - {"name":"店名", "selectors":["div:nth-child(2) > .title", "div:nth-child(3) > .title"]}
    - {"name":"電話番号", "selectors":["div:nth-child(2) > .tel", "div:nth-child(3) > .tel"]}
  format: csv
  multiple: true
```

#### アウトプット \(CSV\)

```text
[
  [
    "店名", "電話番号"
  ],
  [
    "夢谷ばー 渋谷本店", "03-xxxx-xxxx"
  ],
  [
    "イタリアンバル 丸の内店", "03-xxxx-xxxx"
  ],
  [
    "Cafe Bar Ocean", "03-xxxx-xxxx"
  ],
  [
    "ポートポート赤坂見附店", "03-xxxx-xxxx"
  ]
]
```

#### multiple: falseの場合

```yaml
+extract_data_1:
  action>: ExtractData
  browser: +open_browser_1
  extractor: [{"name":"店名","selectors":["div#title"]},{"name":"エリア","selectors":["div#sub_title"]}]
  format: csv
  multiple: false
```

#### アウトプット \(CSV\)

```text
[
  [
    "店名",
    "エリア"
  ],
  [
    "日比谷Bar 渋谷本店",
    " 渋谷駅 228m / バル・バール、イタリアン、ダイニングバー"
  ]
]
```

## GetURL

### 概要

GetURLは、現在表示しているウェブサイトのURLを取得します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text  | 文字列 | 取得したURL | "https://roboticcrowd.com/" |

### 使用例

```yaml
+get_u_r_l_1:
  action>: GetURL
  browser: +open_browser_1
```

## GetAttribute

### 概要

GetAttributeは、セレクタで指定した要素の属性値を取得します。

このアクションは、30秒間要素の出現をまちます。30秒たっても要素が出現しない場合、デフォルトでは、そのまま次のアクションに進みます。ただし、ignoreErrorにfalseがセットされている場合は、要素が出現しない場合にエラーとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | body &gt; div &gt; img |
| attribute\* | 文字列 | 取得する属性（id, src, href, altなど） | src |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |

#### 補足: attribute

代表的な属性として以下のものがあります。

| 属性 | 説明 |
| :--- | :--- |
| src | 画像のURL（パス） |
| href | リンク先のURL（パス） |
| alt | 画像などの説明文 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Text  | 文字列 | 取得した属性値 | "/images/logo.svg" |

### 使用例

```yaml
+get_attribute_1:
  action>: GetAttribute
  browser: +open_browser_1
  selector: 'body > div > img'
  attribute: src
```

