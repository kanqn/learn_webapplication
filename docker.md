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
  
  
  
  
## dockerについて

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

#### 仕様書(Dockerfile)をビルドする

```
-t で名前をつける
docker build ./ -t example

または、イメージタグを使ってバージョン名を明記する
docker build . -t hello:1.0
```

#### ビルドしたイメージをコンテナとして実行する

```
docker run example
```
  
  
  
## Dockerfileの基本的な記述

### 環境のベースを何に使うかを指定する FROM

```
FROM ubuntu:latest
```

### 実行したいコマンドを記載する RUN

```
RUN uptget update && uptget install -y vim
```

### コンテナ起動時に実行するコマンドとオプションを変更する CMD

```
CMD ["ls", "-a"]
```

### 操作するディレクトリの絶対パスを指定する WORKDIR

指定したら、それ以降はそのディレクトリを基準にDOckerfileが実行される  

```
WORKDIR /opt
```

### 環境変数の設定を行う ENV

```
ENV DB_USER="user" \
    DB_PASSWORD="password" \
    DB_DATABASE="sample_db"
```

### コンテナに指定したフォルダやファイルをコピーする COPY , ADD

#### COPYとADDの違い

容量が大きいファイルの場合はtarで圧縮した場合→**ADDでコピー**  
それ以外→**COPYでコピー**

```
COPY ./file.conf /etc/conf
ADD ./file.tar /etc/conf
```
