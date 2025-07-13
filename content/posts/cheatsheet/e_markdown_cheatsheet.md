+++
title = 'Extended markdown cheatsheet with KaTeX'
date = 2023-11-25T09:46:19+05:30
draft = false
tags = ["markdown", "cheatsheet", "katex", "latex", "math"]
author = "Aum Pauskar"
description = "A basic cheatsheet of markdown with KaTeX"
+++

# Extended Markdown Cheatsheet

## Heading
```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

## Paragraph
```markdown
This is a paragraph.
```

## Code snippet
```markdown
'print("Hello World")'
```

block of code
```markdown
'''
print("Hello World")
'''
```

code within the clock of code can be selectively highlighted
```markdown
'''python
print("Hello World")
'''
```

## Emphasis
```markdown
*This text will be italic*
_This will also be italic_
**This text will be bold**
__This will also be bold__
_You **can** combine them_
```

## Table
```markdown
| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |
```

## Bulletpoints
```markdown
- Bulletpoint 1
- Bulletpoint 2
	- Bulletpoint 2.1
	- Bulletpoint 2.2
```

or

```markdown
* Bulletpoint 1
* Bulletpoint 2
	* Bulletpoint 2.1
	* Bulletpoint 2.2
```

## Numbered list
```markdown
1. Numbered item 1
2. Numbered item 2
3. Numbered item 3
	1. Numbered item 3.1
	2. Numbered item 3.2
```

or
```markdown
1. Numbered item 1
1. Numbered item 2
1. Numbered item 3
	1. Numbered item 3.1
	1. Numbered item 3.2
```
Note that this will be rendered as normal numbered list when rendered.

## Blockquotes
```markdown
> Blockquote
```

## Horizontal rule
```markdown
---
```

## Link
```markdown
[Link](https://www.google.com)
```

## Image
```markdown
![Image](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)
```

## KATeX
KATeX is a math rendering engine that can be used to render math equations in markdown. It is supported by Github and Gitlab. It is not supported by Bitbucket.

```markdown
Inline math: $x^2$
```

```markdown
Block math:
$$ x^2 $$
```
This will be rendered when ran in a proper renderer. \
[All formulas](https://katex.org/docs/supported.html)