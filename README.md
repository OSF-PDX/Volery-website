# Volery-website
This is the static site for Volery! -- Our conference app!
It's made using [Zola](https://www.getzola.org/).

To make a blog post add a markdown file to `content/blog/` i.e: `content/blog/post.md`. In that file you need to include some metadata before the post body, like so:

```markdown
+++
title = "this is my post"
date = 2025-10-28
+++
This is the body of my post.
```

Then to render the post run `zola build` in the repo directory and push the changes.

you can also colocate resources (if you want to include images)

by instend creating `content/blog/mypost/index.md` and then including `content/blog/mypost/mypic.jpg`.