# Horizon Website

Our new website is powered using a tool called `jekyll`. Jekyll is a static-site generator. Basically, Jekyll allows us to create templates for the style and layout of posts. Then, we write our articles/perspectives in an easy-to-write format. Jekyll takes the templates, inserts the text in the correct place, and generates an entire website, eliminating the need for any over-engineered solutions. Because we operate on a template-based system, it's very easy to change the styling of the website or the hierarchical layout. 

## Adding Posts

Posts go in the `_posts/` directory. The general file naming convention is `YYYY-MM-DD-title-with-dashes.md`. Use the `2018-09-10-test.md` file as a template. The code between the dashed lines is the metadata for the post, given in key-value pairs. Some of the important keys are:

- `layout`, which tells Jekyll how to render the post. Should usually be `post`.
- `title`, which is the full title of the article/perspective. 
- `author`, which should include the author's name and year of graduation

### Excerpts

The website also has a space for a short (~ 25 words) description of the post to let readers know what the high-level subject matter is. To denote the end of the excerpt and the beginning of the post, add in a `<!--excerpt-->` line.

### Post Components

The majority of the post will most likely be plain text prose, written in Markdown. For regular text, you can use a plain text editor and type normally. The font type and size will be taken care of for you. Hit enter a few times to start a new paragraph.

If italics are needed, wrap the text to be italicized in underscores or asterisks (e.g. `_italic text_`). If bold is needed, wrap the text in double asterisks (e.g. `**bold text**`). Links follow the format `[display text](https://website.com)`. Images have the format `![back up text](https://website.com/image.png)`. Numbered lists will be automatically formatted, and bulleted lists can be written in plain text using a dash (`-`) for each bullet. Nested lists are also taken care of automatically.

A heading for a section can be formatted as `# Heading`. For a smaller font size, add more `#` characters to the beginning. Each subsequent `#` makes the font smaller. Remember that the title is already taken care of in the metadata.

Both Jekyll and Markdown are very popular tools, so more information about how to use both can be found easily online. Now, for Horizon specific components

### Horizon-Specific Features

Figures are important for presenting sound scientific research. We will use tables to show an image as well as a caption. 

```
| ![](/imgs/image-name.EXT) | 
|:--:| 
| **Figure**. Caption (Citation) |
```

This is a standard markdown table, so data tables can also be shown quite easily.

Math might sometimes appear in posts. We use MathJax, which is a popular tool for rendering math in browser. For inline math, use the standard LaTeX `$a+b=c$` type formatting. Otherwise, use double dollar signs. 