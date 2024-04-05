# 例1 ログインフォームに```1' or 'a' = 'a ```を入力

- フォームにこのようなコードを入れる意図
ログインフォームなので、usersテーブルからデータを取得していると予想。

想像できるSQL
```
SELECT * FROM users where id = [リクエスト内容] :
```

ここに、フォームに入力されたSQLの一部が加わると、次のようなSQLが出来上がる。

```
SELECT * FROM users WHERE id = 1 or a = a;
```

where句は```id = 1``` or ```a = a``` の条件を満たす時DBからデータを取得してくることになる。

よって、```a = a```と常にtrueとなるため、このSQLはusersテーブルから全てのデータをとってくることになる。

# 例2　フォームに```' union select @@hostname,database() #```を入力

こちらに関しては、SELECTしてそうなフォームに対して行う

想像できるSQL
```
SELECT * FROM products WHERE name = ;
```

ここに、フォームに入力されたSQLの一部が加わると、次のようなSQLが出来上がる。

```
SELECT * FROM products WHERE name = '' UNION SELECT @@hostname, database() #
```

このようにすると、前半のSELECT句がどんな状態であれ、UNIONしているため、無視できる。
後半は、ちゃんと取得され、データベースホスト名とデータベース名が取得できる。

