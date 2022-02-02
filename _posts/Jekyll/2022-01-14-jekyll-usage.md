---
layout: post
title:  "Jekyll使用"
date:   2022-01-14 16:30:00 +0800
categories: [jekyll, jekyll-usage]
tags: jekyll
---


<ul> 
	{% for post in site.posts %}   
    <div>      
        <a href="{{ post.url }}">👉🏼 {{ post.title }}</a>
    </div>
    {% endfor %}
</ul>



### 1.新建Repo

{% highlight bash %}
jekyll new RepoName
{% endhighlight %}

### 2.本地开启jeckll服务

{% highlight bash linenos %}
jekyll serve
{% endhighlight %}

### 3.markdown写作格式

{% highlight bash %}
/---
layout: post
title:  "Jekyll使用"
date:   2022-01-14 16:30:00 +0800
categories: jekyll update
/---
{% endhighlight %}

{% highlight bash %}
/{/% highlight bash linenos%/}/
/{/% endhighlight %/}/
{% endhighlight %}





