---
layout: post
title: Transitions Only After Page Load
tags: [jQuery]
permalink: transitions-only-after-page-load
---

To fix it, just add a class of "preload" to the body element.

{% highlight html %}
<body class="preload">
{% endhighlight %}

{% highlight css %}
.preload * {
  -webkit-transition: none !important;
  -moz-transition: none !important;
  -ms-transition: none !important;
  -o-transition: none !important;
}
{% endhighlight %}

{% highlight js %}
$("window").load(function() {
  $("body").removeClass("preload");
});
{% endhighlight %}
