# Docup

## Introduction

Docup is a single script that you can use to create a beautiful one-page documentation without build process.

The idea is inspired by my another project ([Docute](https://docute.js.org)) which in turn is inspired by [Flatdoc](http://ricostacruz.com/flatdoc/). And the design is inspired by [tj (TJ Holowaychuk)](https://github.com/tj)'s wonderful docs for [Apex Up](https://up.docs.apex.sh).

## Usage

Create an HTML file: `index.html` which will be be homepage of your documentation website:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0" />
  <title>My Awesome Doc</title>
  <!-- Stylesheet -->
  <link rel="stylesheet" href="https://unpkg.com/@egojump/docup/dist/docup.css">
</head>
<body>
  <div id="app"></div>
  <!-- Script -->
  <script src="https://unpkg.com/@egojump/docup/dist/docup.js"></script>
  <!-- Start app -->
  <script>
    var doc = new Docup()
    doc.start('#app')
  </script>
</body>
</html>
```

Then populate a `README.md` file to the same directory where `index.html` is located.

```md
# My Project

## Introduction

How about this.

## Advanced

How about that.
```

Finally serve this directory as a static website:

- node.js: `npm i -g serve` && `serve ./docs`
- python: `cd ./docs` && `python -m SimpleHTTPServer`
- golang: `cd ./docs` && `caddy`
- ...etc, you can use any static file server, for real.

## Conventions

### Site Title

We use the value of `h1` title as the site title.

### Message Blocks

To highlight some messages in your documentation, use the following format to write a `blockquote`:

```md
> __Alert__: This is a very dangerous action!
```

On GitHub it will be rendered as follows:

![2017-12-01 1 22 20](https://user-images.githubusercontent.com/8784712/33468930-b835cb64-d69a-11e7-8ab2-25585d61915d.png)

And with Docup it renders:

> __Alert__: This is a very dangerous action!

We also support other message types which are:

```md
> __Info__: This is a info!

<!-- -->

> __Warning__: This is a warning!

<!-- -->

> __Success__: This is ok!

<!-- -->

> __Note__: This is just a note!
```

> __Warning__: Notice the `<!-- -->` here, we use it to write multiple blockquotes in sequence without them being merged into one blockquote. It's unnecessary if you only have one blockquote.

And they look like:

> __Info__: This is a info!

<!-- -->

> __Warning__: This is a warning!

<!-- -->

> __Success__: This is ok!

<!-- -->

> __Note__: This is just a note!

## Deploy

### GitHub Pages

Simply put all your files in `docs` folder on `master` branch, or root directory on the `gh-pages` branch.

Don't forget to add `.nojekyll` file to tell GitHub to treat it as a normal static website.

## API

### Constructor

```js
const doc = new Docup(options)
```

#### options

##### indexFile

Type: `string`<br>
Default: `README.md`

##### root

Type: `string`<br>
Default: `./`

##### highlight

Type: `boolean` `function`<br>
Default: `true`

Whether to highlight code blocks, you can supply a function to customize this:

```js
function highlight(code, lang) {}
```

##### highlightFirstParagraph

Type: `boolean`<br>
Default: `false`

Highlight the first paragraph after `h2` titles. Basically this option enables following CSS:

```css
h2 + p {
  font-size: 1.6rem;
  line-height: 1.6;
}
```

#### doc.start(target)

##### target

Type: `string` `HTMLElement`

The place to mount app to.

## Roadmap

### Browser support

I will add support for IE10+ very soon.

### Prerender

Prerender `index.html`

### Multi-route support

Maybe, maybe not.

## License

MIT &copy; EGOIST
