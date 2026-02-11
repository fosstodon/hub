---
title: Fosstodon Hub
header: Fosstodon Hub
description: The largest FOSS focussed instance on the Fediverse.
permalink: /
layout: landing
---

{% assign target_page = site.pages | where: "title", "About | Fosstodon Hub" | first %}
{% if target_page %}
  {{ target_page.content | markdownify }}
{% else %}
  <p>Error: Page not found.</p>
{% endif %}

<!-- **THESE LINKS ARE HIDDEN ON THE FRONT END** - they're only used for Mastodon verification purposes -->
<div class="verification-links">
  <a rel="me" href="https://mastodon.social/@fosstodon">Mastodon</a>
  <a rel="me" href="https://fosstodon.org/@kev">Mastodon</a>
  <a rel="me" href="https://fosstodon.org/@mike">Mastodon</a>
</div>
