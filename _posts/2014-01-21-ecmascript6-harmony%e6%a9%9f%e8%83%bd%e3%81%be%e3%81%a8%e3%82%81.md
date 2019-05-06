---
id: 121
title: ECMAScript6 Harmony機能まとめ
date: 2014-01-21T08:00:55+00:00
author: chikathreesix
layout: post
guid: http://chikathreesix-blog.herokuapp.com/?p=335
permalink: /archives/121
categories:
  - JavaScript
tags:
  - ECMAScript6
  - Harmony
  - JavaScript
---
そろそろHarmonyの新仕様をちゃんと理解しておかねばと思ったので、調べついでにまとめました。

現在どのブラウザでどのくらい使えるのかはこちらから確認出来ます。

<a href="http://kangax.github.io/es5-compat-table/es6/" target="_blank">ECMAScript 6 compatibility table</a>

ここに乗っていないものもまだまだありますが、ひとまず気になったもの、主要な物を列挙しました。

<!--more-->

## Let

letキーワードを使う事により、ブロックスコープが使える様になります。

IE11, Firefox, Chromeと対応している環境も多いですね。

for文中で気にせずガンガン変数が定義できちゃうわけです。

<pre class="lang:js decode:true" title="let">var i = 100;
for (let i = 0; i &lt; 3; i++){
  //Do something
}
console.log(i); //100</pre>

&nbsp;

## Const

constキーワードを使う事により、定数を定義することができます。

今まで変数名を大文字にして定数である事を明示していたりしましたが、代入不可な定数を定義する事が可能になります。

さらにconstはブロックスコープになります。

対応環境が最も多い仕様ですね。

<pre class="lang:js decode:true" title="const">const VALUE = 100;
VALUE = 200; //Error</pre>

&nbsp;

## Default Function parameters

今までありそうで無かった機能！　関数のデフォルト引数。

今までこいつが無いことで、いちいち関数の頭でa = a || 1とかやって初期化しなきゃいけなかった訳です。

<pre class="lang:js decode:true" title="Default function parameters">function add(a, b = 1){
  return a + b;
}
console.log(add(2)); //3</pre>

&nbsp;

## Rest Parameters

これまで可変長の引数をとる関数を定義することは多々ありましたが、argumentsを使って引数を判別していました。

rest parametersを使えば、残りの引数を一つの配列にまとめることが出来ます。

Rubyだと*（アスタリスク）を付けることで実現出来るアレです。

<pre class="lang:default decode:true" title="Rest Parameters">function sum(base, ...rest){
  for(let i = 0; i &lt; rest.length; i++){
    base += rest[i];
  }
  return base;
}
console.log(sum(1, 2, 3, 4, 5)); //15</pre>

&nbsp;

## Class

待ってました、クラス！

やはりなんだかんだ言って、JavaScriptの大きな問題点はクラスが定義できないことだと思っています。

クラス実装が山ほどありすぎるが故に、コーディングパターンが人それぞれ違うことが、JavaScriptコードの保守性・可読性を著しく下げていると考えます。

しかし実際の実装がまだTraceurコンパイラに留まり、ブラウザなどが対応していないことから、まだまだ普及は遠い道のりの様に感じます。。

<pre class="lang:js decode:true" title="Class">class Instrument{
  constructor(name) {
    this.name = name;
  }
  play() {
    //Do something
  }
}

//Extend
class Guitar extends Instrument{
  constructor(name, strings) {
    super(name);
    this.strings = strings;
  }
}</pre>

&nbsp;

## Generators

generator functionはコルーチンを生成する仕組みです。

コルーチン自体僕には馴染みがないのですが、関数を実行して、途中で止まって、そこから再度実行できるという仕組みです。

JavaScriptの遅延処理によるcallback地獄を解決する手段になりそうです。

<pre class="lang:js decode:true" title="Generators">function* hello(){
  console.log(1);
  yield "Hello";
  console.log(2);
  yield "My name is";
  console.log(3);
  yield "chikathreesix";
}

var func = hello();
console.log(func.next().value);
console.log(func.next().value);
console.log(func.next().value);</pre>

上記の例で、consoleは以下の様になります。

<pre class="lang:default decode:true" title="Output">1
Hello
2
My name is
3
chikathreesix</pre>

&nbsp;

個人的には早くClassが使いたいです。

Generatorも使いこなすと面白そうですね。