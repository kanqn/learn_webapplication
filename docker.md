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

もしくは--nameはコンテナの名前をtest-containerにするコマンドで、testは基となるDockerイメージの名前
docker run -d -p 8080:80 --name test-container test
```





## Dockerの基本コマンド

### コンテナ一覧を表示する

```
$ docker ps

停止中含めたコンテナを表示する
$ docker ps -a
```

### イメージ一覧を表示する

```
$ docker images
```

### コンテナ停止

```
docker stop <コンテナIDもしくはNAME>

停止したことは、docker psで確認すること
```

### コンテナ起動

```
$ docker start <コンテナIDもしくはNAME>
```

### イメージを取得する

```
$ docker pull <Docker Hubにあるイメージ名>

例:
$ docker pull lukaszlach/merry-christmas
```

### コンテナ内でコマンド実行

```
$ docker exec <コンテナ名> ls -l /usr
```

### イメージの削除

```
docker rmi <REPOSITORY:TAGまたはIMAGE ID>
```

### コンテナの削除

```
コンテナ停止を確認した後に以下コマンド

docker rm <CONTAINER IDまたはNAME>
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

## Docker Composeとymlファイルについて

### Docker Composeとは
  
**複数のコンテナで構成されるアプリケーションについて、Dockerイメージのビルドや各コンテナの起動・停止などをより簡単に行えるようにするツール**  

### DockerComposeでコンテナを起動するまでの流れ

1. Dockerfileの作成　(これをdocker-compose.ymlから参照する)
2. docker-compose.ymlの作成　(Docker Composeの設定ファイル)
3. docker-composeコマンドでコンテナ起動

### docker-compose.ymlファイルの書き方

```
例:
services: 
  db:
    image: mysql:5.7 
    volumes: 
      - db_data:/var/lib/mysql 
    restart: always
    environment: 
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: your_database
      MYSQL_USER: user_name
      MYSQL_PASSWORD: user_password

  web:
    build: ./rails_project 
    command: bundle exec rails s -p 3000 -b '0.0.0.0' 
    volumes: 
      - .:/myapp
    ports: 
      - "3000:3000"
    depends_on: 
      - db
      
volumes: 
    db_data:
```
