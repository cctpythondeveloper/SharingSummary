# コミットについて

## プレフィックスをつけよう
プレフィックスはコミットメッセージの前につける識別子のことである．

- fix: バグ修正
- add: 新規ファイル作成
- update: 機能修正
- change: 仕様変更
- clean: リファクタリングやファイルの移動
- disable: コメントアウトなどの無効化
- remove: ファイルの削除
- upgrade: バージョンアップ
- revert: 変更取消

例)
```
index.htmlの追加
add: トップページの追加
login.pyの修正
fix: 誰でもログインできてしまうバグの修正
change: loginメソッドの仕様変更
```

ひと目で何をしたかわかるようなコミットメッセージを書こう

## 参考
- [Qiita: Gitのコミットメッセージの書き方] (https://qiita.com/itosho/items/9565c6ad2ffc24c09364)
