# これは何？
MySQLについての基本的な内容をメモします。  

## データフォーマット
データフォーマットはテキストベースのデータ処理との対比がわかりやすい。  
sedやgrep、awkで扱いやすいよう１行に複数フィールドを持つデータが複数行集まって一つのテキストファイルになるのが一般的。  

<dl><dt>テキストデータベース：</dt>
<dd>レコード（フィールド ,フィールド, フィールド, ...）</dd>
<dd>レコード（フィールド ,フィールド, フィールド, ...）</dd>
<dd>...</dd></dl>

MySQLではこれに呼応する形で。。。  
１行にいくつかのカラムを持つデータの集合をTABLE  
これが複数行集まった２次元の表形式のDATABESE  
となり、MySQLでは複数のDATABASEに跨ったデータ処理ができる。  

<dl><dt>TABLE</dt>
<dd>ROW (COLUMN, COLUMN, COLUMN, ...)</dd>
<dd>ROW (COLUMN, COLUMN, COLUMN, ...)</dd>
<dd>...</dd></dl>

## コマンド形式
MySQLコマンドは;を一区切りとした命令形式で、改行してもコマンド入力は終わらないことが多い。。。  
が、終わることもあるので行末に;を与える癖をつけよう。  
基本は大文字らしいけれど小文字も受け付けるOSもある。  
ctrl+Cで命令キャンセルはできず、MySQLそのものが終了することが多い。  

### HELP: ヘルプ表示
どこまで詳細がわかるかは不明だけれど。。。  
ex) HELP;

### QUIT: 終了
これさえ知っていればシェルに戻れる！  
ex) QUIT;

### SHOW: 情報の表示
DATABASE名やTABLEの構成要素を表示する。（英語なので対象は複数形）  
ex) SHOW DATABASES;  
ex) SHOW TABLES;  
ex) SHOW GRANTS FOR user\_name@localhost;  

### USE: 使用するDATABASEの指定
基本的にコマンドはDATABASEに対する操作なので、まずは対象を明確に。  
ex) USE db\_name;

### SELECT: COLUMNの表示
TABLEに格納されたCOLUMNを選択して表示できる。ワイルドカードは\*。  
また、WHERE区で対象ROWを絞り込むことができる。  
ex) SELECT user, host FROM user;  
ex) SELECT \* FROM table\_name WHERE key\_name = 'value';  
ex) SELECT field\_name FROM table\_name WHERE field\_name REGEXP "regexp";

### CREATE: DATABASEやTABLEの生成
DATABASE, TABLEやUSER（USERもTABLE管理されている）を生成する。  
ex) CREATE USER user\_name@localhost IDENTIFIED BY 'password';  
ex) CREATE DATABASE db\_name;  
ex) CREATE TABLE table\_name(id INT(5) NOT NULL AUTO\_INCREMENT, name VARCHAR(20), PRIMARY KEY(id));  

### DROP: DATABASEやTABLEの削除
DATABASEやTABLEを削除する。  
ex) DROP USER user\_name@localhost;  
ex) DROP DATABASE db\_name;  
ex) DROP TABLE table\_name;

### GRANT: 権限の指定
DATABASEにアクセスできるuserと権限の範囲を指定する。  
ex) GRANT ALL PRIVILEGES ON db\_name.\* TO user\_name@localhost;

### FLUSH: 権限情報の更新
GRANTで書き換えた権限情報を有効化するために更新作業が必要らしい。。。  
ex) FLUSH PRIVILEGES;

### DESCRIBE: COLUMN項目の表示
TABLEを構成するCOLUMNの内容を表示する。（短縮形はDESC）  
ex) DESCRIBE table\_name;

### INSERT: TABLEデータを新規作成する。  
新たにデータを追記する。  
ex) INSERT INTO table\_name (id, name) VALUES (1, 'name');

### UPDATE: TABLEデータの内容を更新する。  
既にあるデータを更新する。  
ex) UPDATE table\_name SET field\_name = REPLACE(field\_name, 'target\_value', 'replace\_value') WHERE field\_name = 'value';
