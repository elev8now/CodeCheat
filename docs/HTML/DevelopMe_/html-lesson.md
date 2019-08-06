# HTML - Day 1

Computers take everything you write very literally. We can interpret slurred speech, but computers cannot. Do not add spaces to any files or folders.

## How the internet works

NOT a bubble cloud. The internet is a WIRE. A server is a folder connected to the internet, and a website is a file on that server.

## Languages

### Backend languages

-   PHP
-   Ruby
-   Python
-   Java
-   C (C++, C#)
-   JavaScript

### Front-end languages

-   HTML
-   CSS
-   JavaScript

CSS makes HTML look pretty. JavaScript makes HTML functionally interactive.

## HTML

HTML is data. Based on XML. Stands for Hypertext Markup Language.

## HTML structure

```html
<element attr="param">
	insert content here
</element>
```

### Paragraph element

```html
<p class="paragraph" id="specificParagraph">Paragraph content</p>
```

### Anchor element (or link)

```html
<a href="http://www.google.com">Google</a>
```

### Self closing element tags

```html
<input type="text" name="firstname" />

<img src="" />
```

## File Naming

Always start with index.html. The browser will always look for index.html. That's why it's called index.

When you have a really long !DOCTYPE, it just means the page is an older version of HTML.

Where possible, ALWAYS use semantic elements e.g. section, aside, article.

## Layout

`article` - Generally an article element is used for standalone content

`section` - Generally a section denotes a specific area of the page e.g. some text and images. Used for page layout or to separate areas of the page.

`aside` - Generally used for related content, or a sidebar.

## Special Elements

`button` - NOT to be used as links, just in page behaviour, e.g. close modal, play video

`details` - Details element must contain nested summary element. Creates a summary title with expandable details.

## Head Section

What's included in a HTML head tag?

See this link: <https://github.com/h5bp/html5-boilerplate/blob/master/src/index.html>
