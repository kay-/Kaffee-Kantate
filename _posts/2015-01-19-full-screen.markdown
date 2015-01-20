---
layout: post
title: ウェブサイトのフルスクリーン表示 (CSS / JavaScript)
date: 2015-01-19
published: true
excerpt: 要素のフルスクリーン表示をCSSとJavaScriptそれぞれで実装。
tags: javascript css
cover_image: /2015/
---

要素のフルスクリーン表示をCSSとJavaScriptそれぞれで実装。
元になるHTMLは以下を使用。


	<body>
		<section class="full1"><p>Page1</p></section>
		<section class="full2"><p>Page2</p></section>
		<section class="full3"><p>Page3</p></section>
	</body>



##CSSその1

よく見かける`position:absolute`と`height:100%`の組み合わせ。
複数の要素をフルスクリーン表示させる場合、それぞれpositionの指定が必要になるため使いづらい。


<div data-height="350" data-theme-id="0" data-slug-hash="emWEJJ" data-default-tab="css" data-user="kay8" class='codepen'><pre><code>body {
  margin: 0;
  padding: 0;
}
p {
  text-align: center;
  color: white;
  font-size: 2em;
  margin-top: 0;
}
.full1, .full2, .full3 {
  position: absolute;
  height: 100%;
  width: 100%;
  display: block;
}
.full1 {
  background-color: teal;
  top: 0;

}
.full2 {
  background-color: blue;
  top: 100%;
}
.full3 {
  background-color: black;
  top: 200%;
}</code></pre>
<p>See the Pen <a href='http://codepen.io/kay8/pen/emWEJJ/'>Full Screen: CSS1</a> by Kei (<a href='http://codepen.io/kay8'>@kay8</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
</div><script async src="//assets.codepen.io/assets/embed/ei.js"></script>

##CSSその2

`height: 100vh`を使った方法。vhはviewport heightの略でビューポートに対する割合を指定可能。上から10%の場合は`height: 10vh`。

<div data-height="350" data-theme-id="0" data-slug-hash="JoNyGN" data-default-tab="css" data-user="kay8" class='codepen'><pre><code>		body {
			margin: 0;
			padding: 0;
		}
		p {
			text-align: center;
			color: white;
			font-size: 2em;
			margin-top: 0;
		}
		.full1, .full2, .full3 {
			height: 100vh;
			width: 100%;
			display: block;
		}
		.full1 {
			background-color: teal;

		}
		.full2 {
			background-color: blue;
		}
		.full3 {
			background-color: black;
		}</code></pre>
<p>See the Pen <a href='http://codepen.io/kay8/pen/JoNyGN/'>Full Screen: CSS2</a> by Kei (<a href='http://codepen.io/kay8'>@kay8</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
</div><script async src="//assets.codepen.io/assets/embed/ei.js"></script>

%による指定との大きな違いは

>% の場合は対象となる要素のプロパティが親要素のそれと紐付けられるため、必ずしもビューポートの幅が基準になるとは限りません。(中略)vw, vh にはそのようなプロパティの紐付けがありません。([CSS には vw, vh, vmin, vmax という単位がある ｜ Developers.IO
](http://dev.classmethod.jp/?p=95757))

ただし、現時点(2015/1/19)でAndroid Brower4.4以降にしか対応していないため使用するかどうかはまだ微妙なところ。ちなみに2015/1/5時点ではAndroidユーザの中でJelly Beanの割合が約半分([Platform Versions](http://developer.android.com/about/dashboards/index.html))。


##JavaScript

こちらは`getElementsByTagName`で取得したNodeListの要素へstyle属性を設定するもの。単に要素のリストがほしいだけなので`getElementsByTagName`を使用。([参考: getElementsByTagName()がquerySelectorAll()より高速な理由](http://news.mynavi.jp/articles/2010/10/01/javascript-nodelist-difference/))

<div data-height="310" data-theme-id="0" data-slug-hash="vEmJLR" data-default-tab="js" data-user="kay8" class='codepen'><pre><code>		window.addEventListener(&#x27;load&#x27;, setGreetHeight, false);
		window.addEventListener(&#x27;resize&#x27;, setGreetHeight, false);
		var w = window.innerWidth;

		function setGreetHeight() {
		  var h = window.innerHeight;
		  var sec = document.getElementsByTagName(&#x27;section&#x27;);
		  console.log(sec);
		  for (var i = 0; i &lt; sec.length; i++) {
		  	sec[i].style.height = h + &quot;px&quot;;
		  }
		}</code></pre>
<p>See the Pen <a href='http://codepen.io/kay8/pen/vEmJLR/'>Full Screen: JavaScript</a> by Kei (<a href='http://codepen.io/kay8'>@kay8</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
</div><script async src="//assets.codepen.io/assets/embed/ei.js"></script>

対象となる要素が一つしかない場合は`document.getElementById`を使った方がすっきりすると思います。

##その他
モバイルでランドスケープ表示にした際、viewport外にある要素が表示されないサイトをたまに見かけるので必要に応じて`min-height`の設定を。







