# Git の使い方．

## Bash に関して

* 起動方法

1. `Windows` + `R` を押して「ファイル名を指定して実行」というウィンドウを開く．
1. Bash と入力して `Enter`．

* 基本的なコマンド

  * ディレクトリ移動 `cd <DIRECTORY>`
  * ディレクトリ作成 `mkdir <DIRECTORY>`
  * ファイル作成 `touch <FILE>`
  * ディレクトリ削除 `rm -r <DIRECTORY>`
  * ファイル削除 `rm <FILE>`

## Git 管理　＜ローカル編＞

ローカルのディレクトリ名を"ROBOT"とする．

* ROBOT に移動

```sh
cd ROBOT
```

* git リポジトリの新規作成

```sh
git init
```

次に，ファイル"file_a"を追加・編集したとする．

* file_a（を含む全ての新ファイル）を git 管理下に置く

```sh
git add -A
```

* file_a（を含む全てのファイル）の変更をコミット

```sh
git commit -am "Add file_a"
```

また，既に何度かコミット済のファイル"file_b"に新しく変更を加えたとする．

* file_b（のみ）の変更をコミット

```sh
git commit -m "Update file_b" file_b
```

更に，ファイル"file_c"を追加したが git 管理下に置きたくないとする．

* .gitignore ファイルに"file_c"を追記．

```sh
touch .gitignore  # .gitignore の作成
echo "file_c" >> .gitignore
```

## Git 管理　＜リモート編＞

* リモートリポジトリを登録

```sh
git remote add origin git@github.com:Tinblackstar/Robot-Lancer.git
```

* リモートでの変更をローカルに反映

```sh
git pull
```

* ローカルでの変更をリモートに反映

```sh
# 最初は
git push -u origin master
# ２回目以降
git push
```
