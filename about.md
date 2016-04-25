---
layout: pages
title: "About"
description: "嘿，你總算找到我啦"
header-img:  "img/about.jpg"
---

<div id="hitokoto"><script>hitokoto()</script></div>

>
>敲敲代码，学学设计，随意捣鼓。
>世界那么大，我想去看看。
>

<center>
    <img src="http://7xqllw.com1.z0.glb.clouddn.com/about-person.png" title="Logo" width="150" high="150">
</center>

--- 


Well...This is a tough question.  
My Name is Voleking. You may find me in sites like zhihu.com / douban.com / github / twitter, so on and so forth. It’s easy to know me. However, I don't have a deep insight into myself. This blog may help you and me to know me better.  

大学僧，程序猿。喜欢折腾的伪技术宅，刚入门的ACMer，想要学些设计，学学摄影。一点点 geek，一丢丢的执著，恰到好处就够。日常之中，多的是折腾劲，也希望能添几分专注、几许勇敢。 努力向上ing。这就是我。  

*——Voleking*


> Be the change you wish to see in the world.

<center>
    <p><img src="http://dreamofbook.qiniudn.com/hacker.png" align="center"></p>
</center>


{% if site.duoshuo_username %}
<!-- 多说评论框 start -->
<div class="comment">
    <div class="ds-thread"
    {% if site.duoshuo_username == "huxblog" %}
        data-thread-id="1187623191091085319"
    {% else %}
        data-thread-key="{{site.duoshuo_username}}/about"
    {% endif %}

    data-title="{{page.title}}"
    data-url="{{site.url}}/about/"></div>
</div>
<!-- 多说评论框 end -->

<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
    // dynamic User hacking by Hux
    var _user = '{{site.duoshuo_username}}';

    // duoshuo comment query.
    var duoshuoQuery = {short_name: _user };
    (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0]
         || document.getElementsByTagName('body')[0]).appendChild(ds);
    })();
</script>
<!-- 多说公共JS代码 end -->
{% endif %}


{% if site.disqus_username %}
<!-- disqus 评论框 start -->
<div class="comment">
    <div id="disqus_thread" class="disqus-thread">

    </div>
</div>
<!-- disqus 评论框 end -->

<!-- disqus 公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES * * */
    var disqus_shortname = "{{site.disqus_username}}";
    var disqus_identifier = "{{site.disqus_username}}/{{page.url}}";
    var disqus_url = "{{site.url}}{{page.url}}";

    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<!-- disqus 公共JS代码 end -->
{% endif %}

