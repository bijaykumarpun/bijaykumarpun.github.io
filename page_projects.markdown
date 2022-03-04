---
layout: page
title: projects 
permalink: /projects/
---

<div>


  {%- if site.posts.size > 0 -%}
    <ul class="post-list"> 
      {%- for post in site.posts -%}
      <li style=" margin-top:20px; ">
              <a class="post-link" href="{{ post.url | relative_url }}" style="color:green;">
            {{ post.title | escape }}
          </a>
       
        
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <div>

                {{ post.excerpt }}


                <a href="{{post.url}}" style="font-size:16px;">Continue reading...</a> 
        </div>      
      </li>
      {%- endfor -%}
    </ul>

    <!-- <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p> -->
  {%- endif -%}

</div>          
