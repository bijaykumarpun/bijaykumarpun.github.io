---
layout: page
title: tags
permalink: /tags/
---

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
<div style="margin-top:20px; color:green;">


    #{{ category_name }}
</div>    


{% for post in site.categories[category_name] %}
<div style="margin-left:20px;">
      - <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
</div>    
{% endfor %}
  </div>
{% endfor %}
</div>
