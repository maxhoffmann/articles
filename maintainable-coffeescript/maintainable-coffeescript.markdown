---
date: 2013-08-08
---
# Maintainable CoffeeScript

__Update:__ I didn’t switch to CoffeeScript. Blog post may follow soon.

In 2012 I decided to master JavaScript. I started with Addy Osmani’s free ["Learning JavaScript Design Patterns"](http://addyosmani.com/resources/essentialjsdesignpatterns/book/), read ["JavaScript: The Good Parts"](http://shop.oreilly.com/product/9780596517748.do) by Douglas Crockford, then went on with ["Effective JavaScript"](http://effectivejs.com) by David Herman, learned about ["Maintainable JavaScript"](http://shop.oreilly.com/product/0636920025245.do) from Nicholas Zakas and am currently half through ["Secrets of the JavaScript Ninja"](http://jsninja.com/) by John Resig and Bear Bibeault. I also had a glimpse into ["Eloquent JavaScript"](http://eloquentjavascript.net/) by Marijn Haverbeke and ["Object Oriented JavaScript"](http://www.packtpub.com/object-oriented-javascript/book) by Stoyan Stefanov. Each one of these books is a fantastic resource and helped me enormously to enhance my JavaScript knowledge. I already have another book on my reading list: ["Test-Driven JavaScript Development"](http://tddjs.com/) by Christian Johansen.

While learning to avoid the quirks of JavaScript I started to value its good parts and then felt in love with the expressiveness of the language. Having written some web applications without and with frameworks like [Angular.js](http://angularjs.org), I got aware of the boilerplate code one has to write though. Class inheritance is pretty painful without a library and some things like type or existence checking isn’t fun.

Fortunately the next version of ECMAScript has evolved to a very powerful and beautiful standard, which will definitely have a huge influence on how we write JavaScript. Combined with Web Components web site and application development will be very different in one or two years—hopefully sooner than later.

Until the standard has been implemented in most browsers we can use _compile-to-javascript_ languages like [CoffeeScript](http://coffeescript.org/), which allow us to use some of the ES6 features today. I’ve looked into CoffeeScript before, but I never felt that I was ready for it. I had to learn JavaScript first. This week I stumbled again on CoffeeScript when [these slides](http://aseemk.com/talks/intro-to-coffeescript) by Aseem Kishore made the round on twitter. CoffeeScript itself influenced the new standard and provides some syntactical improvements. I have been playing around with it lately and really like to use arrow functions, class inheritance and splats today, but I think CoffeeScript is too lax when it comes to omitting braces and keywords. Maybe this is just because I’m not used to read it, but as I use CoffeeScript just in the interim until ES6 is useable I defined some conventions I want to share. These should make it easier to read and maintain the code especially for JS developers without a lot of CoffeeScript experience (myself included). On CoffeeScript’s website it says: _“The golden rule of CoffeeScript is: It’s just JavaScript.”_ My conventions try to make CoffeeScript’s syntax more like JavaScript.

## Code Conventions

## 1. always wrap function parameters in parentheses

Readability is important. Without parentheses it’s hard to see where functions are called—even for syntax highlighters like [prism.js](http://prismjs.com/). It’s also inconsistent as one has to use parantheses calling functions without parameters.

### without parentheses

```coffeescript
request = new XMLHttpRequest
  request.responseType = type
  request.onload = handleResponse
  request.open method, url, true
  request.setRequestHeader 'X-Requested-With', 'XMLHttpRequest'
  request.send()
```

### with parentheses

```coffeescript
request = new XMLHttpRequest()
  request.responseType = type
  request.onload = handleResponse
  request.open(method, url, true)
  request.setRequestHeader('X-Requested-With', 'XMLHttpRequest')
  request.send()
```

Now you can see on the first sight which parts of the code are assignments and which ones are function calls.

## 2. always write return if you intend to do so

CoffeeScript always returns the last statement of a function. This leads to lines with just a variable name, but lines with just a variable name could also be part of an array for example. It’s also not explicit if you return early. Look at the last line. In my opinion it looks unintentional.

### without return

```coffeescript
getVar = (para) ->
  context = this or window
  if not /^\'/g.test(para)
    return context[para]
  para
```

### with return

```coffeescript
getVar = (para) ->
  context = this or window
  if not /^\'/g.test(para)
    return context[para]
  return para
```

## 3. wrap functions which are not the last argument in parentheses

Without parantheses and the return statement this looks like a syntax error to me. Apparently this is also hard to understand for CoffeeScript’s compiler as this syntax isn’t valid when compiled with the new [CoffeeScript Redux compiler](http://michaelficarra.github.io/CoffeeScriptRedux/). The Redux compiler is also smart enough not to wrap the function in parentheses when compiled.

### without parentheses

```coffeescript
func = string.split('.').reduce (obj,i) ->
  obj[i] or false
, obj
```


### with parentheses

```coffeescript
func = string.split('.').reduce( ((obj,i) ->
    return obj[i] or false
), obj)
```


## 4. wrap objects in curly braces

This again fights inconsistency. Arrays have to be wrapped in braces so should objects.

### without braces

```coffeescript
obj =
  name: 'Max'
  age: 23
  likes: [
    'javascript'
    'es6'
    'code conventions'
  ]
  hobbies:
    sport: 'fitness'
    music: 'piano'
    other: 'web development'
  from: 'germany'
```


### with braces

```coffeescript
obj = {
  name: 'Max'
  age: 23
  likes: [
    'javascript'
    'es6'
    'code conventions'
  ]
  hobbies: {
    sport: 'fitness'
    music: 'piano'
    other: 'web development'
  }
  from: 'germany'
}
```

## Why should I use more parentheses?

CoffeeScript allows me to write JavaScript with some of ES6’s features today and JavaScript’s syntax has parentheses. I still want to write JavaScript and when ES6 is out I’ll switch back. I also think that omitting everything CoffeeScript allows is more error-prone and not good for maintainability. Another factor is readability, which suffers from a too lax syntax. Brendan Eich proposed a [syntax for ES6](http://brendaneich.com/2010/11/paren-free/) with less parentheses for conditions and loops, which combines the advantages of both styles in my opinion.

If you want to write CoffeeScript, learn JavaScript first. For beginners I recommend ["Effective JavaScript"](http://addyosmani.com/resources/essentialjsdesignpatterns/book/). Afterwards read ["Secrets of the JavaScript Ninja"](http://jsninja.com/) and the most important thing: write JavaScript—a lot. If you feel that you are ready to move on take a look at CoffeeScript’s documentation __and__ at real world code. The example pseudo code is far away from the code you’ll write. Real CoffeeScript looks more like [this](https://github.com/heelhook/chardin.js/blob/master/chardinjs.coffee). If you have learned JavaScript properly the transition to CoffeeScript will be quick and easy.

I can not wait for the next version of JavaScript and CoffeeScript is a foretaste of what’s to come. ECMAScript.next has powerful features like modules, Proxies, Weakmaps etc. which will make JavaScript more beaufitul and powerful than ever before.

## Further Reading

- [Short summary of ECMAScript 6](http://espadrine.github.io/New-In-A-Spec/es6/)
- [[Video] David Herman: The Future of JavaScript](http://www.youtube.com/watch?v=u4IdoBU1uKE)
