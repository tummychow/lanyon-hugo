# Lanyon for Hugo

[Lanyon](http://github.com/poole/lanyon) is a great theme for [Jekyll](http://jekyllrb.com). This is a port of that theme, but to another static site generator, [Hugo](http://github.com/spf13/hugo). I'm aiming to get the same look and interactions as the original Lanyon.

Hugo and Jekyll are similar in that, out of the box, you can't make a presentable website out of them. You need some kind of theme first, or otherwise your site will be *really* bare-bones. If you're a designer, you might be comfortable doing that yourself. If you aren't, Jekyll has a thriving ecosystem of themes waiting for you. Hugo, being younger than Jekyll, does not. Lanyon-Hugo attempts to remedy that problem.

Lanyon-Hugo is a theme designed for blogging. While Hugo is flexible enough to turn almost any static content into a website, this theme is focused on blog-like use cases. Lanyon-Hugo retains the CSS, and therefore the look and feel, of the parent theme, Lanyon. This includes a sidebar that is hidden by default, and can be toggled with a button (implemented entirely in CSS). The sidebar gives some convenient navigation links, but when it is hidden, Lanyon-Hugo, just like Lanyon, is discreet and puts your content front and center.

## Usage

To begin authoring content, all you have to do is clone this repository and start writing Markdown files in [`content/post`](content/post). Front matter for Hugo can be written in JSON, YAML or TOML. I am using JSON out of preference, but it's your content - use whatever language you want. Two example posts are already provided (lifted from the parent Lanyon, with links fixed for Hugo) as an example of the front matter you need.

Note for Jekyll users: Jekyll parses the date out of your post's title, but Hugo does not. You must specify a date in the front matter. I specify the permalinks to look like Jekyll's in `config.json`, so if you set the date correctly, the permalinks will also look correct.

Hugo's universal config file is [`config.json`](config.json) (or YAML, or TOML). You can change the base URL of your site, the title, and the tagline from this file. The link to your GitHub repository (for whatever the site represents, say a dev blog, or a personal GitHub Page) can also be changed here. If you are familiar with Hugo, you already know that you can add more parameters to the `params` object to introduce more variables.

### Fixed Pages

The original Lanyon had a layout for "pages", fixed content that didn't have a date. Lanyon-Hugo retains this concept, and refers to these pages as "fixed" (that's the content type, if you're familiar with Hugo concepts). Fixed pages will not display a date, only a title, and they will not be listed on the homepage of your site. Pages such as About (an example `about.md` has been lifted from the parent Lanyon) should generally be fixed.

You can alter the content of the custom 404 via [`fixed/404.md`](content/fixed/404.md). This is useful if you want a custom 404 for your GitHub Page.

### Sidebar Links

To indicate that a given piece of content should be linked in the sidebar, add a key `sidebar` to the front matter, and set it to `true`. See [`about.md`](content/fixed/about.md) for an example of this. Sidebar links currently appear in an arbitrary order; this will be improved in the future. You can pin content to the sidebar regardless of whether it is a post, or if it is fixed.

Note for Jekyll users: In the original Lanyon, any content that had the `page` layout would be added to the sidebar. However, in Lanyon-Hugo, content with the `fixed` type will not be added to the sidebar automatically. You must specify the `sidebar` flag in the front matter.

### Look and Feel

The CSS from the original Lanyon is unchanged, and you can find it in [`static/css`](static/css). Any of the modifications suggested for Lanyon can also be applied to Lanyon-Hugo, by changing the CSS here.

You can use syntax highlighting, if you have [Pygments](http://pygments.org/). See the "example content" post for an example. Lanyon has a color scheme of some kind for Pygments in `css/syntax.css`, but right now Hugo doesn't know how to use it (everything will be higlighted in Monokai). When Hugo implements this feature, I will also add it to Lanyon-Hugo. More detail on Hugo's syntax highlighting shortcode can be found [here](http://hugo.spf13.com/extras/highlighting).

## To Do

While Lanyon-Hugo is aiming for functional compatibility with Lanyon (ie all the old functionality is available and looks similar), there are still some things I'm missing:
- pagination. Lanyon-Hugo does not have next/previous buttons. Jekyll's pagination feature is quite good, but Hugo's pagination is still on the roadmap for now. I may implement a hackish solution in the meantime, but ideally I'd rather wait until Hugo has a solid solution for this problem.
- post lists. Lanyon didn't have a feature for listing posts (my fork of Lanyon implemented one). Hugo has a feature called indexes, which can probably provide this functionality. I intend to make use of it.

## Contributing

If you're interested in hacking on this theme, please check out [CONTRIBUTING](CONTRIBUTING.md).

## License
None for now. Not a big priority for me. But it'll probably be MIT.
