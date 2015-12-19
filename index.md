---
title: Home
---

# Exploreapollo.org Project Documentation

## Project Repositories

- [project.exploreapollo.org](https://github.com/UTD-CRSS/project.exploreapollo.org): Overall project planning and documentation.
- [exploreapollo.org](https://github.com/UTD-CRSS/exploreapollo.org): The entry point for the exploreapollo.org project.
- [audio.exploreapollo.org](https://github.com/UTD-CRSS/audio.exploreapollo.org): Provides endpoints that mixes and streams combinations of audio channels.
- [exploreapollo.org-schema](https://github.com/UTD-CRSS/exploreapollo.org-schema): Documentation and scripts to support the RDBMS used by the API and audio servers.
- [app.exploreapollo.org](https://github.com/UTD-CRSS/app.exploreapollo.org): The primary web application interface.
- [API.exploreapollo.org](https://github.com/UTD-CRSS/API.exploreapollo.org): Provides REST and WebSocket endpoints for the web application.

## Documents

{% for page in site.pages %}
- [{{ page.title }}]({{ page.url }})
{% endfor %}

## Posts

<ul>

{% for post in site.posts %}

<li>
<div class="post-date">
<span>{{ post.date | date: "%b %d, %Y" }}</span>
</div>
<div class="title">
<a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
</div>
</li>

{% endfor %}

</ul>
