# サンプルマスターデータ

## フォルダ構成

- tools/: ツールを置いてある seedtableなど
- templates/: テンプレートxlsxは適当な単位でテーブルまとめてここへ
- master_data/: マスターデータ

## Excelでデータを編集するときの手順

1. リポジトリをmasterブランチまたはその時点での開発ブランチにします(`git checkout master` or `git checkout develop-1.2.0`)
2. リポジトリを更新します(`git pull`)
3. seedtable-gui.exeを立ち上げます
4. templatesフォルダにあるそれっぽいテンプレートExcel
   （キャラクターならcharacters.xlsx、クエストならquest.xlsx等）を
   seedtableの"yml→X"にドラッグ＆ドロップして、
   編集用Excelを好きな場所に保存してください。
   この操作でmaster_dataにあるデータが編集用Excelに入ります。
5. 編集用Excelを編集してください
6. いい感じになったら編集用Excelをseedtableの"X→yml"にドラッグ＆ドロップして、
   master_dataに編集後のデータを書き出してください。
7. 手元のGitツールで念のため差分確認してからリモートにpushし、プルリクエストを出してください。
8. 本番/staging用ならレビューをもらってください。
   バランス調整サーバー用ならそのままマージしてください。しばらくするとCIでサーバーに反映されます。

## テンプレートまわり

自動生成の都合で以下のように設定して射ます。

### シート

- テーブルを表すシート名はフルネームで記載(charactersテーブルはcharactersシート)
- 長すぎて入らないテーブル名は適当に略して設定に`mapping`オプションを指定して対応します。
    - 例: `mapping: ["character_quest_special_parameter_condifions:character_quest_SPCNDS"]`
- Excel外部参照は使わず、`primary`オプションでマスターとなるxlsxファイルを指定して、参照するxlsxからは同名シートを作って参照することとします(同名シートだけどマスターとなるxlsxファイル以外からはそのシートが書き出されない)。
- テーブル外の設定記述用シートなどは`__`をシート名の先頭につけてください（書き出されなくなります）。

### カラム

- 2行目の文字列がカラム名、3行目以降がデータ行です。
- `__dummy`という名前のカラムはymlデータ出力時に無視されます。
- そのほかの`__`で始まるカラム名はymlには出力されますがサーバーには反映されません。
  意図やメモなどを残すことができます。

### 制約

- A:AやA:Dなど行指定なしの範囲指定はエラーになります。`$`固定の範囲を取ることで回避できます。
    - 例: A:AであればA$1:A$100000とか

## seedtableアップデート方法

エンジニアで判断して`tools/update_seedtable`を叩いてコミットしてください。

## インストールするもの

### Windows

.NET Frameworkの4あたりが入っていれば特にすることはないはずです。

### Linux/Macの人

seedtableを動かすためにmonoがいるので、 http://www.mono-project.com/download/ のOlder releasesからでダウンロードできる5.0.1をダウンロードしてください。（5.4ではGUI版が動かないようです。)

あとどうもbrewのやつはダメっぽいです。

## License

[MIT License](https://narazaka.net/license/MIT?2017)
