---
date: 2012-12-09
---
# Mobile First

I have been familiar with mobile first and its advantages for a long time, but my blog’s latest iteration is the first site which actually uses this approach. First I had started implementing the new design desktop first and added mobile styles later via media queries, but after having seen Brad Frost’s inspiring talk [“Beyond Media Queries”](https://vimeo.com/55076713) I have finally changed my mind and wrote the <abbr>CSS</abbr> from scratch, which was the best decision I could make.

My styles are smaller in file size, easier to maintain and flexible like never before. Additionally I have started my own small Sass framework full of useful components and mixins, which faciliates things like using ems instead of pixels and includes my new way of laying out elements on a page. This “new” way has a lot in common with grids as it uses floats, but I think it is superior to most grids, because of its missing row divs and its mobile first approach.

## Reverse Engineering

I started with looking at the new design based on my old desktop first approach and reverse engineered the grid. The first thing I recognized is that most designs on mobile devices have centered elements, so I wrote a placeholder class, which were introduced in Sass 3.2, to center elements:

```scss
%centered {
  margin-left: auto;
  margin-right: auto;
}
```

Next I added a `.container` class to give elements some horizontal space.

```scss
.container {
  @extend %centered;
  width: 88%;
  max-width: 64em;
}
```

Notice `max-width` limiting the width of my site to `1024px`, which fits best for my design, but you could change the value to your needs or omit it completely.

Now it’s time to add columns, which will later lay out as a grid on wider screens. On mobile devices these again look like centered boxes.

```scss
.col {
  @extend %centered;
  max-width: 30em;
}
```

This time `max-width` prevents columns of enlarging too wide, so that their content is good to read on tablet devices. These classes are enough to give your site a basic and readable layout for most mobile and tablet devices. Browsers without media queries like <abbr>IE8</abbr> and below render the page fine as columns are never too wide for their content and centered by default.

## Applying the grid

The actual grid is wrapped in a media query. The following styles are inside this query:

```scss
@media (min-width: 48em) {
  /* styles */
}
```

For viewport sizes wider than `767px` columns will float and form the grid.

```scss
.col {
  float: left;
  overflow: hidden;
  max-width: none;
}
.col.right {
  float: right;
}
```

Columns are floated left by default, but may be floated to the right by adding `.right`. Overflowing content is hidden and `max-width` is reset allowing columns to use more space depending on their size class.

You could add a lot of grid sizes to define a flexible 12-column grid, but for my purposes I’ve chosen the following sizes as my grid may have nested columns to further split up columns.

```scss
/* col sizes */
.full { width: 100%; }
.half { width: 50%;  }

.third      { width: 33.33%; }
.two-thirds { width: 66.66%; }

/* golden ratio */
.gold-big   { width: 61.8%; }
.gold-small { width: 38.2%; }

.quarter        { width: 25%; }
.three-quarters { width: 75% }
```

Like in [Bootstrap](http://getbootstrap.com) I have added space classes to avoid the usage of empty columns for layout purposes.

```scss
/* space sizes */
.space-half { margin-left: 50%; }

.space-third      { margin-left: 33.33%; }
.space-two-thirds { margin-left: 66.66%; }

.space-gold-big   { margin-left: 61.8%; }
.space-gold-small { margin-left: 38.2%; }

.space-quarter        { margin-left: 25%; }
.space-three-quarters { margin-left: 25%; }
```

The last thing we need is a class to start a new row if columns don’t add up to 100%.

```scss
.new-row {
  clear: both;
}
```

The advantage of starting rows by just adding a class to an element is its flexibility. You can remove and add this class to different elements on different viewport sizes via JavaScript and change the site’s layout with ease.

This is my small insight into my blog’s foundation. You can take a look at the full code in my [Sass framework](https://github.com/maxhoffmann/sass-framework/blob/master/components/grid.scss) repository. For vertical spacing I have added default padding-bottom of `24px` to `.col` and wrote some generic space classes, but those are different in every project that’s why I have left them out of my grid component.

_Note:_ This is my first article written in English and I’m really thankful for feedback and critique.
