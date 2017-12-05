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
   seedtableの"yml→xlsx"にドラッグ＆ドロップして、
   編集用Excelを好きな場所に保存してください。
   この操作でmaster_dataにあるデータが編集用Excelに入ります。
5. 編集用Excelを編集してください
6. いい感じになったら編集用Excelをseedtableの"xlsx→yml"にドラッグ＆ドロップして、
   master_dataに編集後のデータを書き出してください。
7. 手元のGitツールで念のため差分確認してからリモートにpushし、プルリクエストを出してください。
8. 本番/staging用ならレビューをもらってください。
   バランス調整サーバー用ならそのままマージしてください。しばらくするとCIでサーバーに反映されます。

## seedtableアップデート方法

エンジニアで判断して`tools/update_seedtable`を叩いてコミットしてください。

## License

[MIT License](https://narazaka.net/license/MIT?2017)
