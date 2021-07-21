# Sequence diagrams


```mermaid
sequenceDiagram
  Alice->>John: Hello John, how are you?
  John-->>Alice: Great!
  Alice-)John: See you later!
```


---


## Syntax


### Participants (アクター)

```mermaid
sequenceDiagram
  participant John
  participant Alice
  Alice->>John: Hello John, how are you?
  John-->>Alice: Great!
```

### Aliases

```mermaid
sequenceDiagram
  participant A as Alice
  participant J as John
  A->>J: Hello John, how are you?
  J->>A: Great!
```


---


## Messages

- メッセージは、実線または点線で2つ表示できる

```
[Actor][Arrow][Actor]:Message text
```

### 現在サポートされている矢印の6種類

Type   | Description
------ | ------------------------------------------------
`->`   | Solid line without arrow
`-->`  | Dotted line without arrow
`->>`  | Solid line with arrowhead
`-->>` | Dotted line with arrowhead
`-x`   | Solid line with a cross at the end
`--x`  | Dotted line with a cross at the end.
`-)`   | Solid line with an open arrow at the end (async)
`--)`  | Dotted line with a open arrow at the end (async)


---


## Activations

- アクターをアクティブ化および非アクティブ化することができる
- （非）アクティブ化は、専用の宣言にすることができる

```mermaid
sequenceDiagram
  Alice->>John: Hello John, how are you?
  active John
  John-->>Alice: Great!
  deactivate John
```

- メッセージ矢印に`+`/`-`サフィックスを追加することによるショートカット表記も可能

```mermaid
sequenceDiagram
  Alice->>+John: Hello John, how are you?
  John-->>-Alice: Great!
```

- 同じアクターに対してアクティベーションをスタックできる

```mermaid
sequenceDiagram
  Alice->>+John: Hello John, how are you?
  Alice->>+John: John, can you hear me?
  John-->>-Alice: Hi Alice, I can hear you!
  John-->>-Alice: I feel great!
```


---


## Notes

- シーケンス図にメモを追加することができる
- `Note [ right of | left of | over ] [Actor]`

```mermaid
sequenceDiagram
  participant John
  Note right of John: Text in note
```

- 2人のアクターにまたがるメモを作成することもできる

```mermaid
sequenceDiagram
  Alice->John: Hello John, how are you?
  Note over Alice,John: A typical interaction
```


---


## Loops

- シーケンス図でループを表現することができる

```
loop Loop text
... statements ...
end
```

```mermaid
sequenceDiagram
  Alice->John: Hello John, how are you?
  loop Every minute
    John-->Alice: Great!
  end
```

