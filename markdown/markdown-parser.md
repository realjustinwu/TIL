# Markdown Parser

Markdown 文本需要经过 markdown parser 的处理才能转成 html，才能被 preview。
不同种类的 markdown parser 提供的功能不一样。因此经常遇到在 VS code 上能 preview 的 markdown，上传到 github pages 之后，达不到预期效果。
比如，`<details><summary>` 里面插入代码，或者使用自定义的 css 等。在不同的 parser 中展示的结果不同。
选择一个自己喜欢的 Parser 很重要。

## Markdown Parser 分类

| Language | Library (download project) |
| - | - |
| Perl | [Original version](http://daringfireball.net/projects/markdown/) |
| JavaScript | [CommonMark](https://github.com/jgm/commonmark.js), [Marked](https://github.com/markedjs/marked), [Markdown-it](https://github.com/markdown-it/markdown-it), [Remarkable](https://github.com/jonschlinkert/remarkable), [Showdown](https://github.com/showdownjs/showdown) |
| Ruby | [Github Flavored Markup(GMF)](https://github.github.com/gfm/), [Kramdown](https://github.com/gettalong/kramdown), [Maruku](https://github.com/bhollis/maruku), [Redcarpet](https://github.com/vmg/redcarpet) |
| PHP | [Cebe Markdown](https://github.com/cebe/markdown), [Ciconia](https://github.com/kzykhys/Ciconia), [Parsedown](https://github.com/erusev/parsedown), [PHP Markdown Extended](https://github.com/piwi/markdown-extended) |
| Python | [Python Markdown](https://pypi.python.org/pypi/Markdown) |

## Markdown 功能

Markdown Parser 都支持的功能包括：Inline HTML, Automatic paragraphs, headers, blockquotes, lists, code blocks, horizontal rules, links, emphasis, inline code and images。
除了这些常规功能，每一个 parser 都支持其他特殊的功能。

- GMF: Fenced Codeblocks, Syntax Highlighting, Tables, URL AutoLinking, To-dos, Strikethrough.
- CommonMark: Fenced Codeblocks, URL AutoLinking
- Multi-markdown: Fenced Codeblocks, Syntax Highlighting, Tables, Metadata, Fragments/Cross References Links, Footnotes, Strikethrough, Definition Lists, Math.

参考：

1. [Link](https://css-tricks.com/choosing-right-markdown-parser/)
