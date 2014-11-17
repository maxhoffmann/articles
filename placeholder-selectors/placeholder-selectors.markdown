---
date: 2013-02-14
---
# Placeholder Selectors

Introduced with Sass 3.2 placeholder selectors enable us to write better modular <abbr>CSS</abbr> by extending classes, which won’t be included in the compiled file. The main advantage of using placeholder selectors is the reduction of classes in your <abbr>HTML</abbr> __and__ <abbr>CSS</abbr>.

## Plain CSS

Let’s assume we want to implement a website, which has tiles with different colors. Each tile has the same width, height and margin.

```scss
.tile {
  width: 200px;
  height: 200px;
  margin-right: 20px;
}
```

For the ability to add different colors to the tiles we included two theme classes in our <abbr>CSS</abbr>.

```scss
.tile-blue {
  background-color: blue;
}
.tile-red {
  background-color: red;
}
```

The corresponding markup could look like this:

```markup
<div class="tile tile-blue"></div>
<div class="tile tile-red"></div>
```

## Without Placeholder Selectors

We’ve added two classes to the tile element: one for basic tile styles and one for the color. To reduce the number of classes we could simply extend `.tile` and remove it from our <abbr>HTML</abbr>.

```scss
.tile {
  width: 200px;
  height: 200px;
  margin-right: 20px;
}
.tile-blue {
  @extend .tile;
  background-color: blue;
}
.tile-red {
  @extend .tile;
  background-color: red;
}
```

Although we wouldn’t have to use the `.tile` class in our markup anymore, it would still be in our compiled <abbr>CSS</abbr>:

```scss
.tile, .tile-blue, .tile-red {
  width: 200px;
  height: 200px;
  margin-right: 20px;
}
```

To save some bytes or to prevent other developers from using the basic tile class without a color, we could also remove it from the compiled <abbr>CSS</abbr>.

## Using Placeholder Selectors

Changing the dot before a class to a percent sign tells Sass to use it as a placeholder class.

```scss
%tile {
  width: 200px;
  height: 200px;
  margin-right: 20px;
}
.tile-blue {
  @extend %tile;
  background-color: blue;
}
.tile-red {
  @extend %tile;
  background-color: red;
}
```

Now we just need to use our theme classes.

```markup
<div class="tile-red"></div>
<div class="tile-blue"></div>
```

And our compiled <abbr>CSS</abbr> doesn’t contain the basic tile class anymore.

```scss
.tile-blue, .tile-red {
  width: 200px;
  height: 200px;
  margin-right: 20px;
}
.tile-blue {
  background-color: blue;
}
.tile-red {
  background-color: red;
}
```

To sum up placeholder classes are not included in your compiled <abbr>CSS</abbr> so that you can prevent developers from using those classes in their <abbr>HTML</abbr>. It is also possible to build a framework solely out of placeholder classes, which will only be added to the compiled <abbr>CSS</abbr> if developers extend them.

## Further Reading

[Sass Reference: Placeholder Selectors](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#placeholder_selectors_)
