---
layout: post
title: SVGアニメーションを行う上で遭遇したイシュー
date: 2016-04-02
published: true
excerpt: SVGアニメーションにおけるブラウザ動作環境の違いなど
tags: svg css
cover_image:
---

仕事でSVGアニメーションをやったものの予想以上に大変だったので遭遇したイシューをいくつか。ブラウザ環境に依存する話が多いのであくまで __2016年4月2日__ 時点の内容です。

##[Firefox] SVG要素に対してtransform-originが正しく動作しない

現状だとFirefoxでtransform-originを他のブラウザと同じように動作させるには、

- `transform-box: fill-box;`を設定
- preferenceにて`svg.transform-origin.enabled`を有効

にしなければならない模様。

これはtransform及びtransform-originにおけるポジションを規定する`transform-box`というプロパティがまだW3Cにおいてドラフトだから、という理由からくる実装らしい。なのでSVG要素をtransformさせたい場合は現状JavaScriptを使うしかなさそう。([Bug 1209061 - transform-origin not applied correctly on svg content](https://bugzilla.mozilla.org/show_bug.cgi?id=1209061))

>You'd need to set transform-box: fill-box; and also enable the svg.transform-origin.enabled pref (Firefox 41, 42) or the svg.transform-box.enabled pref (Firefox 43).


##[IE(9以上)] SVG要素を正しいアスペクト比で表示させるには幅と高さの設定が必要

他のブラウザでは'width'と'height'を設定していなくても問題ないですが、残念ながらIEの場合、元のアスペクト比を保てない。([Test Scaling Of SVG Images In Fluid Layouts](http://codepen.io/tomByrer/pen/qEBbzw?editors=110))

><svg ... viewBox="0 0 500 500" width="500px" height="500px" preserveAspectRatio="xMinYMin meet">

pxで値を設定してしまうとレスポンシブにならないため、user-agentがIEのときのみwindow resizeに合わせて縦横の値を調整するようにしました。

##[Chrome] 複雑なパスの場合、stroke-dasharrayを正しく描画できない

波線状のストロークを描画する`stroke-dasharray`を複雑なパスに用いるとChromeでは描画されなくなるバグ。どの程度の複雑性なら描画されるのか不明。それぞれのパスが独立していても全体に影響することが多々あったのでファイルサイズや要素数も関係しているのかもと勝手に予想してはいますが...

検索してみるとこの問題を報告しているブログ等が多く見つかるので有名なバグのよう。もとのSVGファイルを修正して破線状のパスを減らすしかないのでは。([SVG stroke-dasharray applies dashes across disconnected (M) path segments.](https://bugs.chromium.org/p/chromium/issues/detail?id=364866))


##[Snap.svg] animate APIはパフォーマンスに問題があるため、アニメーションさせたい場合は別の方法との組み合わせを

SVGを操作するライブラリとして有名な[Snap.svg](http://snapsvg.io/)(jQuery for SVGのような役割)ですが、animate APIを使うとかなりパフォーマンスに問題がでます。([Adventures with SVG animation and Snap.svg](http://www.newicon.net/svg-animation-snapsvg/))

リンク先の記事では以下の通りフレームレートの低さを指摘していますが、CPU使用率もかなり高くなってしまいました。

>Both scripting and rendering were taking longer than was needed for a clean 60fps framerate...I found a ton of timers firing as each animation loop stacked atop the other. In addition to this, rendering time was also significant

簡単なアニメーションならVanilla JSで、そうでないならパフォーマンス的にも安定した[Velocity.js](http://julian.com/research/velocity/)や[GSAP](https://greensock.com/gsap)との併用が必要になります。


##[Illustrator] 破線状のラインを多用するとファイルサイズが著しく肥大化

これはイラストレータ及びSVGファイルの話ですが、破線状のラインを使うと、破線のドットそれぞれにanchor pointが設定されるためファイルサイズが極端に肥大化。破線ライン以外には単純な丸と四角のオブジェクトしか使われていないようなファイルが簡単に1MB近くなったりするので注意。

理由がわからず困っていたところ即答してくれた[Aki Aoki](http://akiaoki.com/)氏には感謝。