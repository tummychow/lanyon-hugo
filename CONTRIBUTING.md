# Contributing

So you want to help me with Lanyon-Hugo? **AWESOME**!

I'm not a designer, nor do I know CSS or HTML. Most of those things are coming straight out of the original Lanyon. However, the parts that make it work with Hugo, those are mine. And if you're interested, what's mine is yours. I'll explain what has changed from the original Lanyon, if you were familiar with that theme already. And I'll explain the structure of this Hugo theme, assuming you already understand some of how Hugo works.

Hugo's docs are a bit lacking in the "big picture" of how things fit together (I might submit a PR when I'm more familiar with the tool), but they're quite complete. I recommend you read them first.

## Layouts
Lanyon-Hugo uses two content types, `fixed` and `post`. These are analogous to Lanyon's `page` and `post` layouts, respectively. The `fixed` type is meant to be very simple, for pages that don't need any of the support structure provided by a blog (no tags, no dates, etc). The `post` type is more detailed; it has a list view and stuff like that.

They both have single views, which are quite similar. In fact, the only difference is that `post` shows a date, where as `fixed` does not. [This](http://golang.org/pkg/time/#Time.Format) documentation explains how to change the date formatting. This format is set in the `config.json` under `.Site.Params.DateForm`, so you can affect the entire site at once.

Both content types call out to a set of general HTML files which provide the universal bits and pieces. These are stored in `layouts/chrome`, which is a Hugo convention, and they are analogous to Lanyon's `_includes`.

In Jekyll, you can nest layouts. Lanyon's `page` and `post` layouts are both based on a `default` layout. The `default` layout is the one that provides things like the header and the sidebar. But Hugo doesn't have this functionality, so I took the `default` layout, and I split it into two files: `default_head.html` and `default_foot.html`. These two are meant to be included at the top and bottom, respectively, of any other content views. You can see this in `fixed/single.html` and `post/single.html`.

## Sidebar
The most interesting chrome is probably `layouts/chrome/sidebar.html`. This is mostly based on Lanyon's `_includes/sidebar.html`, but ported to Go templates instead of Liquid. We identify the homepage and postlist via `.Url`. Rendered pages (with a content type) do not implement the `.Url` variable, so it comes back as the blank string.

Any pages whose front matter sets the `sidebar` flag are also added to the sidebar (sorted by weight). We match the active page (if any) using its `.Permalink`. Both nodes and pages provide the `.Permalink` variable, so this lets you pin any content to the sidebar. The sidebar also retains the GitHub integration from the original Lanyon, where it lists a repository of your choice.

## Homepage
Hugo implements homepages as a special layout, which does not correspond to any content type. This gets generated into a page called a node. You can see this in `layouts/index.html`. If you want to change the number of posts listed on the homepage, just change the `pagination` variable. One inconvenience of Hugo's system is that you can't include front matter for nodes (as far as I know).

The index implements a full view of each item whose content type is `post`. This is quite repetitive and overlaps heavily with `post/single.html`. I plan to add a `post/summary.html` in the future, which does not include the default header and footer, and which sets the post title to a link. Then, I can replace this with `{{ .Render "summary" }}` to reduce code repetition.

## Post List
The post list is implemented using a Hugo section index, which can list pages under a certain content type (in this case, the `post` type). This index is defined at `layouts/indexes/post.html`. It renders posts using the `layouts/post/li.html` view, which just shows the post's time and date as a list item. Hugo indexes are also nodes, like the homepage (a node is any page in the output, that doesn't have a content type).

## Statics
Jekyll will take every file in its source directory and mirror it in the destination, unless the file's name begins with an underscore. Hugo is not quite so inclusive. The contents of the `static` directory are mirrored into the root of the destination exactly as they are. This is where the Lanyon/Poole CSS files are placed. I have not changed those files at all (literally nothing).

If your GitHub Page has a custom name, the `CNAME` file should go in this directory.
