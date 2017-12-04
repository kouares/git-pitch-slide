# Scalaを書く時に気をつけてること

4月からScalaを使い始めて、気をつけてることをつらつらと書いてみる

---
## 関数型

- 副作用を持った関数は書かない
  - 書く場合はわかりやすくかつ、副作用を持つ関数がプロジェクト内に散らばることのない設計にする
  - 基本的に副作用は悪だが、ファイルアップロード等のどうにもならない場合は `Unit` 型を返して、この関数は副作用があるとわかりやすくする

- 式
  - scalaにおいて、if , for などは式であり値を返せることを忘れない

---
## Futureの入れ子, Optionの入れ子

- flattenで平坦化できる
  - `Future[Future[Future[T]]]` は `Future[T]` になる
  - `Option[Option[Option[T]]]` は `Option[T]` になる

---
## ボイラープレートコード 

- `case class` を用いる
  - コンストラクタを別に用意する時は、コンパニオンオブジェクトを作成してapplyをオーバーロードする

---
## javaで書かれたAPIの呼び出し

- `Option(map.get("hoge"))` のように書くことで、`null` は `None` に変換される

---
## 比較

- 同値比較は `==` （String型も）

---
## 式展開

- 文字列中での式展開
before
`Logger.debug("No.%d is %s".format(i+1, user.name))`
after
`Logger.debug(s"No.${i + 1} is ${user.name}")`
