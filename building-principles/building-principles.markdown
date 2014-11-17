---
date: 2013-02-12
---
# Building Principles

During my internship I have realized that most of my decisions while building websites or web applications are based on three essential principles. Most of them have developed by reading articles and books so you are probably familiar with them, but additionally I want to give some examples where those influence my opinion about certain solutions.

## 1. Content First
The main reason people visit your website or use your web application is because they want to consume its content. Therefore every distraction should be eliminated.

You probably know that advertisment before, inside or overlaying your content is a distraction, but this principle is also the reason why I think navigations shouldn’t have a fixed position. People should see navigations when they want to navigate and shouldn’t when they want to read an article or watch a video. Don’t hide your content behind navigational elements.

## 2. Progressive Enhancement
As content is the most important part of your website, it should be accessible from anywhere. Start with the content and don’t force details.

Animations are great if they run smoothly. <abbr>CSS</abbr> transitions and animations are hardware accelerated and have a good performance even on mobile devices whereas Javascript animations are rendered by the <abbr>CPU</abbr>, which looks choppy in most cases. Don’t let your clients expect to see animations in browsers without <abbr>CSS</abbr> transitions/animations support.

## 3. Functional Beauty
To emphasize your content by design, make it beautiful, but unobtrusive. Design to convey a point.

I prefer minimalistic design, but thoughtful skeuomorphism can add personality to your product and guide users. Keep in mind that skeuomorphic elements should emphasize functionality. Don’t add textures or shadows just to make it look good.

## Further Reading

- [Death to Bullshit by Brad Frost](https://vimeo.com/album/2241146/video/56164296)
- [The Vanilla Web Diet by Christian Heilmann](http://coding.smashingmagazine.com/2012/11/13/the-vanilla-web-diet/)
- [Skeuomorphism vs. Simplicity (Video)](http://blog.asana.com/2012/11/design-town-hall/)
