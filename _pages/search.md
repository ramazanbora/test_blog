---
layout: page
title: Search
permalink: /search/
---

<!---
<script src="{{ site.baseurl }}/assets/some-script-2.js" type="text/javascript"></script>

<script src="{{ site.baseurl }}/assets/some-script-4.js" type="text/javascript"></script>


<script src="{{ site.baseurl }}/assets/some-script-3.js" type="text/javascript"></script>


--- >


<div id="search-container">
    <input type="text" id="search-input" placeholder="Search through the blog posts...">
    <ul id="results-container"></ul>
</div>

<script src="{{ site.baseurl }}/assets/simple-jekyll-search.min.js" type="text/javascript"></script>

<script>
    SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    searchResultTemplate: '<div style="text-align: left !important;"><a href="{url}"><h1 style="text-align:left !important;">{title}</h1></a><span style="text-align:left !important;">{date}</span></div>',
    json: '{{ site.baseurl }}/search.json'
    });
</script>
