# Class diagrams

```mermaid
classDiagram
  Animal <|-- Duck
  Animal <|-- Fish
  Animal <|-- Zebra
  Animal : +int age
  Animal : +String gender
  Animal: +isMammal()
  Animal: +mate()
  class Duck {
    +String breakColor
    +swim()
    +quack()
  }
  class Fish {
    -int sizeInFeet
    -canEat()
  }
  class Zebra {
    +bool is_wild
    +run()
  }

```


---


# Syntax

- 上部のコンパートメント
  - クラスの名前が含まれている
  - 太字で中央に表示され、最初の文字は大文字になる
  - また、クラスの性質を説明するオプションの注釈テキストが含まれる場合もある
- 中央のコンパートメント
  - クラスの属性が含まれている
  - 左揃えで、最初の文字は小文字
- 下部のコンパートメント
  - クラスが実行できる操作が含まれる
  - 左揃えで、最初の文字は小文字

```mermaid
classDiagram
  class BankAccount
  BankAccount : +String owner
  BankAccount : +Bigdecimal balance
  BankAccount : +deposit(amount)
  BankAccount : +withdrawl(amount)
```


---


# Define a class


## 2種類のクラス定義方法

- `class Animal` のようなキーワードクラスを使用してクラスを明示的に定義
- `Vehicle<| -Car` のように、2つのクラスの関係とともに定義

```mermaid
classDiagram
  class Animal
  vehicle <|-- Car
```

## 命名規則

- クラス名は、英数字とアンダースコア文字で構成する必要あり


---


# Defining Members of a class


- Mermaidは、括弧 `()` が存在するかどうかに基づいて、属性と関数/メソッドを区別している
  - `()` が付いているものは関数/メソッドとして扱われ、その他は属性として扱われる
- クラスのメンバーを定義する方法は2つ

## コロンの後にメンバー名を使用してクラスのメンバーを関連付け

```
class BankAccount
BankAccount : +String owner
BankAccount : +BigDecimal balance
BankAccount : +deposit(amount)
BankAccount : +withdrawal(amount)
```

## 波括弧を使用してクラスのメンバーを関連付け

```
class BankAccount{
    +String owner
    +BigDecimal balance
    +deposit(amount)
    +withdrawl(amount)
}
```

## Return Type

- メソッドの返り値は、末尾に半角スペース区切りで記述
```
class BankAccount{
    +String owner
    +BigDecimal balance
    +deposit(amount) bool
    +withdrawl(amount) int
}
```

## Generic Types

- `List <int>` などのジェネリック型を使用して、型を `~` (チルダ) で囲むことによって定義できる
```mermaid
classDiagram
class Square~Shape~ {
  int id
  List~int~ position
  setPoints(List~int~ points)
  getPoints() List~int~
}

Square : -List~string~ message
Square : +setMessage(List~string~ message)
Square : +getMessage() List~string~
```

## Visibility

### アクセス修飾子を表す記号

- `+` Public
- `-` Private
- `#` Protected
- `~` Package/Internal
- `*` Abstract
- `$` Static


---


# Defining Relationship

- `relationship` は、クラス図とオブジェクト図に見られる特定のタイプの論理接続をカバーする一般的な用語

```
[classA][Arrow][ClassB]:LabelText
```

Type   | Description
-------| ------------
`<|--` | 継承 (Inheritance)
`o--`  | 集約 (Aggregation) (クラス間の関連で全体と一部という関係性を表現)
`*--`  | コンポジション (Composition) (集約よりも強い集約)
`-->`  | 関連 (Association) (クラス間の関連を表現)
`..>`  | 依存 (Dependency)
`..|>` | 実現 (Realization) (クラス間のインターフェースを表現)
`--`   | 直線リンク (Link) (Solid)
`..`   | 破線Link (Dashed)

```mermaid
classDiagram
classA <|-- classB
classC *-- classD
classE o-- classF
classG <-- classH
classI -- classJ
classK <.. classL
classM <|.. classN
classO .. classP
```

- ラベルを使用して、2つのクラス間の関係の性質を説明することも可能
- 矢印は反対方向にも使用できる
```mermaid
classDiagram
classA --|> classB : 継承(Inheritance)
classC --* classD : コンポジション(Composition)
classE --o classF : 集約(Aggregation)
classG --> classH : 関連(Association)
classI -- classJ : 直線リンク(Link)(Solid)
classK ..> classL : 依存(Dependency)
classM ..|> classN : 実現(Realization)
classO .. classP : 破線Link(Dashed)
```


---


# Labels on Relations

- リレーションにラベルテキストを追加することが可能
```
[classA][Arrow][ClassB]:LabelText
```
```mermaid
classDiagram
classA <|-- classB : implements
classC *-- classD : composition
classE o-- classF : association
```


---


# Cardinality / Multiplicity on relations

- 多重度表記は、関連付けの終わり近くに配置

## カーディナリティのオプション

- `1` Only 1
- `0..1` Zero or One
- `1..*` One or more
- `*` Many
- `n` n {where n>1}
- `0..n` zero to n {where n>1}
- `1..n` one to n {where n>1}

## カーディナリティの定義

- カーディナリティは、指定された矢印の前(オプション)と後(オプション)の引用符でカーディナリティテキストを配置することで簡単に定義できる
```
[classA] "cardinality1" [Arrow] "cardinality2" [ClassB]:LabelText
```
```mermaid
classDiagram
  Customer "1" --> "*" Ticket
  Student "1" --> "1..*" Course
  Galaxy --> "many" Star : Contains
```


---


# Annotations on classes

- クラスのメタデータのような特定のマーカーテキストでクラスに注釈を付けて、その性質を明確に示すことができる
- 注釈は、 `<<` と `>>` で定義
- クラスに注釈を追加する方法は2つ

## 一般的な注釈の例

- `<<Interface>>` To represent an Interface class
- `<<abstract>>` To represent an abstract class
- `<<Service>>` To represent a service class
- `<<enumeration>>` To represent an enum

## クラスが定義された後の別の行に定義する例

```mermaid
classDiagram
class Shape
<<interface>> Shape
```

## クラス定義とともにネストされた内側に定義する例

```mermaid
classDiagram
class Shape {
  <<interface>>
  noOfVertices
  draw()
}
class Color {
  <<enumeration>>
  RED
  BLUE
  GREEN
  WHITE
  BLACK
}
```