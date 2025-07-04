# todoApp_terasoluna_Sample

### 注意

チュートリアルはコピペだけして、内容は詳しく見ていません。 詳しく学びたい場合はチュートリアルの記事を読んでください。  
純粋にチュートリアルを PostgreSQL に接続できるようにしたものです。検索機能やスタイルの変更等の機能追加は行っていません。

### 参考資料

- チュートリアルは以下サイトの Thymeleaf 編（MyBatis3 用）を使用  
  https://terasolunaorg.github.io/guideline/current/ja/Tutorial/TutorialTodoThymeleaf.html
- 同ページの「11.2.6.1. O/R Mapper に依存したブランクプロジェクトの作成」を参照  
  https://terasolunaorg.github.io/guideline/current/ja/Tutorial/TutorialTodoThymeleaf.html#tutorialcreateormapperblankproject-thymeleaf
- PostgreSQL の DB 接続設定については以下サイトを参照（オプション項目と工番 8 はスキップ）  
  https://qiita.com/5zm/items/03915a7232fcbbd5768a

## ローカルで動作させるまでの手順

### 1. リポジトリのクローン

任意のフォルダでターミナルを開き、以下のコマンドを実行。

```bash
git clone https://github.com/Tosaka11/todoApp_terasoluna
```

### 2. PostgreSQL のセットアップ

1. **PostgreSQL のインストール・データベースの作成**  
   pgAdmin でローカルサーバーにデータベースを作成。  
   参考：[【PostgreSQL】 「pgAdmin 4」データベースとテーブルの操作](https://www.kemmy-it.com/2024/08/15/pgadmin_1/)

2. **テーブルの作成**  
    `todo`テーブルを作成する SQL スクリプトを実行。

   ```sql
   CREATE TABLE todo (
    todo_id VARCHAR(36) PRIMARY KEY,
    todo_title VARCHAR(30) NOT NULL,
    finished BOOLEAN NOT NULL,
    created_at TIMESTAMP NOT NULL
   );
   ```

### 3. DB 情報の反映

\src\main\resources\META-INF\spring\todo-infra.properties のかっこの箇所を自身で設定した DB 情報に変更

```ts
// ポスグレの情報をここに記載
database=POSTGRESQL
database.url=jdbc:postgresql://127.0.0.1:5432/「DB名」
database.username=「ユーザ名」
database.password=「パスワード」
database.driverClassName=org.postgresql.Driver
```

### 4. アプリの起動

クローンしたプロジェクトに対して、プロジェクトを右クリックして出てくる「Maven ＞プロジェクトの更新」と Maven ビルドを行う。  
アプリの起動については、チュートリアルのサイトに記載されている方法と同じため割愛。  
\*PostgreSQL の DB を立ち上げた状態で行ってください。

### 5. 画面で確認

http://localhost:8080/todo/todo/list  

---
### Ex1. （追記）フロントエンドを修正  
チュートリアルからフロント周りを変更した資材をBranch「working」へコミットしました  
クローン後にブランチを上記に変えて参考にしてください  

---
### Ex2. （追記）アプリが起動しないときの参考  
①SQLの設定を見直す（\src\main\resources\META-INF\spring\todo-infra.properties ）  
②プロジェクトのクリーンを実施する  
③Maven Installを実施する  
④プロジェクトを起動する  
  
※「Maven ＞プロジェクトの更新」をすると資材が変に更新されてアノテーションが正常に読み取れないことがある

