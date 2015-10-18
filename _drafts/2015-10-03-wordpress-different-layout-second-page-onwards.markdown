---
layout: post
title: WordPress - 記事一覧で2ページ目以降のレイアウト及び記事表示数を変更する
date: 2015-10-03
published: false
excerpt: get query varによるページ送り番号取得とWP Queryのoffsetパラメータ指定。
tags: wordpress
cover_image: /common/wordpress.png
---

ブログ記事一覧ページにて1ページ目だけ特集記事を表示したり、2ページ目以降レイアウトの都合から記事表示数を変更したい場合に。

##Practicum概要

1. Get the Current Page Number
http://wordpress.stackexchange.com/questions/12372/get-the-current-page-number
{% highlight php %}
     $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
{% endhighlight %}
2. set condition for post number and page offset like this
{% highlight php %}
                if ($paged === 1) {
                    $post_num = 13;
                    $post_offset = 0;
                } else if ($paged === 2) {
                    $post_num = 16;
                    $post_offset = 13;
                } else {
                    $post_num = 16;
                    $post_offset = 13 + ($paged - 2) * 16;
                }
                $query = new WP_Query(array(
                    'posts_per_page'   => $post_num,
                    'offset' => $post_offset
                ));
{% endhighlight %}
3. Loop and condition inside
{% highlight php %}
     <?php if (have_posts()) : while ($query->have_posts()): $query->the_post(); ?>
          <?php if ( $paged !== 1 ): ?>
{% endhighlight %}