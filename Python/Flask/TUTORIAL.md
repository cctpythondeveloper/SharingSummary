# Flaskチュートリアル

## 最小規模のFlaskアプリケーション

```python
# flaskというモジュールからFlaskというクラスをインポートする
from flask import Flask

# appという変数にFlaskオブジェクトを格納する(Javaのnewと同じ)
app = Flask(__name__)

# アプリケーションを実行するURLを指定
# '/'はindex.htmlと同じ
@app.route('/')
# defで関数を作成
def hello_world():
  return "Hello World!"

# main関数
# おまじないみたいなもの
if __name__ == '__main__':
  # サーバの実行
  app.run()
```

### 説明
`Flask(__name__)`の`__name__`はどのクラスからこのプログラムが実行されたかを表している．
mainとして呼ばれた(直接実行された)場合は`__name__ = __main__`であり，モジュールとして呼ばれた場合はインポート名が呼ばれる．

`@app.route`はURLを指定する．
例えば`@app.route('/')`とした場合，その関数が実行されるのは`http://127.0.0.1:5000/`であり，`@app.route('/hello')`とした場合，その関数が実行されるのは`http://127.0.0.1:5000/hello/`である．

### URLに変数を入れる
マジ便利な機能．
例えばUser毎にページを変えたい場合，Userの情報が分かればその情報から各ページに移動することができる．

```python
@app.route('/user/<username>')
def show_user_profile(username):
    return "User Name is {}".format(username)

@app.route('/user/<id:user_id>')
def show_user_id(user_id):
    return "User ID is {}".format(user_id)
```

`http://127.0.0.1:5000/taro`のURLに飛ぶと，ブラウザには`User Name is taro`と表示され，`http://127.0.0.1:5000/1`とすると，`User ID is 1`と表示される．
IDで表示される情報を決める場合にわざわざ変数の受け渡しをする必要がなくなる．
