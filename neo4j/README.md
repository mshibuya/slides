Neo4j 初歩の初歩
===



# Neo4jとは

- グラフデータベース
- Neo Technologies, Inc.
- 2000年頃から開発が始まった
- オープンソース
- スキーマレス
- ACID保証
- 構成
	- アプリケーションに埋め込み
	- クライアント／サーバ



# グラフ？


円グラフ・棒グラフ・折れ線グラフ…


ではなく


グラフ理論

- 頂点(節点, vertex)と辺(枝, edge)
- 有向・無向グラフ



## グラフデータベースの種類
|        |グラフ       |リレーショナル|
|--------|--------------------|----|
|オンライン|Graph Database      |OLTP|
|オフライン|Graph Compute Engine|OLAP|




# Neo4jのグラフ

Labeled Property Graph

ノード(Node)

- ラベルを付けられる
- プロパティ(key-value)

関係(Relationship)

- 方向あり
- プロパティ(key-value)



# 利点
## パフォーマンス

ノードのつながったデータを近くに配置できる


例: 100万ノードのSocial Graph探索

|深さ|RDB(s)|Neo4j(s)|レコード数||----|-----:|-------:|-------:||2   | 0.016|    0.01|  ~2,500||3   |30.267|   0.168|~110,000||4   |1543.505| 1.359|~600,000||5   |終了せず|2.132|~800,000|<small>「Graph Databases 2nd Edition」より</small>
   


## 柔軟性

ビジネスドメインの構造を直接表現できる


	
## アジリティ

スキーマレス



# API

## embedded

```
// データベースを開く
graphDb = new GraphDatabaseFactory().newEmbeddedDatabase( DB_PATH );
// トランザクション開始
Transaction tx = graphDb.beginTx();
// ノード作成
firstNode.setProperty( "name", "foo" );
secondNode.setProperty( "name", "bar" );
// リレーションシップ作成
relationship = 
firstNode.createRelationshipTo( secondNode, RelTypes.KNOWS );
// リレーションシップもPropertyを持てる
relationship.setProperty( "message", "hoge" );
tx.success();
```


## REST

Cypher Query LanguageというSQLっぽい？言語を利用 

JSONをPOSTすると

```
{"statements" : [ {
  "statement" : "CREATE (n) RETURN id(n)"
} ]}
```

JSONで返ってくる

```
{"results" : [ {
    "columns" : [ "id(n)" ],
    "data" : [ {
      "row" : [ 18 ]
    } ]
  } ],
  "errors" : [ ]}
```



# Cypher

## CREATE

```
CREATE (n) RETURN n
```

## MATCH&RETURN

ノードで絞り込み

```
MATCH (n) RETURN n
```

ラベルの指定

```
MATCH (n:Person) RETURN n
```


リレーションシップの指定

```
MATCH (n)-->(o) RETURN n, o
```
```
MATCH (n)<--(o) RETURN n, o
```
```
MATCH (n)-->(o)<--(p) RETURN n, o, p
```
```
MATCH (n)--(o) RETURN n, o
```
```
MATCH (n)-[r]->(o) RETURN n, o, r
```
```
MATCH (n)-[r:FRIEND]-(o) RETURN n, o, r
```
```
MATCH (n)-[*2]-(o) RETURN n, o
```

プロパティへのクエリ

```
MATCH (n {name: 'foo'})-[r]->(o) RETURN n, o, r
```
```
MATCH (n)-[{kind: 'bar'}]->(o) RETURN n, o
```


## インデックスの利用
```
CREATE INDEX ON :Person(name)
```
```
MATCH (person:Person { name: 'Andres' }) RETURN person
```

## WHERE
```
MATCH (person:Person) WHERE person.name = 'Andres' RETURN person
```

 



## 製品ラインナップ

Neo4j Community Edition

- GPL

Neo4j Enterprise Edition

- 有料
- オープンソースプロジェクト向けにAGPLにて提供あり



# まとめ
## グラフデータモデルが面白い
何か実用的なアプリを作ってみたい




# 参考資料
- The Neo4j Manual
	- http://neo4j.com/docs/stable/
- Graph Databases 2nd Edition(O'reilly)
	- http://neo4j.com/books/graph-databases/
	- 無料で読めます（要ユーザー登録）
	- 日本語版も出てますね
		- http://www.oreilly.co.jp/books/9784873117140/
- http://www.creationline.com/neo4j/
