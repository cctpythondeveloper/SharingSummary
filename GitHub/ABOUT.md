# GitHubとは
GitHub: ソースコード管理システム

主な機能
- ソースコードの閲覧
- 簡単なバグ管理機能
- SNS
- など

## ローカルリポジトリとリモートリポジトリ
リポジトリ: ファイルやディレクトリの状態を保存する場所．
変更履歴を管理したいファイルやディレクトリをリポジトリの管理下に置くことで，そのディレクトリ内のファイルなどの変更履歴を記録できる

リポジトリは自分のPCにある**ローカルリポジトリ**とサーバなどのネットワーク上にある**リモートリポジトリ**が存在する．
開発社はローカルリポジトリで作業を行い，その作業内容をリモートリポジトリへプッシュする．

![](./figs/about-1.png)

## コミットとプッシュ
- コミット(commit): ファイルの追加や変更の履歴をローカルリポジトリに保存すること
- プッシュ(push): ファイルの追加や変更の履歴をリモートリポジトリにアップロードするための操作

## ブランチ
ソフトウェアの開発では，現在リリースしているバージョンのメンテナンスをしながら新たな機能追加やバグ修正を行うことがある．
このように，並行して行われる複数のバージョン管理を行うためにGitにはブランチ(branch)という機能がある．

ブランチは履歴の流れを分岐して記録していくものである．
分岐したブランチは他のブランチの影響を受けないため，同じリポジトリ内でそれぞれの開発を行っていくことができる．

## GitHubの流れ(Web(GitHub)とCUI(コマンドプロンプト/ターミナル))

1. [GitHubでリポジトリを作成する](#repository)
2. [リモートリポジトリからローカルリポジトリに持ってくる(clone/クローン)](#clone)
3. ファイルを作成/編集/削除する
4. [ファイルの作成/編集/削除をgitのインデックスに追加する](#add)
5. [変更結果をローカルリポジトリにコミットする](#commit)
6. [ローカルリポジトリでコミットした内容をリモートリポジトリへプッシュする(反映させる)](#push)

<a name="repository"></a>
#### リポジトリの作成
![](./figs/about-2.png)

---

![](./figs/about-3.png)

- Owner: リポジトリの管理者
- Repository name: リポジトリの名前
- Description(optional): そのリポジトリの名前
- Public/Private: そのリポジトリを公開する(Public)か公開しない(Private)か
- Initialize this repository with a README: [README](#README)をトップページに追加するかどうか
- Add .gitignore: [gitignore](#gitignore)のデフォルト設定
- Add a license: ライセンスを追加するかどうか

<a name="clone"></a>
#### クローン

![](./figs/about-4.png)

ここのURLをコピーして使用する

```shell
$ git clone https://github.com/<Owner名>/<リポジトリ名>.git

~/GitHub ❯❯❯ git clone https://github.com/Sylphy0052/SharingSummary.git
Cloning into 'SharingSummary'...
warning: You appear to have cloned an empty repository.
```

<a name="add"></a>
#### ファイルの作成/編集/削除をgitのインデックスに追加する

```shell
# ファイルの状態を表示する
$ git status
# ファイルを追加する
$ git add <ファイル名>
~/G/SharingSummary ❯❯❯ git add README.md
```

<a name="commit"></a>
#### 変更結果をローカルリポジトリにコミットする

```shell
# コミットする
$ git commit -m "<コミットメッセージ>"
```

<a name="push"></a>
#### ローカルリポジトリでコミットした内容をリモートリポジトリへプッシュする(反映させる)

```shell
$ git push <レポジトリのURLの別名> <ブランチ名>
# originのmasterブランチにプッシュする
$ git push origin master
```

<a name="readme"></a>
### README
このシステムの説明書的な文書ファイル．
通常Markdown方式で書かれている．

<a name="gitignore"></a>
### gitignore
`.gitignore`ファイルを使用すると，コミットを無視するファイルやディレクトリを指定することができる．
ビルドファイルや個人的に作ったものをここに記入し，コミットしないようにする．

例えば，`test.txt`ファイルや`build`ディレクトリ以下のものを無視したい場合，
```
test.txt
/build
```
と書く．

<a name="branch"></a>
## ブランチの使い方

```shell
# ブランチの一覧
$ git branch
# ブランチの作成
$ git branch <ブランチ名>
# ブランチの移動
$ git checkout <ブランチ名>
# ブランチを作成しつつ移動
$ git checkout -b <ブランチ名>
# masterブランチにdevelopの内容をpullする
$ git checkout master
$ git pull origin develop
# ブランチの削除
$ git branch -d <ブランチ名>
```

### マージ
機能ごとにブランチを作って開発を行い，テストが終了したらそれを別のブランチに取り込む．この取り込むことを`マージ(merge)`という．

```shell
# func1ブランチをdevelopブランチに取り込む
$ git checkout develop
$ git merge func1
# 最後にpushする
$ git push origin develop
```

### つまり…
1. developブランチから新規ブランチを作る
2. プログラムを作成する
3. addする
4. commitする
5. 2~4を繰り返す
6. pushする

という流れになる．

```shell
# developブランチに切り替える
$ git checkout develop
# developブランチを最新状態にする
$ git pull origin develop
# ブランチを切ってブランチを変更する
$ git checkout -b <ブランチ名>
# 編集
# addする
$ git add <ファイル名>
# commitする
$ git commit -m "<コミットメッセージ>"
# add,commitをこまめに繰り返す
# ある程度機能ができたらpushする
$ git push origin <ブランチ名>
# 最初に戻る
```

<a name="ref"></a>
## 参考
- [今さら聞けない！GitHubの使い方【超初心者向け】](https://techacademy.jp/magazine/6235)
