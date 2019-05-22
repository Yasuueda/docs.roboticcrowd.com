# WebService

Web上のファイルをダウンロードしたり、HTTP要求を送信したりします。

## HTTPRequest

### 概要

HTTPRequestは、HTTPリクエストを送るアクションです。JSONレスポンスのみに対応しています。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| url\* | 文字列 | URL | [https://www.googleapis.com/books/v1/volumes](https://www.googleapis.com/books/v1/volumes) |
| params | オブジェクト | クエリパラメーター | {"q": "ロボット"} |
| method | セレクト | リクエストメソッド | GET、POST、PUT、PATCH、DELETE |
| headers | オブジェクト | ヘッダー | {"Content-Type": "application/json"} |
| multipart | 真理値 | マルチパート | false\(default\) |
| file\_input\_name | 文字列 | アップロードするファイルのパラメーター名。マルチパートのときのみ有効になります。 | +get\_file\_1 |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| JSON | オブジェクト | JSONレスポンス | ※使用例のアウトプット参照 |

### 使用例

Google Books APIsから本のデータを取得する。

```yaml
+h_t_t_p_request_1:
  action>: HTTPRequest
  url: 'https://www.googleapis.com/books/v1/volumes'
  params:
    q: 'チュートリアル'
    langRestrict: ja
    maxResults: 1
  method: GET
  headers: ''
  multipart: false
  # => {
#   "kind": "books#volumes",
#   "totalItems": 2756,
#   "items": [
#     {
#       "kind": "books#volume",
#       "id": "ZCrIJy0LG-MC",
#       "etag": "tku9myZ1oyE",
#       "selfLink": "https://www.googleapis.com/books/v1/volumes/ZCrIJy0LG-MC",
#       "volumeInfo": {
#         "title": "ロボットは涙を流すか",
#         "subtitle": "映画と現実の狭間",
#         "authors": [
#           "石黒浩",
#           "池谷瑠絵"
#         ],
#         "publisher": "PHP研究所",
#         "publishedDate": "2010",
#         "description": "日進月歩の科学はSFを凌駕する!? ロボットが心を持つ日が来るかもしれない。その時、人間とロボットを分かつものはあるのか?",
#         "industryIdentifiers": [
#           {
#             "type": "ISBN_13",
#             "identifier": "9784569775630"
#           },
#           {
#             "type": "ISBN_10",
#             "identifier": "4569775632"
#           }
#         ],
#         "readingModes": {
#           "text": true,
#           "image": true
#         },
#         "pageCount": 189,
#         "printType": "BOOK",
#         "categories": [
#           "Technology & Engineering"
#         ],
#         "maturityRating": "NOT_MATURE",
#         "allowAnonLogging": true,
#         "contentVersion": "2.14.9.0.preview.3",
#         "panelizationSummary": {
#           "containsEpubBubbles": false,
#           "containsImageBubbles": false
#         },
#         "imageLinks": {
#           "smallThumbnail": "http://books.google.com/books/content?id=ZCrIJy0LG-MC&printsec=frontcover&img=1&zoom=5&edge=curl&source=gbs_api",
#           "thumbnail": "http://books.google.com/books/content?id=ZCrIJy0LG-MC&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api"
#         },
#         "language": "ja",
#         "previewLink": "http://books.google.com/books?id=ZCrIJy0LG-MC&printsec=frontcover&dq=%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88&hl=&cd=1&source=gbs_api",
#         "infoLink": "http://books.google.com/books?id=ZCrIJy0LG-MC&dq=%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88&hl=&source=gbs_api",
#         "canonicalVolumeLink": "https://books.google.com/books/about/%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88%E3%81%AF%E6%B6%99%E3%82%92%E6%B5%81%E3%81%99%E3%81%8B.html?hl=&id=ZCrIJy0LG-MC"
#       },
#       "saleInfo": {
#         "country": "US",
#         "saleability": "NOT_FOR_SALE",
#         "isEbook": false
#       },
#       "accessInfo": {
#         "country": "US",
#         "viewability": "PARTIAL",
#         "embeddable": true,
#         "publicDomain": false,
#         "textToSpeechPermission": "ALLOWED",
#         "epub": {
#           "isAvailable": true,
#           "acsTokenLink": "http://books.google.com/books/download/%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88%E3%81%AF%E6%B6%99%E3%82%92%E6%B5%81%E3%81%99%E3%81%8B-sample-epub.acsm?id=ZCrIJy0LG-MC&format=epub&output=acs4_fulfillment_token&dl_type=sample&source=gbs_api"
#         },
#         "pdf": {
#           "isAvailable": true,
#           "acsTokenLink": "http://books.google.com/books/download/%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88%E3%81%AF%E6%B6%99%E3%82%92%E6%B5%81%E3%81%99%E3%81%8B-sample-pdf.acsm?id=ZCrIJy0LG-MC&format=pdf&output=acs4_fulfillment_token&dl_type=sample&source=gbs_api"
#         },
#         "webReaderLink": "http://play.google.com/books/reader?id=ZCrIJy0LG-MC&hl=&printsec=frontcover&source=gbs_api",
#         "accessViewStatus": "SAMPLE",
#         "quoteSharingAllowed": false
#       },
#       "searchInfo": {
#         "textSnippet": "日進月歩の科学はSFを凌駕する!? ロボットが心を持つ日が来るかもしれない。その時、人間とロボットを分かつものはあるのか?"
#       }
#     }
#   ]
# }
```

## DownloadFile

### 概要

DownloadFileは、URLにあるファイルをダウンロードするアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| url\* | 文字列 | ダウンロードするファイルのURL | [https://images.unsplash.com/photo-1522518961115-07c922089dd4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2734&q=80](https://images.unsplash.com/photo-1522518961115-07c922089dd4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2734&q=80) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | ダウンロードしたファイル | /tmp/ac44342d-d956-4818-b3ee-e3d4990b06c8/web\_files/photo-1522518961115-07c922089dd4 |

### 使用例

```yaml
+download_file_1:
  action>: DownloadFile
  url: 'https://images.unsplash.com/photo-1522518961115-07c922089dd4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2734&q=80'
  # => "/tmp/ac44342d-d956-4818-b3ee-e3d4990b06c8/web_files/photo-1522518961115-07c922089dd4"
```

