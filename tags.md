---
layout: page
title: Tags
header: Posts By Tag
group: navigation
---

<style>
  .tag-posts {display: none;}
</style>

<div class="pageTitle" id="tagTitle">Querying...</div>

{% capture tags %}
    {% for tag in site.tags %}
        {{ tag[0] }}
    {% endfor %}
{% endcapture %}
{% assign sortedtags = tags | split:' ' | sort %}

{% for tag in sortedtags %}
<div id="tag-{{ tag }}" class="tag-posts">
    {% for post in site.posts %}
        {% for otag in post.tags %}
            {% if tag == otag %}              
                <blockquote>
                    <h3><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h3>
                    <div class="time">{{ post.time }}</div>
                    
                    <div class="tagPanel">

                    {% for t in post.tags %}
                        <a href="{{ site.url }}/tags?tag={{ t }}"><div class="tag">{{ t }}</div></a>
                    {% endfor%}
                    
                    </div>
                    
                </blockquote>
            {% endif %}
        {% endfor %}
    {% endfor %}
</div>
{% endfor %}

<script type="text/javascript">
    function getParameterByName(name) {
        var regex = new RegExp("[\\?&]" + name + "=([^&#]*)"),
            results = regex.exec(location.search);
        return results == null ? "" : decodeURIComponent(results[1].replace(/\+/g, " "));
    }
    
    window.onload = function() {
        var tag = getParameterByName('tag');
        if (tag && document.getElementById('tag-' + tag)) {
            document.getElementById('tag-' + tag).style.display = 'block';
            document.getElementById('tagTitle').innerHTML = tag;
        } else {
            document.getElementById('tagTitle').innerHTML = 'Illegal Tag Query';
        }
    };
</script>