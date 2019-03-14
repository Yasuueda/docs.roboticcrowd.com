# Data

配列・変数などのデータを取り扱うアクション一覧です。

## CreateList

### 概要

CreateListは、リストを作成するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| items\* | 配列 | 作成するリスト | \["夏目漱石","太宰治","三島由紀夫","川端康成"\] |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | 作成したリスト | \["夏目漱石","太宰治","三島由紀夫","川端康成"\] |

### 使用例

```yaml
+create_list_1:
  action>: CreateList
  items: ["夏目漱石","太宰治","三島由紀夫","川端康成"]
# => ["夏目漱石","太宰治","三島由紀夫","川端康成"]
```

## CreateObject

### 概要

CreateObjectは、オブジェクトを作成するアクションです。keysパラメータを設定すると、各キーの型を指定することができます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| object\* | オブジェクト | 作成するオブジェクト | { id: 123, name: 'taro', mail: 'taro@co.jp' } |
| keys | 配列 | 各キーの型を指定する場合は、配列で記載 | \[\["id","integer"\],\["name","string"\]\] |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | JSON形式 | 作成したオブジェクト | { id: 123, name: 'taro', mail: 'taro@co.jp' } |

### 使用例

```yaml
+create_object_1:
  action>: CreateObject
  object:
    id: 123
    name: taro
    mail: 'taro@co.jp'
  keys: [["id","integer"],["name","string"]]
# => {
#  "id": 123,
#  "name": "taro",
#  "mail": "taro@co.jp"
#}
```

## GetItemFromList

### 概要

GetItemFromListは、リストから要素の場所を指定して値を取得するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| list\* | 配列 | 対象のリスト | \["夏目漱石","太宰治","三島由紀夫","川端康成"\] |
| index\* | 数値 | 取り出したい要素のインデックス（0から始まる） | 1 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Anything | 返却された値による | 取り出した要素 | "太宰治" |

### 使用例

```yaml
+get_item_from_list_1:
  action>: GetItemFromList
  list: ["夏目漱石","太宰治","三島由紀夫","川端康成"]
  index: 1
# => "太宰治"
```

## GetValueWithKey

### 概要

GetValueWithKeyは、オブジェクトからキーを指定して値を取得するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| object\* | 配列 | 対象のオブジェクト | {"author":"夏目漱石","title":"我輩は猫である"} |
| key\* | 文字列 | キー | author |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Anything | 返却された値による | キーの値 | "夏目漱石" |

### 使用例

```yaml
+get_value_with_key_1:
  action>: GetValueWithKey
  object:
    author: '夏目漱石'
    title: '我輩は猫である'
  key: author
# => "夏目漱石"
```

## SearchItemFromList

### 概要

SearchItemFromListは、リスト内を文字列で検索するアクションです。この検索にはワイルドカードが利用できます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| list\* | 配列 | 対象のリスト | \["夏目漱石","太宰治","三島由紀夫","川端康成"\] |
| query\* | 文字列 | 検索クエリ | 太宰\* |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| List | 配列 | 検索にマッチしたもののリスト | \["太宰治"\] |

### 使用例

```yaml
+search_item_from_list_1:
  action>: SearchItemFromList
  list: ["夏目漱石","太宰治","三島由紀夫","川端康成"]
  query: '太宰*'
# => ["太宰治"]
```

## StoreValue

### 概要

StoreValueは、変数に値を保存するアクションです。変数は、 ${...} により呼び出しが可能になります。また、同じ変数名に値を保存することで変数の値を更新することができます。nullの値が定義された場合、空の文字列として登録されます。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| key\* | 文字列 | 変数名 | time |
| value | 格納する値による | 保存する値 | ${moment\(\).zone\("Asia/Tokyo"\).format\("YYYY年MM月DD日"\)} |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Anything | 返却された値による | keyとvalueがオブジェクト型で返却される | {"time":"2019年3月12日"} |

### 使用例

ScrapePageアクションで取得した情報をStoreValueアクションで変数に保存する。

```yaml
+store_value_1:
  action>: StoreValue
  key: titles
  value: +scrape_page_1
# => {
#  "titles": [
#    "決定版猫と一緒に生き残る防災BOOK",
#    "牝の猫と女のネコ",
#    "通い猫アルフィーの奇跡",
#    "猫をよろこばせる本",
#    "猫の困った行動解決ハンドブック"
#  ]
#}
```

#### StoreValueアクションで保存した変数titlesを他アクションで呼び出す

```yaml
+text_1:
  action>: Text
  text: ${titles[0]} # 変数を呼び出す際は、${変数名}の形式で記載
# => "決定版猫と一緒に生き残る防災BOOK"
```

## RunScript

### 概要

アクション内で、JavaScript実行することができます。StoreValueで保存された変数は、同名の変数名でコード内で使用できます。コードはSandbox環境で実行され、利用できるコードは、JavaScriptのにBuilt-inされたオブジェクトのみが利用できます。30秒後にTimeoutします。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| code\* | 文字列 | 実行したいJavaScriptのコード | ※code例参照 |

#### code例

ScrapePageアクションで情報を取得し、StoreValueアクションで変数booksに格納した後、RunScriptアクションでbooksの値を整える。

```yaml
var element = ${books}; 
var newBook = []; 
for ( let book of element ) { 
　newBook.push(book.split("\n")); 
} 
return newBook;
```

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Anything | 返却された値による | RunScriptの結果 | ※使用例のアウトプット参照 |

### 使用例

```yaml
+run_script_1:
  action>: RunScript
  code: 'var element = ${books};  var newBook = [];  for ( let book of element ) {   newBook.push(book.split("\n")); }   return newBook;'
# => [
#  [
#    "決定版猫と一緒に生き残る防災BOOK",
#    "猫びより編集部",
#    "http://books.google.co.jp/books?id=a5JSvwEACAAJ&dq=%E7%8C%AB&hl=&source=gbs_api",
#    ""
#  ],
#  [
#    "牝の猫と女のネコ",
#    "岩井志麻子",
#    "https://play.google.com/store/books/details?id=VFgVDgAAQBAJ&source=gbs_api",
v    ""
#  ],
#  [
#    "通い猫アルフィーの奇跡",
#    "レイチェル・ウェルズ 中西和美",
#    "https://play.google.com/store/books/details?id=WhkVDQAAQBAJ&source=gbs_api",
#    ""
#  ],
#  [
#   "猫をよろこばせる本",
#    "沼田朗",
#    "https://play.google.com/store/books/details?id=kcgMBvj8pzgC&source=gbs_api",
#    ""
#  ],
#  [
#    "猫の困った行動解決ハンドブック",
#    "高崎一哉",
#    "http://books.google.co.jp/books?id=Szcc61SiSHYC&dq=%E7%8C%AB&hl=&source=gbs_api",
#    ""
#  ]
#]
```



