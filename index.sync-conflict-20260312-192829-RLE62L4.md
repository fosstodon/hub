---
title: Fosstodon Hub
header: Fosstodon Hub
description: The largest FOSS focussed instance on the Fediverse.
permalink: /
layout: default
---

{% for post in site.posts %}
  <p class="blog-item"><b><a href="{{ post.url }}">{{ post.title }}</a></b><br>
  <span class="post-description">{{ post.description }}</span><br>
  <span class="post-meta">📅 {{ post.date | date_to_string }}</span></p>
{% endfor %}

<!-- **THESE LINKS ARE HIDDEN ON THE FRONT END** - they're only used for Mastodon verification purposes -->
<div class="verification-links">
  <a rel="me" href="https://mastodon.social/@fosstodon">Mastodon</a>
  <a rel="me" href="https://fosstodon.org/@kev">Mastodon</a>
  <a rel="me" href="https://fosstodon.org/@mike">Mastodon</a>
</div>
