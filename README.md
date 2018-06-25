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
```javascript
const shape = new createjs.Shape();
shape.graphics
  .beginFill('green') // 塗りの設定
  .drawCircle(50, 50, 50); // x座標50、y座標50、半径50の円を作成

stage.addChild(shape); // stageの子要素に挿入
state.update(); // stageの更新
```


## インタラクションの実装

### マウスオーバー、マウスアウト
- マウスオーバー、マウスアウトを使う場合は、`stage.enableMouseOver()` を実行する必要がある。
