---
layout: default
title: Home
---

Hi! I am Xitong, a MS CS student in University of Central Florida. Here is my [resume](resume.html)

<p><br /><b>My Blog:</b></p>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>

<p><b>Find me on:</b></p>

<ul>

<li><a href="https://www.linkedin.com/in/lixitong/">LinkedIn</a></li>
<li><a href="https://github.com/lixit/">Github</a></li>
<li><a href="https://leetcode.com/lixiton/">LeetCode</a></li>
<li><a href="https://stackoverflow.com/users/10984033/xitong">Stack Overflow</a></li>

</ul>
<p><br /><b>Contact Information:</b></p>

<blockquote>
xitong@ucf.edu
</blockquote>
