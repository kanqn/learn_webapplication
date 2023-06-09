## Reactについてのメモ

### useState()で配列を保持する  

```
//配列を保持するための配列を作成する
const [tasklist , settasklist] = useState([]);

//文字入力
const [inputText, setinputText] = useState("");

//...はスプレッド構文でひとつ前の状態を意味する

settasklist([
...tasklist,
  {
  text: inputText
  }
]);
```

### map関数を使う  
```

//                   ↓{}ではなく()なのに注意！
tasklist.map(task => (
     //この中にdivで囲んだhtmlフォームを書くとdivで囲まれたまとまりごと更新できる(todolistのtodoを更新するのに使える)
      
   
      //task.textのtextはsetTaskListを呼び出した際のtext: inputTextからきている
      <span>{task.text}</span>
))

```

### filter関数でリスト除外する
filterは条件式がfalseであればリストから除外し、trueであればリストに残される
```
//idと比較して!==であれば(1 == 1はtrueだが、filter関数はfalseを除外するため!==とする)
//リストから除外するコード

const handleDelete = (id) => {
  setTaskList(taskList.filter((task) => task.id !== id));
  }
```

### fetchについて  
主にAPIを取得する際に使用するもので、  
fetch(取得したいURL,{method: メソッド指定(基本的にはGET) })  
また、.thenを使用してレスポンスを取得する。  
#### 使い方  
  
<details>
<summary>コードを表示する</summary>
  
```
import React, {useState, useEffect} from 'react'

const Fetch = () => {

    const [posts, setPosts] = useState([])

    useEffect(() => {
        fetch('https://jsonplaceholder.typicode.com/posts', {method: 'GET'})
        .then(res => res.json())
        .then(data => {
            setPosts(data)
        })
    },[])

    return (
        <div>
            <ul>
                {
                    posts.map(post => 
                    <li key={post.id}>{post.title}</li>
                    )
                }
            </ul>

        </div>
    )
}

export default Fetch;
```
</details>  

### Promiseについて  
Promiseを使うと何かの処理を施して、その結果が戻ってくることが約束される  
また、Promiseは**非同期通信を行うことも可能**  

  
#### 使い方  
<details>
<summary>コードを表示する</summary>
  
```
//結果は成功(Resolve)もしくは失敗(Reject)のどちらかの方法で帰って来ます。

const iceCreams = ["strawberry", "chocolate", "vanilla"];
const iceCreamType = "lemon";

getIceCream = (iceCreamType) => {
  return new Promise((resolve, reject) => {
    if(iceCreams.indexOf(iceCreamType) > -1){
      resolve(iceCreamType);
    } else {
      reject("There is no ice cream");
    }

  };
}

```
</details>  

### useState  
stateを管理するためのReactフック  

#### 関数コンポーネントでの定義の仕方
``` const [状態変数, 状態を変更するための関数] = useState(状態の初期値); ```


### useEffect  
useEffectは**毎回のレンダリング後**に呼ばれる  
つまり、useEffectは**副作用を実行、制御するためにuseEffectを利用する**  

#### 主な書き方  
```
const [count, setCount] = useState(0);

  useEffect(() => {
    document.title =`${count}回クリックされました`
  })
```  
**※第2引数を省略すると、コンポーネントがレンダリングされるたびに副作用関数が実行されることから、  
　無限ループの温床になりやすいので注意する必要があります。  
　実際には、第2引数を省略するケースはほとんどありません。**  

#### 初回レンダリング時のみ副作用関数を実行する場合  
第2引数に空の依存配列[]を指定する。  
以下はクリックしてもクリック数はインクリメントされない  
例:  
```
useEffect(() => {
    document.title =`${count}回クリックされました`
    console.log(`再レンダーされました`)
  },[])
```  

