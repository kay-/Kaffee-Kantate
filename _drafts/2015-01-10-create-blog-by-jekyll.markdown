---
layout: post
title:  "Jekyllで作ったブログをGitHub Pagesにホストする"
date:   2015-1-10
excerpt: 新年ということでJekyllでブログ作ってgh-pagesにホストしてカスタムドメイン設定してみました。
tags: jekyll github
cover_image: /2015/0108-jekyll.png
---
![Jekyll](/images/2015/0108-jekyll.png)

> (Image credit: [Jekyll](http://jekyllrb.com/))




昨年末にブログを作ろう、と思い立ち検討した結果Jekyllになりました。その他の選択肢としては

1. [Hatena blog](http://hatenablog.com/), [Medium](https://medium.com/)
2. [WordPress](https://wordpress.org/)
3. [Hugo](http://gohugo.io/)

があったものの、
1:カスタマイズ性に欠けるためメインには使いづらい、
2:管理画面から操作するのが面倒、
3:Go全く分からないのでそもそも完成するか怪しい(面白そうだけど...)

ということでシンプル且つそれなりに柔軟性がありそうなJekyllに。他の理由としては基本的にcommitとpushしかしていないGit/GitHubとRubyの勉強にもなりそうという点が大きいです。

というわけで以下、導入から運用までのメモ。

##導入

構造含めてざっと把握したかったのでこの辺りから読みました。ゼロからCSS書くのが面倒になったため最終的に `jekyll new` コマンドでひな形作成してカスタマイズ。前者はVersion1.0なので最新版とは異なる点もありますが分かりやすかったです。

- [Jekyllいつやるの？ジキやルの？今でしょ！](http://melborne.github.io/2013/05/20/now-the-time-to-start-jekyll/)

- [Build A Blog With Jekyll And GitHub Pages](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/)





~~~~~~~~
lll
~~~~~~~~





To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
