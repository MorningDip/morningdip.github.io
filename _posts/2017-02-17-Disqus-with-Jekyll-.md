---
layout: 	post
title: 		"Disqus with Jekyll"
subtitle: 	"為你的部落格加上Disqus留言插件"
comments: 	true
tags:		[disqus, jekyll]
---

## 什麼是Disqus

![alt text](https://www.drupal.org/files/project-images/disqus_logo_-_white_on_blue_background.png)

Disqus提供一個簡單、方便而且超快速的方法，為你的部落格嵌入討論串的功能，你不用去擔心自己還要弄Database那些有的沒的，也不用煩惱到要該安裝Facebook留言插件，還是Google+留言插件，Disqus統合所有帳號，同時還還可以幫你統計最近被熱烈討論的文章，種種的方便管理好處，非常適合Jekyll Blog。

## 萬事起頭總是先辦個帳號

來到[Disqus](https://disqus.com/)辦個帳號。

辦好帳號會來到這個頁面，我們選擇下面這個選項`I want to install Disqus on my site`為我們的部落格嵌入Disqus討論串。

![alt text](http://i.imgur.com/gUnKZkf.png)

下一個頁面為我們的Disqus設定一個`Website Name`，它是用來產生一個獨一的disqus URL，基本上就命名自己看得懂的名字，像是你的部落格名稱，種類`Category`、語言`Language`，就按照自己喜好設定，然後點選`Create Site`。

![alt text](http://i.imgur.com/yezHJwo.png)

接著選擇平台，這邊理所當然選擇`Jekyll`。步驟一主要是跟你說明，你可以在你的markdown文件新增一個變數`comments`在標頭，這是方便你覺得該篇文章要不要開起討論串的功能，格式類似這樣：

![alt text](http://i.imgur.com/sDczcRY.png)
![alt text](http://i.imgur.com/Tc13rGp.png)

	---
	layout:		post
	title:		標題
	subtitle:	子標題
	comments:	true
	---

另外編輯`_layouts/default.html`，在第11行後段插入程式碼`{% raw %} {% include comments.html %} {% endraw %}`：

```html
{% raw %}
<!DOCTYPE html>
<html lang="en-us">

  {% include head.html %}

  <body class="theme-base-08">

    {% include sidebar.html %}

    <div class="content container">
      {{ content }} {% include comments.html %}
    </div>
  </body>
</html>
{% endraw %}
```
![alt text](http://i.imgur.com/EowLJmz.png)

最後我們在`_includes/`資料夾底下新增一個`comments.html`，貼上剛剛步驟二所產生的`Universal Embed Code`，並在頭尾個加上`{% raw %} {% if page.comments %} {% endraw %}`與`{% raw %} {% endif %} {% endraw %}`，像是這樣：

```html
{% raw %}
{% if page.comments %}
<div id="disqus_thread"></div>
<script>

var disqus_config = function () {
this.page.identifier = '{{ page.url }}';
};

(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = '//morningdip-github-io.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}
{% endraw %}
```

特別要注意的是`this.page.url`與`this.page.identifier`必須依照自己的網站設定，基本上把我`this.page.url`中的`morningdip`替換成你的網域username就沒問題了，`s.src`這個變數Disqus會自動幫你生成你帳號對應的變數值，別傻傻地也把我的設定複製過去了。