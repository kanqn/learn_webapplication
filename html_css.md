### インライン要素とブロック要素の違い  
インライン要素は、主に文章の一部を装飾したり、特定の部分に対してスタイルを適用するために使用されます。  
ざっくり説明すると、行の中の一部のまとまり  
  
  
ブロック要素はブロックレベル要素とも呼ばれ、ページの構造やレイアウトを定義するために使用されるHTMLの要素です。  
ざっくり説明すると、行全体のまとまりを作るのがブロック要素  
また、***初期状態だと縦並びになる  
  
  
  
  
#### liタグの黒ポチを消す list-style: none;
  
  
#### HTMLブロックを横並びにする display: flex;  
なお、display: flex;は親要素に対して追加すること  

  
#### 縦方向に対して中央に寄せる align-items: ;  
  
  
#### 横並びの位置を揃える justfy-content: ;  

#### text-alignプロパティ: 文字や画像に対して、水平方向の揃え方を指定するプロパティ  
#### 右側に余白を作る margin-right: ~px; 
#### 前後左右に余白を作る padding: 上下(0) 左右(2rem);  
  
#### ブロック要素を横並びにする  display: inline-block;
  

#### divの縦の大きさを変更する　transform: translateY(-50%); //この場合は伸びる  
#### divの大きさを左に小さくする left: -10%;
#### divを丸くするborder-radius: 50%; 

#### aタグのアンダーラインを非表示　text-decoration: none;  

#### ホバー(カーソルが要素に触れた)したときに色を変える  
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

#### relativeとabsolute  
・position:によく使われる  
・absoluteは絶対値つまりは、親要素(relative)を基準にして位置を決める  

