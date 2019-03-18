# Storage

ファイルをクラウドサービスに保存したり、クラウドサービスから取得したりします。

## SaveFile

### 概要

SaveFileは、ファイルを保存するアクションです。
directoryパラメータを設定することで、ファイルの保存先を指定できます。directoryパラメータで設定した保存先がない場合、Dropboxはフォルダが自動生成されますが、その他のプロバイダはエラーとなります。
create_Pathパラメータをtrueにすることで、保存先のパスを新たに作成することができます。
ファイルの保存先が未設定の場合は、「Robotic Crowd」フォルダに保存します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列、画像、ファイル | 保存するファイル。ファイルはフルパスで指定されますが、指定できるのはワークフロー内でダウンロードしたものや作成したファイルのみです。 | +download_file_1 |
| provider\* | 文字列 | 利用するコネクションのプロバイダID。デフォルトではRobotic Crowdのストレージ(local)が使用されます。local、Google Drive、Dropbox、boxが利用できます。 | local(default) |
| directory | 文字列 | 保存先のパス。指定がない場合、/[アプリ]/RoboticCrowd/yyyy-mm-dd/になります。ルートディレクトリに保存したい場合は、'/'を指定してください。 | /spring/sakura |
| createPath | 真理値 | trueの場合、保存先のパスを新たに作成します。 | false(default) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| Object | オブジェクト | ストレージ保存のレスポンス | ※使用例のアウトプット参照 |

### 使用例

```yaml
+save_file_1:
  action>: SaveFile
  filename: +download_file_1
  provider: gdrive_********************
  directory: 'spring/sakura'
  createPath: true
  # => {
#   "file_id": "1Y2O5qBUBIPpiZfd9gW1UqehiZoXHBysJ",
#   "filename": "photo-1552521923-b46b3137bab3"
# }
```

## GetFile

### 概要

GetFileは、ファイルを取得するアクションです。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列、画像、ファイル | 取得するファイルのID、もしくは、パス（この値の形式は、プロバイダーごとに異なります。） | rc_33b74e85777203729f2d |
| provider\* | 文字列 | 利用するコネクションのプロバイダID | local(default) |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | 取得したファイル | /tmp/02975d17-a685-4054-9859-d26a2baca435/gdrive_4d58af37ea2b6c4dfb8c/today_sakura |

### 使用例

```yaml
+get_file_1:
  action>: GetFile
  filename: '/spring/sakura/today_sakura'
  provider: gdrive_********************
  # => "/tmp/02975d17-a685-4054-9859-d26a2baca435/gdrive_4d58af37ea2b6c4dfb8c/today_sakura"
```

## RenameFile

### 概要

RenameFileは、ファイルの名前を変更するアクションです。拡張子も変更しますのでご注意ください。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列、画像、ファイル | 対象ファイル。ファイルはフルパスで指定されますが、指定できるのはワークフロー内で取得したものや作成したファイルのみです。 | +get_file_1 |
| save_as\* | 文字列 | 新しいファイル名。拡張子も正しいものを入力してください。 | sakura |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | 名前を変更したファイル | /tmp/b6b90347-f455-43ce-af42-f6ba8f17a920/local/新集計表.xlsx |

### 使用例

```yaml
+rename_file_1:
  action>: RenameFile
  filename: +get_file_1
  save_as: '新集計表.xlsx'
  # => "/tmp/b6b90347-f455-43ce-af42-f6ba8f17a920/local/新集計表.xlsx"
```

## CompressFile

### 概要

CompressFileは、ファイルをZipで圧縮するアクションです。filesパラメータで圧縮対象のファイルを配列で設定します。ファイルを複数設定した場合、アウトプットのファイルパスは、files[0]のディレクトリ名/archive.zipとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| files\* | 配列 | 対象ファイルのパス | ["/tmp/1322ce71-4c37-480a-bf23-9035a47be089/local/turn_pages.jpeg"] |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | 圧縮したファイル | /tmp/1322ce71-4c37-480a-bf23-9035a47be089/local/turn_pages.zip |

### 使用例

```yaml
+compress_file_1:
  action>: CompressFile
  files: +create_list_1
  # => "/tmp/1322ce71-4c37-480a-bf23-9035a47be089/local/turn_pages.zip"
```

