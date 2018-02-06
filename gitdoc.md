# Git の使い方．

- [Bash に関して](#bash-%E3%81%AB%E9%96%A2%E3%81%97%E3%81%A6)
- [Git 管理　＜ローカル編＞](#git-%E7%AE%A1%E7%90%86-%EF%BC%9C%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E7%B7%A8%EF%BC%9E)
- [Git 管理　＜リモート編＞](#git-%E7%AE%A1%E7%90%86-%EF%BC%9C%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E7%B7%A8%EF%BC%9E)
- [Git 管理　＜ブランチ編＞](#git-%E7%AE%A1%E7%90%86-%EF%BC%9C%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E7%B7%A8%EF%BC%9E)
- [Git 管理　＜他人の Repo 編＞](#git-%E7%AE%A1%E7%90%86-%EF%BC%9C%E4%BB%96%E4%BA%BA%E3%81%AE-repo-%E7%B7%A8%EF%BC%9E)

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

* .gitignore ファイルに"file_c"を追記

```sh
touch .gitignore  # .gitignore の作成
echo "file_c" >> .gitignore
```

* Git の状態を表示

```sh
git status
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

* リモートリポジトリの一覧を表示

```sh
git remote
```

## Git 管理　＜ブランチ編＞

* ブランチを切って作業する

```sh
git branch dev  # dev というブランチを追加
git checkout dev  # dev に移動

# 以下のコマンドで，上２つのコマンドを同時に実行できる
git checkout -b dev
```

* リモートの dev ブランチにプッシュ

```sh
git push origin dev

# その後 GitHub ページにてプルリクエスト，レビューしてマージ
```

* ローカルの master ブランチにマージ，リモートにプッシュ

```sh
git checkout master  # master ブランチに移動
git merge dev  # マージ
git branch -d dev  # dev ブランチ削除．しなくてもよい．
git push
```

* ブランチ名の一覧を表示

```sh
git branch
```

## Git 管理　＜他人の Repo 編＞

リポジトリ"Robot-Lancer"の持ち主を"Tinblackstar"，自分のユーザ名を"Sample"とする．

* Fork してできた Sample/Robot-Lancer というリポジトリをローカルにクローン

```sh
git clone git@github.com:Sample/Robot-Lancer.git
```

* 変更を Sample/Robot-Lancer にプッシュ

```sh
git push

# その後，Tinblackstar/Robot-Lancer にプルリクを送り，
# レビューを行ったあと Tinblackstar がマージ．
```

* 自動的には Tinblackstar/Robot-Lancer での変更は Sample/Robot-Lancer には反映されないので，対処

```sh
# 元のリポジトリを"upstream"という名でリモートに追加
git remote add upstream git@github.com:Tinblackstar/Robot-Lancer.git

# upstream での変更をローカルに反映
git pull upstream master
git rebase master

# さらに Sample/Robot-Lancer に反映
git push
```
