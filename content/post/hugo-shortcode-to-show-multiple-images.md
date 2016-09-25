+++
date = "2016-09-25T14:15:30+01:00"
description = "Using Pure CSS Unit Classes"
draft = false
tags = ["hugo", "purecss", "theme", "golang"]
title = "Hugo Shortcode to Show Multiple Images"
topics = ["Techy Stuff"]

+++

I have created a new Hugo [shortcode](https://gohugo.io/extras/shortcodes/) (`fluid_imgs`) that makes it easy to display multiple images in your content files, for example:

{{< fluid_imgs
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
>}}

<!--more-->

### Background

My original `fluid_img` shortcode is limited in that it can only display one image at a time. This means you have to repeat the same shortcode to display more than one image, which is rather inconvenient. `fluid_imgs` improves this. 

### Code

It is not part of my [Blackburn theme](https://github.com/yoshiharuyamashita/blackburn) yet but I will add it once I am happy with it.

```html
{{ $paramCount := len .Params }}
{{ if gt $paramCount 0 }}
<div class="pure-g">
{{ range $param := .Params }}
  {{ $items := split $param "|" }}
  {{ $itemCount := len $items }}
  <!-- Item count must be at least 2 as
  "class" and "src" must be specified -->
  {{ if ge $itemCount 2 }}
  <div class="{{ index $items 0 }}">
    <div style="padding: 0 .2em">
      <img
        class="pure-img-responsive"
        src="{{ index $items 1 }}"
        alt="{{ if ge $itemCount 3 }}{{ index $items 2 }}{{ else }}{{ "" }}{{ end }}">
    </div>
  </div>
  {{ end }}
{{ end }}
</div>
{{ end }}
```

### Usage

The content of the shortcode in your markup file is very simple:


\{\{< fluid_imgs
```html
  "class|src|alt"
  "class|src|alt"
  "... and so on"
```
\>\}}

where each positional parameter is separated by the vertical bar (i.e., |).

- `class`: specifies a Pure CSS unit class name (**required**)
- `src`: specifies the URL of an image (**required**)
- `alt`: specifies an alternate text for an image (optional)

*The shortcode uses positional parameters so the order is important. The first two parameters must be specified in that order. Also see [the official Pure CSS site](http://purecss.io/grids/) for valid unit class names.*

### Example output

3 Images with `pure-u-1-3`:

{{< fluid_imgs
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
>}}

2 Images with `pure-u-1-2`:

{{< fluid_imgs
  "pure-u-1-2|/img/post/dog.jpg|Dog"
  "pure-u-1-2|/img/post/dog.jpg|Dog"
>}}

6 Images with `pure-u-1-3`:

{{< fluid_imgs
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
  "pure-u-1-3|/img/post/dog.jpg|Dog"
>}}

1 image with `pure-u-1-1`:

{{< fluid_imgs
  "pure-u-1-1|/img/post/dog.jpg|Dog"
>}}

### Known Problems

- When used with different units, the resulting output is less aesthetically pleasing. In the following example I am using 1 image with `pure-u-1-2` and 3 with `pure-u-1-6`:

{{< fluid_imgs
  "pure-u-1-6|/img/post/dog.jpg|Dog"
  "pure-u-1-2|/img/post/dog.jpg|Dog"
  "pure-u-1-6|/img/post/dog.jpg|Dog"
  "pure-u-1-6|/img/post/dog.jpg|Dog"
>}}

- Including the vertical bar in any parameters will break the shortcode. For example if you specified `Apple|Orange|Banana` for `alt`, it would be set to `Apple`.

### To Dos

- Experiment to use named parameters instead of positional ones (but bear in mind the latter might be better as it would involve less typing for the user).
- Allow the user to configure the padding setting, which is currently hard-coded as `padding: 0 .2em` within the shortcode.