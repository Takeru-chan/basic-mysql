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

### HELP:ヘルプ表示
どこまで詳細がわかるかは不明だけれど。。。  
ex) HELP;

### QUIT:終了
これさえ知っていればシェルに戻れる！  
ex) QUIT;

### SHOW:情報の表示
DATABASE名やTABLEの構成要素を表示する。（英語なので対象は複数形）  
ex) SHOW DATABASES;  
ex) SHOW TABLES;
ex) SHOW GRANTS FOR user\_name@localhost;  

### USE:使用するDATABASEの指定
基本的にコマンドはDATABASEに対する操作なので、まずは対象を明確に。  
ex) USE db\_name;

### SELECT: COLUMNの表示
TABLEに格納されたCOLUMNを選択して表示できる。ワイルドカードは\*。  
また、WHERE区で対象ROWを絞り込むことができる。  
ex) SELECT user, host FROM user;  
ex) SELECT \* FROM table\_name WHERE key\_name = 'value';  
ex) SELECT field\_name FROM table\_name WHERE field\_name REGEXP "regexp";
