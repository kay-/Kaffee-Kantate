---
layout: post
title: CSSアニメーションによるSVG pathの操作
date: 2015-01-23
published: true
excerpt: stroke-dasharray/stroke-dashoffsetとfill-opacityによるアニメーション。
tags: css
cover_image: /2015/
---

stroke-dasharray/stroke-dashoffsetを使ってSVGのpathをanimateさせようと思った時の話。SVGアニメーションの基本については下記が参考になりました。

- [SVGのアニメーションで線を引く方法まとめ（IEへの対応も 2.IDEA](http://2ndidea.com/svg/svg-path-drawing-animation-even-ie/)

- [SVGのアニメーション mkasumi.com](http://mkasumi.com/entry-653.html)

typographyのアニメーションといえば[Béatrice Créations](http://carlphilippebrenner.com/portfolio/beatricecreations)等が有名ですが、画像背景の上でアニメーションさせたいと思い

- defaultではfill:"none"
- keyframesにてfill:"none"からfill:"#000"に変化
- animation-fill-mode:forwardsを設定

を試しました。

<p data-height="250" data-theme-id="0" data-slug-hash="gbRgKx" data-default-tab="result" data-user="kay8" class='codepen'>See the Pen <a href='http://codepen.io/kay8/pen/gbRgKx/'>Animate SVG Path: not working in FF</a> by Kei (<a href='http://codepen.io/kay8'>@kay8</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

WebKitではfill="#000"になるもののFireFoxでは変化せず。IEはそもそもanimationに対応していないので対象外。

調べてるとFirefoxのSVG関連バグについての投稿がいろいろでてきたためこれもバグだろと勝手に思ってましたが、W3Cの[19.2.12 The ‘animate’ element](http://www.w3.org/TR/SVG/animate.html#AnimateElement)を読めと指摘されました。

`Data type <color>`によると

>Only additive if each value can be converted to an RGB color.

ということで仕様上、noneは指定できないとのこと。WebKitの動きが特殊なだけだと分かりました。

##代替案1

別のアニメーションを作りanimation-delayで開始時間をずらす。

<p data-height="250" data-theme-id="0" data-slug-hash="mywXRg" data-default-tab="result" data-user="kay8" class='codepen'>See the Pen <a href='http://codepen.io/kay8/pen/mywXRg/'>Animate SVG Path: using 2 keyframes</a> by Kei (<a href='http://codepen.io/kay8'>@kay8</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

##代替案2

fill-opacityを0から1に変化させる。

<div data-height="350" data-theme-id="0" data-slug-hash="GgEQra" data-default-tab="css" data-user="kay8" class='codepen'><pre><code>	.letter {
		position: relative;
		max-width: 1024px;
		margin: 0 auto;
	}
	.letter-svg {
		margin: 0 auto;
		position: relative;
		display: block;
	}

    .letter-svg-3 path{
        stroke:#000;
        fill:#000;
        fill-opacity:0;
        stroke-width:.2;
        stroke-dasharray: 800;
        stroke-dashoffset:800;
        -moz-animation:DASH3 3s ease-in-out 1s forwards;
        -webkit-animation:DASH3 3s ease-in-out 1s forwards;
        animation:DASH3 3s ease-in-out 1s forwards;
    }

    @-webkit-keyframes DASH3{
        0%  {stroke-dashoffset:800;}
		   80%  {stroke-dashoffset:0;fill-opacity:0;}
        100%{stroke-dashoffset:0;fill-opacity:1;}
    }
    @-moz-keyframes DASH3{
        0%  {stroke-dashoffset:800;}
		   80%  {stroke-dashoffset:0;fill-opacity:0;}
        100%{stroke-dashoffset:0;fill-opacity:1;}
    }</code></pre>
<p>See the Pen <a href='http://codepen.io/kay8/pen/GgEQra/'>Animate SVG Path: using fill-opacity</a> by Kei (<a href='http://codepen.io/kay8'>@kay8</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
</div><script async src="//assets.codepen.io/assets/embed/ei.js"></script>

* * *
次からはStack Overflowじゃなくて仕様読むようにします。。