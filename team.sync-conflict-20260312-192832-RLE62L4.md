---
title: The Team | Fosstodon Hub
description: A list of the Fosstodon team members and their roles.
permalink: /team/
layout: default
---
# Meet The Team

It takes a lot of work to keep the Fosstodon running. Whether that's moderating reports, providing advice to moderators, creating and editing documentation, or just keeping the lights on and the wheels turning.

This page lists all the amazing volunteers that keep this ship afloat.

## Admins

Admins are responsible for all the stuff that goes on behind the scenes - like responding to DDoS attacks, [large influxes of users](https://hub.fosstodon.org/elon-twitter-post-mortem/) and working with vendors like [Masto.host](https://masto.host) and [Fastly](https://fastly.com), to improve the service for all our members.

{% for member in site.data.admins %}
<div class="team-banner">
    <p class="team-title"><a target="blank" href="{{ member.link }}">{{ member.name }}</a></p>
    <img class="team-avatar" src="{{ member.avatar }}" />
    <p><b>Role:</b> {{ member.role }}</p>
    <p>{{ member.description }}</p>
  </div>
{% endfor %}

<div style="clear: both;"></div>

## Senior Moderators

Our Senior Moderators play a crucial role in offering support and guidance to the moderation team, in addition to crafting and enhancing the documentation that accompanies Fosstodon, such as [our Code of Conduct](https://hub.fosstodon.org/coc) and moderation guidelines. They are also actively involved in the ongoing development and enhancement of Fosstodon, contributing both technically and within the community, collaborating closely with the founders to ensure the platform's continued improvement.

{% for member in site.data.senior-mods %}
<div class="team-banner">
    <p class="team-title"><a target="blank" href="{{ member.link }}">{{ member.name }}</a></p>
    <img class="team-avatar" src="{{ member.avatar }}" />
    <p><b>Role:</b> {{ member.role }}</p>
    <p>{{ member.description }}</p>
  </div>
{% endfor %}

<div style="clear: both;"></div>

## Moderators

The moderators are the unsung heroes of Fosstodon. They're the people who work every single report we receive, and take appropriate action to keep Fosstodon a friendly and inclusive place for all our members.

If you're interested in becoming a moderator, please [contact us](https://hub.fosstodon.org/contact/).

{% for member in site.data.mods %}
<div class="team-banner">
    <p class="team-title"><a target="blank" href="{{ member.link }}">{{ member.name }}</a></p>
    <img class="team-avatar" src="{{ member.avatar }}" />
    <p><b>Role:</b> {{ member.role }}</p>
    <p>{{ member.description }}</p>
  </div>
{% endfor %}

<div style="clear: both;"></div>


## Founders

Kev and Mike are the founders of Fosstodon. It was their idea to start this whole thing in the first place. They started out simply wanting a vanity handle on the Fediverse, but later decided to open things up to other FOSS and tech enthusiasts. As so, Fosstodon was born.

In April 2025, both Kev and Mike decided to step down in their roles with Fosstodon and have passed the batton over to Gina.

{% for member in site.data.founders %}
<div class="team-banner">
    <p class="team-title"><a target="blank" href="{{ member.link }}">{{ member.name }}</a></p>
    <img class="team-avatar" src="{{ member.avatar }}" />
    <p><b>Role:</b> {{ member.role }}</p>
    <p>{{ member.description }}</p>
  </div>
{% endfor %}

<div style="clear: both;"></div>
