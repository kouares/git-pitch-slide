### Playframework scalaでサービスを開発して辛かったこと

4月からPlayframeworkのキャッチアップを初めて
6月にリリースするまでに辛いと感じたことなどなど・・・

---
### scala

* JVM言語
* 関数型 + オブジェクト指向
* 全てがオブジェクト
* 基本的にnull安全
* javaよりも書きやすい

---
### Playframework

* java, scalaで書けるWebアプリケーションフレームワーク
  今日はscalaの方
* 基本的に非同期のみ
* SSRエンジン twirl
* 最新は2.6.1

---
### 辛かったことリスト

* Future 非同期
* Controllerのエンドポイントが返す戻り値がFuture<play.api.mvc.Resluts>型
* イミュータブルな変数
* null安全
* セッション
* slick（DBアクセス）

---
### Future 非同期

* Playframework内での処理は基本的に非同期のみ
* 非同期を表す型
  * `Future[T]` 未来に型パラメータ`T`のオブジェクトが生成される文脈を持つ型

---
### Controllerのエンドポイントが返す戻り値がFuture<play.api.mvc.Resluts>型
* Controllerの戻り値が非同期を期待している
* 非同期を避けることができない

---
### イミュータブルな変数
* イミュータブルな実装を推奨
* ミュータブルな変数宣言は静的解析ツールでコンパイル時に警告される
  * [wartremover](https://github.com/wartremover/wartremover)
* コレクションもデフォルトでイミュータブル

---
### null安全
* nullを明示的に記述しない（これも警告される）
* null安全を表す型
  * `Option[T]` `T`型のオブジェクトがあるかないか分からない状態を表す型

---
### セッション
* サーバー間通信なので当然`Future[T]`
  * ほしい値がセッションに存在するか分からないので、`Future[Option[T]]`で値が取得される

---
### slick（DBアクセス）
* Dapper, ActiveRecord, Doma とかのscala版
* Functional Relational Mapping
* サーバー間通信なので・・・以下略
* SQLを関数で記述する
  * これが地獄への入り口

