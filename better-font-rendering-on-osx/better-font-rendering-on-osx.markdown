---
date: 2013-08-10
---
# Better font-rendering on OSX

The two main factors which define how fonts will look on displays are their hinting and the operating system’s rendering algorithm. Therefore trying different fonts on different devices, operating systems, browsers and browser versions is the only way to get an idea how they will be presented to users.

Photoshop doesn’t use the system’s font rendering so that text looks very differently. One could use [Sketch](http://www.bohemiancoding.com/sketch/) as an alternative, but it’s best to design in the medium itself—the browser. Style guides or new tools like [Typecast](http://typecast.com/) and [Macaw](http://macaw.co/) are great for a responsive workflow.

## Font rendering on OS X

Due to its sub-pixel antialiasing algorithm OS X tends to render light text on dark backgrounds too bold. Using icon fonts sometimes leads to [blurry](http://people.mozilla.org/~jdaggett/tests/social-waterfall.html) rendering.

Fortunately developers can influence how browsers render text on OS X. Webkit/Chromium-based browsers offer `-webkit-font-smoothing` and  Firefox [recently added](https://bugzilla.mozilla.org/show_bug.cgi?id=857142) `-moz-osx-font-smoothing` to version 25.

These properties switch the rendering algorithm to grayscaling, which will result in a thinner and sharper appearance of fonts. As both are non-standard I’ve created a simple mixin to normalize the syntax differences.

### Mixin

```scss
@mixin font-smoothing($value: on) {
    @if $value == on {
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }
    @else {
        -webkit-font-smoothing: subpixel-antialiased;
        -moz-osx-font-smoothing: auto;
    }
}
```

### Usage

```scss
.dark-on-light {
    @include font-smoothing(off);
}

.light-on-dark {
    @include font-smoothing(on);
}
```

My website also uses these properties for better rendering. Keep in mind that these properties should be used as a solution and [not in general](http://www.usabilitypost.com/2012/11/05/stop-fixing-font-smoothing) as it may lead to worse results.

__Update:__ `-moz-osx-font-smoothing` is now supported in stable Firefox.
