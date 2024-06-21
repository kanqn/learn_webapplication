### dockerについて

どんなPCにするか(セットアップの手順書)の仕様書を書いて、それを新しいイメージとして作る  
これには2種類の方法がある  
・コンテナを作って色々とセットアップした後、そのコンテナを新しいイメージとして保存する方法  
・仕様書（＝セットアップ手順書）を新たに書き上げ、それに基づき構築する方法

#### 仕様書（＝セットアップ手順書）を新たに書き上げ、それに基づき構築する手順

以下のような**セットアップ手順書のことをDockerfileと呼ぶ**

```
ubuntuを使用して、flaskをインストールするまで
例:
FROM ubuntu:latest

RUN apt-get update
RUN apt-get install python3 python3-pip -y

RUN pip3 install flask
```

### 動作確認

```
docker run hello-world

Hello from Docker!と表示されればOK
```

### 現在PCにあるイメージを確認する

```
docker images
```

### Ubuntuのイメージを用意する

```
docker pull ubuntu:latest
```
