---
layout: post
title: JavaScriptによるtarget="_blank"の指定
date: 2015-01-14
published: false
excerpt: Markdown記法でtarget="_blank"を指定するのが面倒だったのでJavaScriptで設定するようにしました。
tags: css
cover_image: /2015/
---
![Jekyll](/images/2015/0108-jekyll.png)

(Image credit: [Jekyll](http://jekyllrb.com/))
{: .credit}




昨年末にブログを作ろう、と思い立ち検討した結果Jekyllになりました。その他の選択肢としては

1. [Hatena blog](http://hatenablog.com/), [Medium](https://medium.com/)
2. [WordPress](https://wordpress.org/)
3. [Hugo](http://gohugo.io/)

等があったものの、
1:カスタマイズ性に欠けるためメインには使いづらい、
2:管理画面から操作するのが面倒、
3:Go全く分からないのでそもそも完成するか怪しい(面白そうだけど...)

ということでシンプル且つそれなりに柔軟性がありそうなJekyllに。他の理由としては基本的にcommitとpushしかしていないGit/GitHubとRubyの勉強にもなりそうだという点が大きいです。

というわけで以下、導入から運用までのメモ。

##導入

- [Jekyllいつやるの？ジキやルの？今でしょ！](http://melborne.github.io/2013/05/20/now-the-time-to-start-jekyll/)

- [Build A Blog With Jekyll And GitHub Pages](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/)

構造含めてざっと把握したかったのでこの辺りから読みました。途中まで自分で作っていたもののゼロからCSS書くのが面倒になったため最終的に `jekyll new` コマンドでひな形作成してカスタマイズ。一つ目はVersion1.0が前提なので最新版とは異なる点もありますが分かりやすかったです。

##ホスト

- [What are GitHub Pages?](https://help.github.com/articles/what-are-github-pages/)

GitHub Pageを使えばmasterブランチにコミットするだけでサイトの公開が可能。ただ、GitHub Page上で動的にファイルを生成することができないためPluginは動かず。結局gh-pagesブランチにローカル環境でbuildしたファイルをデプロイすることにしました。

##カスタムドメイン

お名前.comで取得したドメインにサブドメイン設定してCNAMEを追加しました。当初Aレコードを追加していましたが[このページ(Faster, More Awesome GitHub Pages)](https://github.com/blog/1715-faster-more-awesome-github-pages)をよく読めと怒られたので修正。*username.github.ioのusernameには自身のgithubアカウントを設定

##デプロイ

- [俺の最強ブログシステムも火を噴いてたぜ](http://webtech-walker.com/archive/2012/09/fired-myblog.html)

- [Jekyll + Github Pagesでブログを作る](http://chikathreesix.com/?p=297)

gh-pagesブランチへの静的ファイルデプロイについては最終的に[hokaccha氏](https://github.com/hokaccha/webtech-walker/blob/f2b178baa3bb00776f089f50b7b3e2954c83694c/Rakefile#L10-20)のrakefileを参考にさせて頂きました。

##その他
コメント欄は[DISQUS](https://disqus.com/)を使って設置している方が多いみたいなので必要になったら要検討。
