---
layout: project
title: med-map
category: projects
tags: react
---

## Summary

In 2014, when I was still new to software development, I was discussing medical data visualization with a friend in the medical program. This gave me the idea to try displaying occurence rates geographically, rather than in a graph. I found the [CDC Wonder API](https://wonder.cdc.gov/wonder/help/WONDER-API.html){:target="\_blank" rel="noopener noreferrer"} to actually retrieve the data.

I originally wrote this as a single page website that used jQuery and [Raphael.js](http://raphaeljs.com){:target="\_blank" rel="noopener noreferrer"}, a JS SVG library. I later refactored the website to be a React app, using a npm package called [react-svg-maps](https://www.npmjs.com/package/react-svg-map){:target="\_blank" rel="noopener noreferrer"}. While working on this, I ended up adding TypeScript to my app which required me to create a [@types/react-svg-map](https://www.npmjs.com/package/@types/react-svg-map){:target="\_blank" rel="noopener noreferrer"} entry in [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped#readme){:target="\_blank" rel="noopener noreferrer"}.

The website also displays information based on the condition you are currently looking at:

- links to find volunteering opportunities using [Volunteer Match](https://www.volunteermatch.org){:target="\_blank" rel="noopener noreferrer"} and [AARP's Create the Good](https://createthegood.aarp.org/volunteer-search.html){:target="\_blank" rel="noopener noreferrer"}
- census data retrieved from the [US Census Bureau](https://www.census.gov/data/developers.html){:target="\_blank" rel="noopener noreferrer"}
- relevant books from [Springer](https://www.springer.com/us){:target="\_blank" rel="noopener noreferrer"}
- relevant papers from [PubMed](https://pubmed.ncbi.nlm.nih.gov/){:target="\_blank" rel="noopener noreferrer"}
