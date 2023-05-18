### アプリケーションの起動  
``` $ npm run start:dev ```  

### コントローラー  
アプリケーションに対するリクエストを受信して処理を実行する役割がある  
つまり、コントローラーはルーティングを設定し、そのルーティングごとに適切な処理を実行する  

### コントローラーの作成  
``` $ npx nest g controller todo ```  
作成するとファイル名.controller.tsが生成されるので  
そのファイルを編集してルートを作成していく  
また、**コントローラを作成したら、必ずモジュールにマップしてあげる必要がある。**  
  
### モジュールにマップする  
``` app.module.ts ```にコントローラを追加してあげる  
```
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersController } from './users.controller'; // <= 追加

@Module({
  imports: [],
  controllers: [
    AppController,
    UsersController, // <= 追加
  ],
  providers: [AppService],
})
export class AppModule {}

```

### コントローラの実装  
コントローラの実装に関しては以下のサイトを見ると理解がしやすい  
https://www.keisuke69.net/entry/2022/03/14/121506#Controller%E3%82%92%E5%AE%9F%E8%A3%85%E3%81%97%E3%81%A6%E3%81%BF%E3%82%8B



### サービス  
ビジネスロジックを定義する  
(ビジネスロジックとはネットワークで言うところのアプリケーション層で、数字を2倍にする等の部分を指す)  



### データベース  
NestJSでデータベースに接続、操作する際には、Prismaを利用する  
  
#### prismaのセットアップ  
Prismaのインストール  
``` $ npm i prisma ```  
``` $ npm i @prisma/client ```  
初期ファイルの生成  
``` $ npx prisma init ```  
最後に.envファイルのDATABASE_URLを自分のDBに合うように書き直してあげればセットアップは完了  
  
  
### テーブルの作成  
schema.prismaファイルにテーブルの構成を定義する  
例:  
```
model Task {
  id    Int     @id @default(autoincrement())
  title String  @unique
  due_on  DateTime? 
  is_done Boolean  @default(false)
}
```  
  
### テーブル作成コマンド  
``` $ npx prisma migrate dev ```  
  
### seedを作成する  




## 参考文献  
https://zenn.dev/mikakane/books/nestjs-tutorial/viewer/setup  
