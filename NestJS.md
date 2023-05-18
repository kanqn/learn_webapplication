### アプリケーションの起動  
``` $ npm run start:dev ```  

### コントローラー  
アプリケーションに対するリクエストを受信して処理を実行する役割がある  
つまり、コントローラーはルーティングを設定し、そのルーティングごとに適切な処理を実行する  

### コントローラーの作成  
``` $ npx nest g controller todo ```  
作成するとファイル名.controller.tsが生成されるので  
そのファイルを編集してルートを作成していく  

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



## 参考文献  
https://zenn.dev/mikakane/books/nestjs-tutorial/viewer/setup  
