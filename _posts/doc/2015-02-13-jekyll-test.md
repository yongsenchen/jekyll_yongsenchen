---
layout: post
category : doc
tags : [jekyll, github]
---

Test Scripts from https://guides.github.com/features/mastering-markdown/

## Syntax

### Headers

#### This is an h4 tag
##### This is an h5 tag
###### This is an h6 tag


### Emphasis

*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

*You **can** combine them*

### Lists

#### Unordered

* Item 1
* Item 2
  * Item 2a
  * Item 2b

#### Ordered

1. Item 1
2. Item 2
3. Item 3
   * Item 3a
   * Item 3b

### Images

![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)

### Links

http://github.com - automatic!
[GitHub](http://github.com)

### Blockquotes

As Kanye West said:

> We're living the future so
> the present is our past.
Inline code

I think you should use an
`<addr>` element here instead.


### Syntax highlighting

#### Just tab

	int add(int a, int b)
	{
		return a + b;
	}

#### use c

```c
int add(int a, int b)
{
	return a + b;
}
```

#### use c

~~~c
int add(int a, int b)
{
	return a + b;
}
~~~

#### use highligt

{% highlight c %}
int add(int a, int b)
{
	return a + b;
}
{% endhighlight %}

### Task Lists

- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item

### Tables

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

### SHA references

16c999e8c71134401a78d4d46435517b2271d6ac

mojombo@16c999e8c71134401a78d4d46435517b2271d6ac

mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac

### Issue references within a repository

#1

mojombo#1

mojombo/github-flavored-markdown#1

### Username @mentions

@yongsenchen

### Automatic linking for URLs

Any URL (like http://www.github.com/) will be automatically converted into a clickable link.

### Strikethrough

Any word wrapped with two tildes (like ~~this~~) will appear crossed out.

### Emoji

GitHub supports emoji! :sparkles: :camel: :boom:

To see a list of every image we support, check out the Emoji Cheat Sheet.

## Examples

### Text

It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Google!](http://google.com)

### Lists

Sometimes you want numbered lists:

1. One
2. Two
3. Three

Sometimes you want bullet points:

* Start a line with a star
* Profit!

Alternatively,

- Dashes work just as well
- And if you have sub points, put two spaces before the dash or star:
  - Like this
  - And this

### Images

If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)

### Headers & Quotes

# Structured documents

Sometimes it's useful to have different levels of headings to structure your documents. Start lines with a `#` to create headings. Multiple `##` in a row denote smaller heading sizes.

### This is a third-tier heading

You can use  one `#` all the way up to `######` six for different heading sizes.

If you'd like to quote someone, use the > character before the line:

> Coffee. The finest organic suspension ever devised... I beat the Borg with it.
> - Captain Janeway

### Code

There are many different ways to style code with GitHub's markdown. If you have inline code blocks, wrap them in backticks: `var example = true`.  If you've got a longer block of code, you can indent with four spaces:

    if (isAwesome){
      return true
    }

GitHub also supports something called code fencing, which allows for multiple lines without indentation:

```
if (isAwesome){
  return true
}
```

And if you'd like to use syntax highlighting, include the language:

```javascript
if (isAwesome){
  return true
}
```

### Extras

GitHub supports many extras in Markdown that help you reference and link to people. If you ever want to direct a comment at someone, you can prefix their name with an @ symbol: Hey @kneath — love your sweater!

But I have to admit, tasks lists are my favorite:

- [x] This is a complete item
- [ ] This is an incomplete item

And, of course emoji! :sparkles: :camel: :boom:
