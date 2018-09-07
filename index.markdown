---
layout: default
title: Home
---

Hi! I am Xitong, an [Open Source][oss] enthusiast. This site is dedicated to provide informations about [me](resume.html) and [what I do](/work).

<p><br /><b>My Blog:</b></p>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>

<p><b>Find me on:</b></p>

<ul>

<li><a href="https://github.com/lixit/">Github</a></li>

</ul>
<p><br /><b>Contact Information:</b></p>

<blockquote>
lixiton@gmail.com
</blockquote>

[oss]:http://en.wikipedia.org/wiki/Open_source
