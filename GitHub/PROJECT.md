# プロジェクト管理
## タブ
GitHubのリポジトリのメイン画面
- Code: ソースコードが見れる
- Issues
- Pull requests
- Projects

## リポジトリの初期設定
1. リポジトリを作る
2. Settingタブ→Collaboratorsタブ→共同開発者を追加
3. Projectsタブ→Create a project→Project board name，(Description),を書いて，Project templateをAutomated kanban with reviewsに設定する

![](./figs/project-1.png)

機能毎に分けるか，日付ごとに分けるかなど工夫することでToDoを見やすくできる

4. To doカラムのManageの設定

![](./figs/project-2.png)

---

![](./figs/project-3.png)

5. In progressの設定

![](./figs/project-4.png)

6. Review in progressの設定

![](./figs/project-5.png)

7. Reviewer approvedの設定

![](./figs/project-6.png)

8. Doneの設定

![](./figs/project-7.png)

9. IssuesタブのLabelsを追加する

![](./figs/project-8.png)

ラベルはIssueの状態を表すことができ，複数つけることができる．

- 0.優先度(高)
- 0.優先度(中)
- 0.優先度(低)
- 0.優先度(なし)
- 1.バグ
- 1.機能追加
- 1.機能変更
- 1.デザイン
- 1.質問/相談
- 1.リファクタリング
- 1.その他
- 99.再現しない
- 99.おたすけ要請
- WIP
- レビュー待ち

0: 優先度の設定．高から順に対応していく

1: Issueの種類

99:おたすけ
- `99.再現しない`はバグ報告があったがその現象にならないとき
- `99.おたすけ要請`は自分では解決できないとき

その他: 現在の状況
- `WIP(Work In Progress)`は現在対応中のラベル
- `レビュー待ち`はプルリクエストを送った後

![](./figs/project-9.png)

10. ラベルの1に合わせてIssueのテンプレートを作る

例: バグのテンプレート - `.github/ISSUE_TEMPLATE/BUG.md`
```
---
name: バグ報告
about: バグの報告
title: "[BUG]: " ←プレフィックスを付けると分かりやすい
labels: バグ報告 ←設定したラベルと同じもの
assignees: ''

---

#### バグの説明

#### 再現方法

1.
2.
3.

#### 期待される結果

-

#### 実際の結果

-

#### 追加情報(詳細/スクショ)

- ![Screenshot]()
-

```

11. プルリクエストのテンプレートを作る

例) `.github/PULL_REQUEST_TEMPLATE.md`
```
#### 対応issue

close/fix/resolve #<issue番号>

#### 実装内容

何を実装したのか

#### 備考

注意点など

```

12. マイルストーンの追加

![](./figs/project-10.png)

1日ごと，もしくは機能や時間(13:00や午前中など)で細かく分ける

13. `develop`ブランチを作る(統合テスト用)．masterブランチは最後以外触れない

14. もし共有したいことがあればWikiに記入

## プロジェクトの進め方
- WBSなどのエクセルファイルはGoogleスプレッドシートのリンクを`README.md`やWikiに書いて共有する→GoogleスプレッドシートやGoogleスライドは複数人同時に編集可能
- 基本はIssueを追加していく

![](./figs/project-11.png)

![](./figs/project-12.png)

- Title: Issueの概要
- Comment: Issueの細かい内容
- Assignees: 担当者
- Labels: 作ったラベルを選択する．少なくとも0と1は必ずつける
- Projects: どのプロジェクトボードで管理するかの紐付け
- Milestone: 作ったマイルストーンを選択する

CommentにはMarkdown記法が使える．書き方は[こちら](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)を参照．

Assigneesは基本空にしておいて，担当者が決まったら追加する．

![](./figs/project-13.png)

Issueを作るとProjectsのボードに自動で追加される

![](./figs/project-14.png)

Issueは大枠を作ってチェックボックスで細かいTo Doを作ると良い．
その細かいTo Doで更にIssueを書くと細分化できる．

Issueとプルリクエストの連携
```
{キーワード} #{イッシュー番号}

# 例
fix #1
```
これをプルリクエストに追加すると，Issueを自動で閉じてくれる

キーワード
- close
- fix
- resolve

## 開発者フロー
1. Issueを作る(PMがやってもよい)
2. Projectsのプロジェクトボードの`To do`から`In progress`に移動させる
2. Branchを作る(基本的には`issue001`などissueでブランチ名をつける)
3. 空コミットする
4. 途中でタイトルに`[WIP]`をつけてプルリクエストを出す(ToDoリストや終わっていないことを書いておくと良い)
5. レビュアをアサインする(基本PMなど全体がわかっている人)
6. コードを書く
7. 終わったら`[WIP]`を外し，レビュアにメンション(`@ユーザ名`)する
8. Projectsのプロジェクトボードの`In progress`から`Review in progress`に移動させる
8. レビューを受けコードを修正する
9. うまくいったらマージしてもらう
10. 1に戻る

## PMフロー
1. Issueを作る
2. Issueをアサインする
3. 開発社から`[WIP]`がついていないプルリクエストまたはメンションされたら対応する
4. プルリクエストに対してはレビューを書く
5. そのブランチをローカルに持ってきてテストする
6. 問題がなかった場合，マージする

## 参考
- [Qiita: 新入社員におくるGitHubでのプロジェクト管理の初歩](https://qiita.com/gumimin/items/63dcb36d4730213bd63a)
