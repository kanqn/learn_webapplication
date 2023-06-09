### 余計な余白をなくす(cssのおまじないみたいなもの)  
```
* {
  margin: 0;
  padding: 0;
}

```

### インライン要素とブロック要素の違い  
インライン要素は、主に文章の一部を装飾したり、特定の部分に対してスタイルを適用するために使用されます。  
ざっくり説明すると、行の中の一部のまとまり  
**なお、aタグ等のインライン要素にはmarginをあてることができないことに注意  
marginを当てたい場合は、display: inline-block;をあててあげること  
marginは上　左右　下　の順で引数をとっている  
例: margin: 30px 0 50px;

<br />
ブロック要素はブロックレベル要素とも呼ばれ、ページの構造やレイアウトを定義するために使用されるHTMLの要素です。  
ざっくり説明すると、行全体のまとまりを作るのがブロック要素  
また、***初期状態だと縦並びになる  
<br />  

#### relativeとabsolute  
・position:で使われる  
・absoluteは絶対値もしくは、親要素(relative)を基準にして位置を決める 

#### HTMLブロックを横並びにする display: flex;  
なお、display: flex;は親要素に対して追加すること  
<br />

#### テキトーな文字列を作りたい lorem文字数 tab保管

#### liタグの黒ポチを消す list-style: none;
<br />

#### はみ出た部分を隠す overflow: hidden;

#### 文字の折り返し地点を設定する  
max-width: ;を使うことで、表示する枠の大きさを決めてあげることで設定できる  

#### ブラウザを大きくしたり小さくしたりしても画像の大きさを一定に保つ object-fit:  
width heightを設定した状態で、object-fit: cover;  

#### 少し透明にする opacity: 0.8;

#### サイト全体に若干色をつける mix-blend-mode: 色を設定したdivクラス;  
なお、mix-blend-mode: screen;で良い感じにブレンディングしてくれる  

#### 縦方向に対して中央に寄せる align-items: center;  
#### 横並びの位置を中央に揃える justfy-content: center;  
center , space-between(良い感じに隙間を開ける)など指定できる  
なお、これらは**display: flex;が適用されていないと反映されない

space-betweenは**widthを指定しないと反映されない  
<br />

#### text-alignプロパティ: 文字や画像に対して、水平方向の揃え方を指定するプロパティ  
<br />

#### 右側に余白を作る margin-right: ~px; 
<br />

#### 前後左右に余白を作る padding: 上下(0) 左右(2rem);  
<br />

#### 画像の比率をきれいにする object-fit: cover;

#### マウスポインターが要素の上にいる時のマウスカーソルの種類を設定　cursor: 

#### ボタンの角を丸める border-radius: ~px;

#### ブロック要素を横並びにする  display: inline-block;
<br />  
  
### positionプロパティ    
#### position: sticky;  
stickyを設定された要素は、通常の位置に配置され、その要素の位置がウインドウ全体を基準として、  
指定位置の条件を満たすとフロートされる
<br />

#### 要素の重ね順を指定する z-index: 1; //1が一番上に来る  
<br />

#### divの縦の大きさを変更する　transform: translateY(-50%); //この場合は伸びる  
#### divの大きさを左に小さくする left: -10%;
#### divを丸くするborder-radius: 50%; 
<br />

#### div内にクロスするような4つの3角形を作るテク  
divでクラスを指定してdivの枠線の縦横をわざと太くしすぎると三角形になる  

```
.overlay {
  width: 0;
  height: 0;
  border-top: 520px solid red;
  border-right: 520px solid purple;
  border-bottom: 520px solid #fff;
  border-left: 520px solid yellow;
}
```

<br />

#### divタグに画像を挿入する  
background: url(ローカルファイルの画像);  
また、画像がうまく表示されないときは
background-repeat: no-repeat;にする。  


#### 位置を180°回転させる　transform: rotate(-180deg);
<br />

#### aタグのアンダーラインを非表示　text-decoration: none;  
<br />

・インライン要素だとtranslateがあたらない可能性があるため  
display: block;にする必要がある  

  
#### ホバー(カーソルが要素に触れた)したときに色を変える  
なお、うまくtransitionがかからない時は、position: absolute;を指定してあげる必要がある。  
```
.nav-links ul a {
 font-weight: 600;
 color: #fff;
 text-decoration: none;
 //ホバー時やクリック時の動きをを調整できるプロパティがtransitionプロパティ
 //以下は色が変わる時間を指定している
 transition: 0.3s;
 
 }
 
 .nav-links ul a:hover {
  color: 触れたときの色を指定する;
 }
```
<br /> 

