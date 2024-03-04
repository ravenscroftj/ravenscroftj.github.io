---
public: true
tags: software
---
# Eleventy

A [[foss]] static site generator written in [[nodejs]].

## Tag Collection

[this post](https://claytonerrington.com/blog/11ty-nunjucks-tag-count/) shows how to add a collection for tags + tag counts:

```javascript

config.addCollection("tagList", collection => {
    const tagsObject = {}
    collection.getAll().forEach(item => {
      if (!item.data.tags) return;
      item.data.tags
        .filter(tag => !['post', 'all'].includes(tag))
        .forEach(tag => {
          if(typeof tagsObject[tag] === 'undefined') {
            tagsObject[tag] = 1
          } else {
            tagsObject[tag] += 1
          }
        });
    });

    const tagList = []
    Object.keys(tagsObject).forEach(tag => {
      tagList.push({ tagName: tag, tagCount: tagsObject[tag] })
    })
  return tagList.sort((a, b) => b.tagCount - a.tagCount)
});

```


## Adding Search
- [this blog post](https://www.belter.io/eleventy-search/) shows how you can add lunr search to an 11ty site.
- 