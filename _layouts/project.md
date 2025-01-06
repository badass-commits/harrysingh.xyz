---
layout: post
---

{% assign repositoryList = site.github.public_repositories | where: "name", page.title %}
{% assign repository = repositoryList.first %}
{% include project-card.html goToGithub=true %}
{% include break.html %}
{{ content }}
