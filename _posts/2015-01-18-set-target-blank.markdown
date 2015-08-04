---
layout: post
title: JavaScriptによるtarget="_blank"の指定
date: 2015-01-18
published: true
excerpt: Markdown記法でtarget="_blank"を指定するのが面倒だったのでJavaScriptで外部サイトは別タブで開くように設定。
tags: javascript jekyll
cover_image: /2015/
---

Markdownで記事本文に外部リンクをはった際に自動でtarget="_blank"が設定されるように以下のコードを追加。

{% highlight javascript %}
(function() {
	var links = document.links;
	for (var i = 0; i < links.length; i++) {
		if (links[i].hostname != window.location.hostname) {
			links[i].target = '_blank';
		}
	}
}());
{% endhighlight %}

linksプロパティで文書中のarea/anchor要素をHTMLCollectionとして取得し、現在のURLのホスト名と取得した要素のホスト名が異なっていればtarget = "_blank"を指定。

ちなみに文書中から全て取得する必要はないので記事のみを対象に
```
Document.getElementsByClassName('post-content').links
```
とかやってみたものの、linksはdocumentオブジェクトに属するため無理でした
(参考: [documentオブジェクト](https://developer.mozilla.org/ja/docs/Web/API/document))。

基本的に外部サイトは別タブで開くようにしているので自分の場合はこれで問題ないですが、どうしても個別に指定したい場合はplugin探すか素直にhtml書いたほうがいいですね。

####追記
Markdownのパーサーにkramdownを使っていれば

```
[link](url){: attribute="value"}
```

が使えるので`{:target="_blank"}`をつけてあげれば対応可能と知りました。






