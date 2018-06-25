本リポジトリは、[CreateJS入門サイト - ICS MEDIA](https://ics.media/tutorial-createjs/index.html) を参考にしながら実際に試したコードなどを残しておくリポジトリです。
また、学んだ内容は下記に簡単にまとめていきます。

# createJSとは
- HTML5 Canvasというテクノロジーを中心に構築された、リッチコンテンツを制作するためのJSライブラリのスイート（特定用途のソフトウェアを詰め合わせたパッケージ）
  - **EaselJS** : HTML5 Canvasでの制作を扱うためのJSライブラリ。
  - **TweenJS** : JavaScriptのトゥイーンエンジン。
  - **SoundJS** : サウンドを利用するためのJSライブラリ。簡単にクロスブラウザでの音声再生が実現できる。
  - **PreloadJS** : 素材（画像、音声、JS、データ）を先読みできるJSライブラリ
- FlashデベロッパーのGrant Skinner氏が代表を務めるgskinner社が開発

## createJSの事例
- https://lab.gskinner.com/
- http://sandbox.createjs.com/PlanetaryGary/
- http://ics-web.jp/projects/pollenmap/
- http://jsdo.it/tag/createjs?search_order=favorite

## CDNのURL
```javascript
<script src="https://code.createjs.com/1.0.0/createjs.min.js"></script>
```

# 描画の基本
## stageの作成
```javascript
const stage = new createjs.Stage('ID');
```

## シェイプの作成
基本
```javascript
const shape = new createjs.Shape();
shape.graphics
  .beginFill('green') // 塗りの設定
  .drawCircle(50, 50, 50); // x座標50、y座標50、半径50の円を作成

stage.addChild(shape); // stageの子要素に挿入
state.update(); // stageの更新
```

### 円の作成
```javascript
Graphicsオブジェクト.drawCircle(中心のX座標, 中心のY座標, 半径);
```

### 四角形の作成
```javascript
Graphicsオブジェクト.drawRect(X座標, Y座標, 横幅, 高さ);
```

### 角丸四角形の作成
```javascript
Graphicsオブジェクト.drawRoundRect(X座標, Y座標, 横幅, 高さ, 角丸の大きさ);
```

### 多角形の作成
```javascript
Graphicsオブジェクト.drawPolyStar(x座標, y座標, 半径, 頂点数, 谷の深さ, 起点角)
```
- 第5引数の谷の深さは、 `0` 以上 `1` 未満の数値を設定。
デフォルト値の `0` を渡すと谷はなくなり、正多角形になり、 `0.9` だと鋭くなる。
- 第6引数の起点角は頂点の角度で、デフォルト値 `0` ではx軸の正方向つまり時計の3時の方向を起点に描かれる。
y軸の負つまり時計の12時の方向から描くには、`-90` を起点の角度にする。

### 任意の図形の作成
```javascript
Graphicsオブジェクト.moveTo(x座標, y座標);
Graphicsオブジェクト.lineTo(x座標, y座標);
```
`moveTo()` メソッドで現在の描画位置を移動し、 `lineTo()` で現在の描画位置から次の描画位置まで現在の線のスタイルを使用して線を描画する。


## 塗りの設定
```javascript
shape.graphics.beginFill('tomato'); // color name
shape.graphics.beginFill('#e00'); // 16進数
shape.graphics.beginFill('rgba(33, 200, 100, 1)'); // rgba

shape.graphics.beginFill('rgb(33, 200, 100)'); // rgb①
shape.graphics.beginFill(createjs.Graphics.getRGB(255, 0, 0)); // rgb②

shape.graphics.beginFill('hsl(30, 30%, 80%)'); // HSL①
shape.graphics.beginFill(createjs.Graphics.getHSL(30, 30, 80)); // HSL②
```



## インタラクションの実装

### マウスオーバー、マウスアウト
- マウスオーバー、マウスアウトを使う場合は、`stage.enableMouseOver()` を実行する必要がある。

### ドラッグ アンド ドロップ
```javascript
// マウスダウンされた時の処理（一度だけ発生）
ball.addEventLinstener('mousedown', handleDown);
// マウスダウンされた状態でマウスを動かしたとき時の処理（連続して発生）
ball.addEventLinstener('pressmove', handleMove);
// マウスダウンされた状態からマウスが離れたときの処理（一度だけ発生）
ball.addEventLinstener('pressup', handleUp);
```

### タッチデバイス対応
`createjs.Touch` クラスを使ってタッチ操作を有効にすることで、自動的にタッチイベントがマウスイベントに変換される。
そのため、特別な処理を実装する必要がない。

```javascript
// タッチ操作をサポートしているブラウザの場合
if (createjs.Touch.isSupported()){
  // タッチ操作を有効にする
  createjs.Touch.enable(stage);
}
```
