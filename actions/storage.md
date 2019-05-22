# Storage

ファイルをクラウドサービスに保存したり、クラウドサービスから取得したりします。

## SaveFile

### 概要

SaveFileは、ファイルを保存するアクションです。 directoryパラメータを設定することで、ファイルの保存先を指定できます。directoryパラメータで設定した保存先がない場合、Dropboxはフォルダが自動生成されますが、その他のプロバイダはエラーとなります。 createPathパラメータをtrueにすることで、保存先のパスを新たに作成することができます。 ファイルの保存先が未設定の場合は、「Robotic Crowd」フォルダに保存します。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| filename\* | 文字列、画像、ファイル | 保存するファイル。ファイルはフルパスで指定されますが、指定できるのはワークフロー内でダウンロードしたものや作成したファイルのみです。 | +download\_file\_1 |
| provider\* | 文字列 | 利用するコネクションのプロバイダID。デフォルトではRobotic Crowdのストレージ\(local\)が使用されます。local、Google Drive、Dropbox、boxが利用できます。 | local\(default\) |
| directory | 文字列 | 保存先のパス。指定がない場合、/\[アプリ\]/RoboticCrowd/yyyy-mm-dd/になります。ルートディレクトリに保存したい場合は、'/'を指定してください。 | /spring/sakura |
| createPath | 真理値 | trueの場合、保存先のパスを新たに作成します。 | false\(default\) |

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

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x540D;&#x524D;</th>
      <th style="text-align:left">&#x578B;</th>
      <th style="text-align:left">&#x6982;&#x8981;</th>
      <th style="text-align:left">&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">filename*</td>
      <td style="text-align:left">&#x6587;&#x5B57;&#x5217;&#x3001;&#x753B;&#x50CF;&#x3001;&#x30D5;&#x30A1;&#x30A4;&#x30EB;</td>
      <td
      style="text-align:left">&#x53D6;&#x5F97;&#x3059;&#x308B;&#x30D5;&#x30A1;&#x30A4;&#x30EB;&#x306E;ID&#x3001;&#x3082;&#x3057;&#x304F;&#x306F;&#x3001;&#x30D1;&#x30B9;&#x3002;&#x30D5;&#x30A1;&#x30A4;&#x30EB;&#x30D1;&#x30B9;&#x3067;&#x306E;&#x6307;&#x5B9A;&#x306F;&#x3001;box,
        google drive, dropbox&#x306E;&#x30D7;&#x30ED;&#x30D0;&#x30A4;&#x30C0;&#x30FC;&#x3067;&#x5BFE;&#x5FDC;&#x3057;&#x3066;&#x304A;&#x308A;&#x307E;&#x3059;&#x3002;&#xFF08;&#x3053;&#x306E;&#x5024;&#x306E;&#x5F62;&#x5F0F;&#x306F;&#x3001;&#x30D7;&#x30ED;&#x30D0;&#x30A4;&#x30C0;&#x30FC;&#x3054;&#x3068;&#x306B;&#x7570;&#x306A;&#x308A;&#x307E;&#x3059;&#x3002;&#xFF09;</td>
        <td
        style="text-align:left">
          <p>file_id&#x3067;&#x306E;&#x6307;&#x5B9A;:</p>
          <p>rc_33b74e85777203729f2d</p>
          <p>&#x30D1;&#x30B9;&#x3067;&#x306E;&#x6307;&#x5B9A;:</p>
          <p>/path/to/file/image.jpg</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">provider*</td>
      <td style="text-align:left">&#x6587;&#x5B57;&#x5217;</td>
      <td style="text-align:left">&#x5229;&#x7528;&#x3059;&#x308B;&#x30B3;&#x30CD;&#x30AF;&#x30B7;&#x30E7;&#x30F3;&#x306E;&#x30D7;&#x30ED;&#x30D0;&#x30A4;&#x30C0;ID</td>
      <td
      style="text-align:left">local(default)</td>
    </tr>
  </tbody>
</table>### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | 取得したファイル | /tmp/02975d17-a685-4054-9859-d26a2baca435/gdrive\_4d58af37ea2b6c4dfb8c/today\_sakura |

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
| filename\* | 文字列、画像、ファイル | 対象ファイル。ファイルはフルパスで指定されますが、指定できるのはワークフロー内で取得したものや作成したファイルのみです。 | +get\_file\_1 |
| save\_as\* | 文字列 | 新しいファイル名。拡張子も正しいものを入力してください。 | 新集計表.xlsx |

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

CompressFileは、ファイルをZipで圧縮するアクションです。filesパラメータで圧縮対象のファイルを配列で設定します。ファイルを複数設定した場合、アウトプットのファイルパスは、files\[0\]のディレクトリ名/archive.zipとなります。

### パラメーター

\*は、必須パラメーター

| 名前 | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| files\* | 配列 | 対象ファイルのパス | \["/tmp/1322ce71-4c37-480a-bf23-9035a47be089/local/turn\_pages.jpeg"\] |

### アウトプット

| タイプ | 型 | 概要 | 例 |
| :--- | :--- | :--- | :--- |
| File | ファイル | 圧縮したファイル | /tmp/1322ce71-4c37-480a-bf23-9035a47be089/local/turn\_pages.zip |

### 使用例

```yaml
+compress_file_1:
  action>: CompressFile
  files: +create_list_1
  # => "/tmp/1322ce71-4c37-480a-bf23-9035a47be089/local/turn_pages.zip"
```

