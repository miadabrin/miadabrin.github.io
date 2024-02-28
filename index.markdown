---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---
<h1> List of Posts </h1>
{% for post in site.posts %}
<li>
  <a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}