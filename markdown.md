# (WIP) rajayonin's Markdown cheatsheet

Markdown is, in my opinion, just the best text-formatting language. It has a simple and intuitive syntax, making it easy to understand the text structure even as plain text, but also provides great results with just enough formatting for READMEs, notes, instructions, and cheatsheets, such as this one.  
The compiler takes the text in `.md` files and translates it to HTML, so you can even write HTML syntax inside Markdown and it will work!  

For more information, please check [Markdown Guide](https://www.markdownguide.org/). Also, if you'd like to take notes using Markdown, check the [Obsidian](https://obsidian.md/) app.  
  
Note that this guide is for [CommonMark](https://commonmark.org/), the main Markdown flavour, but it is also compatible with [GitHub Flavoured Markdown](https://github.github.com/gfm/).  
A good tool to preview GFM files is [Grip](https://github.com/joeyespo/grip).


## Text formatting
Ways to modify the text itself. All of these can be combined between them.
- **Headings** - `#`, `##`, ...: Creates a heading. The number of number signs indicate the level of the heading, as in HTML (`<h1>`).  
The bigger the number, the smaller the heading.  
    - You can specify a heading ID with by adding `{#<id>}` at the end, but it creates them automatically.
- **Italics** - `_ _`: Makes the text _in italics_.
- **Bold** - `** **`: Makes the text **in bold**.
- **Strikethrough** - `~~ ~~`: Makes the text ~~strikethrough~~.
- **Code** - `` ` ` ``: Makes the text as is, escaping all formatting and giving it a cool `*<{mono font}>*`.
    - To escape backticks, use double backticks on the code formatting:
    ``` `` `code` `` ```.  
    Use three for escaping double backticks, and so on.
- **Equations** - `$ $`: Uses LaTeX markup's `math` enviroment to print out equations. I recommend using the tool [Codelog's Equation Editor](https://www.codecogs.com/latex/eqneditor.php). 
    - use doubles for more complex ones (matrixes, etc)

You can also use regular HTML markings like `<sub></sub>`, `<super></super>` and `<mark></mark>`.
## Structures
The different ways of organizing text.
- **Unordered lists** - `- `: Create bullet point lists.  
    - To create a sub-element, use a tab before the hyphen.
- **Ordered lists** - `1. `: Create numbered lists. The numbers must be put and ordered manually. Can also create sub-elements.
- **Code blocks** - `` ``` ``: Create code blocks to write plaintext in (one at the top and one at the bottom).
    - You can specify a language in order to enable syntax highlighting by adding it next to the top backtics: `` ```lang ``
        ```c
        int main() {
            return 0;
        }
        ```
- **Blockquotes** - `> `:
- **Horizontal rules** - `---`:

## Links
You can create custom links:
```
## Mi long-ass title {#short-title}

As mentioned in [here](#short-title)...
```


## Images


## Others
- **Break line**: In order to use a line break, use double space at the end of the line.
- Emojis: <https://github.com/ikatyang/emoji-cheat-sheet/tree/master#symbols>
