---
layout: "../../layouts/BlogPost.astro"
title: Picostyle v1.0.0
pubDate: "2018-03-03"
description: "Picostyle の v1.0.0 をリリースした。使い方に変更はなく、 Preact でも利用できるようになった。"
heroImage: "/picostyle-logo.png"
---


[Picostyle](https://github.com/morishitter/picostyle) という CSS in JS のライブラリを作っている。

CSS という言語仕様がとにかく機能が貧弱でメンテナンス性に乏しいので、JavaScript でスタイルの定義もしてしまおうというアプローチが CSS in JS である。Picostyle は名前の通り、ミニマムな CSS in JS の実装で、Gzip 時で450バイトほどしかない。おそらく最も小さい CSS in JS の実装だと思う。

そして今日、Picostyle の v1.0.0 をリリースした。使い方に変更はなく、 [Preact](https://preactjs.com/) という JavaScript のライブラリでも利用できるようになった。

Preact で Picostyle を利用した例:

```js
import picostyle from "picostyle"
import { h, render } from "preact"

const ps = picostyle(h)

const Text = ps("a")({
  fontSize: "64px",
  cursor: "pointer",
  color: "#fff",
  padding: "0.4em",
})

const Wrapper = ps("div")({
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
  width: "100vw",
  height: "100vh",
  backgroundColor: "f07",
})

render((
  <Wrapper>
    <Text href="https://github.com/morishitter/picostyle">
      Picostyle meets Preact
    </Text>
  </Wrapper>
), document.body)
```

Picostyle のような CSS in JS ライブラリは CSS の宣言を受け取り、その CSS を style 要素や CSS ファイルとして書き出し、それに対応した新しい Virtual DOM を返す関数である。これまでは [Hyperapp](https://github.com/hyperapp/hyperapp) という JavaScript のライブラリにのみ対応していたが、Hyperapp の Virtual DOM に与える引数の型が Preact のそれと同じになったので、Picostyle ではほとんど変更なしに Preact に対応できるようになった。

React の `React.createElement()` も Preact や Hyperapp と同じ構造の Virtual DOM になればいいのにと思う。