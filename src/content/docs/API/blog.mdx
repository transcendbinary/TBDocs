---
title: Blog
description: Our blog API
---
### api.transcendbinary.co.uk/blog/index.json
## Overview

Our blog API stores an index of blog posts stored in our CDN.

the index is a JSON file containing a sinlge array of filenames:
```json
[
  "20260813-152950.md",
  "20260924-190140.md",
  "20260929-015230.md"
]
```
Posts themselves are stored as markdown files in the CDN at `https://cdn.transcendbinary.co.uk/blog/posts` and can be accessed directly.

## Usage

The index can be fetched using a simple GET request to `https://api.transcendbinary.co.uk/blog/index.json`.
```javascript
fetch(index)
    .then(response => {
        if (!response.ok) {
            throw new Error(`Failed to load index.json: ${response.status}`);
        }
        return response.json();
    })
```
The returned JSON array can then be filtered, sorted and sliced to get the latest posts,
```javascript
    .then(files => {
        const markdownFiles = files
            .filter(file => file.toLowerCase().endsWith(".md"))
            .sort((a, b) => b.localeCompare(a))
			.slice(0, 5);
```
and the markdown files can be fetched and converted to HTML using a markdown parser like `marked`.
```javascript
return Promise.all(
    markdownFiles.map(file =>
        fetch(cdn_directory + file)
            .then(response => {
                if (!response.ok) {
                    throw new Error(`Failed to load ${file}: ${response.status}`);
                }
                return response.text();
            })
            .then(markdown => marked.parse(markdown))
    )
);
```
the resulting HTML strings can be joined together, formatted and displayed in the page as HTML.
```javascript
.then(contents => {
        document.getElementById("markdown-content").innerHTML =
            contents.join("<br><hr><br>");
    })
```
```html
<body style="background-color: #222; display: flex; flex-direction: column; min-height: 100vh; margin: 0;" >
	<div style="flex: 1">
	<div id="markdown-content" style="padding: 20px"></div>
	</div>
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
<script src="/js/markdownParser.js"></script>
</body>
```