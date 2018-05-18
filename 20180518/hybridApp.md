# ハイブリッドアプリ
## ハイブリッドアプリとは
アプリには大きく分けて2種類ある
- ネイティブアプリ
   - 端末にインストールして使用するアプリ
- Webアプリ
   - safariやchromeなどブラウザ上で表示するアプリ

ハイブリッドアプリはその2種類の特徴を組み合わせたアプリ

## メリットとデメリット
### メリット
1. マルチプラットフォーム対応可能である。    

iOS,Android共に共通で利用できるコンポーネントであるWebビューを使用するため    
web画面を生成するコードで実装できる。  
Andorid版はJavaで書いてiOSはSwiftで・・・   
ということをしなくても良い

2. デバイスの機能を利用できる  

Webアプリだとカメラやセンサーを使用するのは難しいが  
ハイブリッドアプリだとインストールしたアプリ内でWebビューを表示しているので  
デバイスの機能を簡単に利用することができる。

3. アプリの変更に再インストールが必要なくなる。  

外部サーバからコードを参照することで再インストールしなくてもアプリの修正ができる。

### デメリット
1. ネイティブアプリと比べて処理が遅い  

コンパイル言語ではないのでネイティブアプリと比べると処理が遅くなってしまうため   
動きが激しいゲームのようなアプリ開発には向かない。

## フレームワーク
- Apache Cordova
HTML5やCSS3、JavaScriptなどのWeb系スキルでアプリが開発できるという点や、  
プラグインによってさまざまなネイティブ機能を実装できる拡張性の高さが人気。


## ちょっとやってみた
```
$ npm install -g cordova
$ cordova create workshop com.yanada.workshop Workshop
$ cordova platforms add ios --save
$ npm install -g ios-deploy
```
こんな感じで実行していくと、workshopという名前のアプリができた。  
workshop/platforms に今回はiosを追加した。  
そこからXcodeを開いてこんな感じに

![2018-05-18 10 32 50](https://user-images.githubusercontent.com/28851703/40211681-e94afe70-5a86-11e8-8e8e-1d226f439368.png)

試しにビルドしてみる

<img width="385" alt="2018-05-18 10 36 08" src="https://user-images.githubusercontent.com/28851703/40211768-69317498-5a87-11e8-9cc8-14c9d25598f8.png">

index.htmlを少し変更してビルドすると

<img width="385" alt="2018-05-18 10 39 37" src="https://user-images.githubusercontent.com/28851703/40212073-0e2e95a6-5a89-11e8-90ff-6908b0ab7d2f.png">

HTMLの修正のみでアプリ内のレイアウトが変更できた。  
このファイルを外部サーバから取得するようにすればアプリの再ビルドもいらなくなりそうだ。


## 参考
https://cordova.apache.org/  
https://furien.jp/columns/135/#1-1  
https://qiita.com/hironaito/items/9690c0757dd345cd5917
