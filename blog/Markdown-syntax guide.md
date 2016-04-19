# Markdown syntax guide and writing on MWeb
<!-- toc -->

- [Markdown syntax guide and writing on MWeb](#markdown-syntax-guide-and-writing-on-mweb)
  - [Philosophy](#philosophy)
  - [Notice](#notice)
  - [Headers](#headers)

- [This is an `<h1>` tag](#this-is-an-h1-tag)
  - [This is an `<h2>` tag](#this-is-an-h2-tag)

- [This is an `<h1>` tag](#this-is-an-h1-tag-1)
  - [This is an `<h2>` tag](#this-is-an-h2-tag-1)
  -           - [This is an `<h6>` tag](#this-is-an-h6-tag)
  - [Emphasis](#emphasis)
  - [Newlines](#newlines)
  - [Lists](#lists)
    - [Unordered](#unordered)
    - [Ordered](#ordered)
    - [Task lists](#task-lists)

  - [Images](#images)
  - [Links](#links)
  - [Blockquotes](#blockquotes)
  - [Inline code](#inline-code)
  - [Multi-line code](#multi-line-code)
  - [Sequence and Flow chart](#sequence-and-flow-chart)
  - [Tables](#tables)
  - [Strikethrough](#strikethrough)
  - [Horizontal Rules](#horizontal-rules)
  - [MathJax](#mathjax)
  - [Footnote](#footnote)
  - [Comment And Read More..](#comment-and-read-more)
<!-- tocstop -->

## Philosophy
> Markdown is intended to be as easy-to-read and easy-to-write as is feasible. Readability, however, is emphasized above all else. A Markdown-formatted document should be publishable as-is, as plain text, without looking like it's been marked up with tags or formatting instructions. Markdown's syntax is intended for one purpose: to be used as a format for _writing_ for the web.
<!-- more -->

## Notice
You can use  `CMD + R` to preview the result.

## Headers
**Example:**

# This is an `<h1>` tag
## This is an `<h2>` tag
**Result:**

# This is an `<h1>` tag
## This is an `<h2>` tag
### This is an `<h6>` tag
## Emphasis
**Example:**

```
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

*You **can** combine them*
```

**Shortcuts:**  `CMD + U`、`CMD + I`、`CMD + B` **Result:**

_This text will be italic_ _This will also be italic_

**This text will be bold** **This will also be bold**

_You **can** combine them_

## Newlines
End a line with two or more spaces + enter. Just typing enter to newline,please set：`Preferences` - `Themes` - `Translate newlines to <br> tags`  enable ( default is enable )

## Lists
### Unordered
**Example:**

```
* Item 1 unordered list `* + SPACE`
* Item 2
    * Item 2a unordered list `* + TAB + SPACE`
    * Item 2b
```

**Shortcuts:**  `Option + U` **Result:**
- Item 1 unordered list `* + SPACE`
- Item 2
  - Item 2a unordered list `* + TAB + SPACE`
  - Item 2b

### Ordered
**Example:**

```
1. Item 1 ordered list `Number + . + SPACE`
2. Item 2
3. Item 3
    1. Item 3a ordered list `Number + . + TAB + SPACE`
    2. Item 3b
```

**Result:**
1. Item 1 ordered list `Number + . + SPACE`
2. Item 2
3. Item 3
  1. Item 3a ordered list `Number + . + TAB + SPACE`
  2. Item 3b

### Task lists
**Example:**

```
- [ ] task one not finish `- + SPACE + [ ]`
- [x] task two finished `- + SPACE + [x]`
```

**Result:**
- [ ] task one not finish `- + SPACE + [ ]`
- [x] task two finished `- + SPACE + [x]`

## Images
**Example:**

```
![GitHub set up](https://help.github.com/assets/images/site/set-up-git.gif)
Format: ![Alt Text](url)
```

**Shortcuts:**  `Control + Shift + I` The Library's document support drag & drop or `CMD + V` paste or `CMD + Option + I` to insert  the pictrue. **Result:**

![GitHub set up](https://help.github.com/assets/images/site/set-up-git.gif)

## Links
**Example:**

```
email <example@example.com>
[GitHub](http://github.com)
autolink  <http://www.github.com/>
```

**Shortcuts:**  `Control + Shift + L` The Library's document support drag & drop or `CMD + Option + I` to insert attachment. **Result:**

An email [example@example.com](mailto:example@example.com) link. [GitHub](http://github.com) Automatic linking for URLs Any URL (like [http://www.github.com/](http://www.github.com/)) will be automatically converted into a clickable link.

## Blockquotes
**Example:**

```
As Kanye West said:
> We're living the future so
> the present is our past.
```

**Shortcuts:**  `Control + B` **Result:**

As Kanye West said:

> We're living the future so the present is our past.

## Inline code
**Example:**

```
I think you should use an
`<addr>` `code` element here instead.
```

**Shortcuts:**  `CMD + K` **Result:**

I think you should use an `<addr>` `code` element here instead.

## Multi-line code
**Example:**

````
```js
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }

}
```
````

**Shortcuts:**  `CMD + Shift + K` **Result:**

```js
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }

}
```

## Sequence and Flow chart
**Example:**

````
```sequence
张三->李四: 嘿，小四儿, 写博客了没?
Note right of 李四: 李四愣了一下，说：
李四-->张三: 忙得吐血，哪有时间写。
```

```flow
st=>start: 开始
e=>end: 结束
op=>operation: 我的操作
cond=>condition: 确认？

st->op->cond
cond(yes)->e
cond(no)->op
```
````

**Result:** ( Please enable  `Preferences` - `Themes` - `Enable sequence & flow chart`, default is enable. )

```sequence
张三->李四: 嘿，小四儿, 写博客了没?
Note right of 李四: 李四愣了一下，说：
李四-->张三: 忙得吐血，哪有时间写。
```

```flow
st=>start: 开始
e=>end: 结束
op=>operation: 我的操作
cond=>condition: 确认？

st->op->cond
cond(yes)->e
cond(no)->op
```

More info: [http://bramp.github.io/js-sequence-diagrams/](http://bramp.github.io/js-sequence-diagrams/), [http://adrai.github.io/flowchart.js/](http://adrai.github.io/flowchart.js/)

## Tables
**Example:**

```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

You can create tables by assembling a list of words and dividing them with hyphens - (for the first row), and then separating each column with a pipe |:

**Result:**

First Header                | Second Header
--------------------------- | ----------------------------
Content from cell 1         | Content from cell 2
Content in the first column | Content in the second column

## Strikethrough
**Example:**

```
 (like ~~this~~)
```

**Result:**

Any word wrapped with two tildes (like ~~this~~) will appear crossed out.

## Horizontal Rules
Following lines will produce a horizontal rule:

```
***

*****

- - -
```

**Result:**

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------

## MathJax
Use double US dollors sign pair for Block level Math formula, and one US dollor sign pair for Inline Level.

```
For example this is a Block level $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$ formula, and this is an inline Level $x = {-b \pm \sqrt{b^2-4ac} \over 2a}$ formula.

\\[ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } } \\]
```

**Result:**

For example this is a Block level

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$

formula, and this is an inline Level $x = {-b \pm \sqrt{b^2-4ac} \over 2a}$ formula.

\[ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} = 1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}} {1+\frac{e^{-8\pi}} {1+\ldots} } } } \]

## Footnote
**Example:**

```
This is a footnote:[^sample_footnote]
```

Header One | Header Two
:--------- | :---------
Item One   | Item Two

**Result:**

This is a footnote:[^sample_footnote]

[^sample_footnote]: footnote text detail...

## Comment And Read More..
<!-- comment --> <!-- more --> Actions->Insert Read More Comment _OR_ `CMD + .`