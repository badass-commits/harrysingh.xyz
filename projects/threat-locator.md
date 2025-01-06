---
layout: project
title: threat-locator
category: projects
tags: electron javascript
---

![Threat Locator](/assets/images/projects/threat-locator/screenshots/ThreatLocator.png)

## Summary

While my dad was working on his Master's in Cybersecurity, we came up with the idea to make this little utility for fun. It was inspired by some of his homework to quarantine and execute questionable payloads to see where they tried to communicate with. I wanted to learn Electron and used this as the opportunity to do so.

This app uses Electron, [node-netstat](https://www.npmjs.com/package/node-netstat){:target="\_blank" rel="noopener noreferrer"}, and [Leaflet.js](https://leafletjs.com){:target="\_blank" rel="noopener noreferrer"} to draw lines between you and the location of all of your current connections in real-time.

While working on this, I ended up adding TypeScript and Webpack to my app which required me to create a [@types/node-netstat](https://www.npmjs.com/package/@types/node-netstat){:target="\_blank" rel="noopener noreferrer"} entry in [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped#readme){:target="\_blank" rel="noopener noreferrer"}.
