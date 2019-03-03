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

選択肢型のUIを操作して、その値（value）により選択肢を選択します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| browser\* | 文字列 | ブラウザの接続先 | +open\_browser\_1 |
| selector\* | 文字列 | 操作対象のCSSセレクタ | \#optionSelect |
| value\* | 文字列 | 選択する値 | okinawa |
| ignoreError | 真理値 | CSSセレクタが見つからないなどのエラーが発生しても次のタスクへ進む。 | true \(default\) |
| waitBefore | 整数 | 実行前待機時間（ms） | 100 \(default\) |
| waitAfter | 整数 | 実行後待機時間（ms） | 100 \(default\) |

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

GetDownloadFilesは、ダウンロードフォルダ内のファイル一覧を取得します。

### パラメーター <a id="paramt-9"></a>

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| - | - | - | - |

### アウトプット <a id="autoputto-9"></a>

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | ファイルの一覧を返します。 | \["/path/to/downloads/1.png", "/path/to/downloads2.png"\] |

### 使用例 <a id="shi-yong-li-9"></a>

ダウンロードフォルダのファイル一覧を取得します。

```yaml
+get_download_files_1:
  action>: GetDownloadFiles
```

## ScrapePage

TODO

## ExtractDataFromTable

TODO

## InjectScript

TODO

## ExtractData

TODO

## GetURL

TODO

## GetAttribute

TODO

