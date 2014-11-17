---
date: 2014-07-14
---
# Why I write tests

In a recent [survey](http://webkrauts.de/artikel/2014/jetzt-wissen-wir-es) over 700 German web workers were asked if they write automated tests. Only 28% answered this question with “yes”. This mirrors my experience I had during my professional career as a web developer up to now and I think this is an alarming situation for the web platform and the software industry in general.

I think there are several reasons for this. In my opinion the only valid one is that some developers are building the visual representation of a system, e.g. CSS and HTML as [this can’t be tested automatically](http://blog.8thlight.com/uncle-bob/2014/04/30/When-tdd-does-not-work.html).

Then there are junior developers. Of course they don’t think about writing tests as they have yet to struggle with the language itself and are happy when the code they write produces the results they want. It’s the task of universities and senior developers to assist them in writing automated tests. In most other crafts this is what mentorships are for. Something the software industry sadly [hasn’t fully adopted yet](http://blog.8thlight.com/uncle-bob/2013/11/25/Novices-Coda.html). I believe companies that manage to create successful apprenticeship programs will succeed in the long run.  

Unfortunately there are also experienced developers that feel like writing tests was invented to make other developers feel bad about their code. For them it doesn’t solve an actual problem. It’s this annoying thing you should probably do, because it’s “the right thing to do”. It’s just the icing on the cake. It’s something you can add later when there is time and budget left. The only thing that matters to them is that their software “works”. Whenever I meet a developer with this opinion in the future I’ll ask him/her one question:

> “How do you know that your software works?”

Funnily these developers have the same goal as the ones with tests: creating _working_ software quickly that solves actual problems. The only difference is that they believe writing tests hinders them from doing so.

Some of them think that following practices like TDD creates a “[magical place](http://www.devjoy.com/2014/07/stop-focusing-on-agile-and-fly-the-damn-plane/)” that creates working software. I’d argue that adding or editing code and believing everything just works without testing sounds more like a “magical place” to me.

## Programming Problems

While building software, I constantly reflect on the code I write. I also read a lot of books and articles about software development and try out new patterns, tools and practices to do my work more efficiently.

I do this mainly because of two reasons:
1. I love programming. I want to master my craft.
2. I get paid for it. I am a professional programmer.

Some time ago I noticed that I was facing the same problems in every project I worked on.

Having added a new feature or having fixed a bug left me wondering if I broke existing functionality. It didn’t matter if I wrote the code or someone else. The more features the software had, the more time it took me to test all of the previous ones to check if I didn’t break anything. Therefore I most often opened the browser and only tested the feature I added or tried to reproduce the bug I fixed. I just _assumed_ the rest would still work, but of course this only worked out rarely.

> I needed a way to immediately see if I broke the existing behavior of my code.

Sometimes I have to jump between different projects and edit code I don’t understand. This may be because I have forgotten how I built the system or just because someone else wrote it. Most often documentation is out-of-date or only about setting up the project, but not how the code itself is structured, which objects and functions exist and how they are supposed to be used. Reading through thousands lines of code takes a long time and hinders me from solving the actual problem, like fixing a bug or adding a feature.

> I needed a way to see how a code base is structured and supposed to work without reading through huge parts of it.

The harder it is to understand the code, the longer it takes to make changes to it. That’s why I often rename variables and functions or restructure modules to make it more readable for the next developer. This could be me in 10 seconds, minutes, hours, days… or someone else. [Refactoring](http://martinfowler.com/bliki/DefinitionOfRefactoring.html) is a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior, but nevertheless I sometimes introduced bugs while doing so. I simply forgot to rename a variable or did a mistake while restructuring.

> I needed a way to feel confident about refactoring to make my code easier to understand.

Being aware of the SOLID principles and the aspects of clean code I constantly try to decouple the entities in my code into small, reusable components and functions that do one thing only. Nevertheless I sometimes struggle to find a good solution and I can’t always ask another developer to point out the architecture’s parts that are too tightly coupled.

> I needed a way to see problems in my software architecture.

Let’s quickly recapitulate what I wanted to achieve:

1. Knowing immediately when I break something.
2. Having an up-to-date documentation about the code.
3. Being confident about making my code easier to understand.
4. Having indications for too tightly coupled code.

## The solution

These goals can be achieved by writing tests. If tests fail I know that something is broken. The tests themselves are an always up-to-date documentation of the code as they would fail if I change its behavior. I am confident about refactoring as I can run the tests to see if everything still works as before. Code that is hard to test is very likely to be too tightly coupled, therefore tested code is less coupled and better structured.

I want these advantages during the whole development process, therefore I push myself to write tests first. (TDD) Yes, it takes some time to get used to, because habits are hard to change. Yes, it is a different way of thinking, but it’s superior in my opinion, as I have to think about the intended behavior of the system before actually building it. Yes, my tests are probably not perfect (yet) and I don’t test everything, because I am still in the learning process. Yes, it takes time to write tests, but in my experience it takes way less time to debug new errors that occur afterwards, because you can literally see where your code breaks. 

I am _not_ suddenly writing perfect code now. There’ll never be perfect code. Systems, tools and requirements are constantly changing. I found a solution for these problems though and these are problems every developer has to solve somehow.

I don’t care _how_ you solve them, as long as you _do_ solve them. Maybe you have found a better solution than writing tests and please let me know if you did, because I don’t think there is one. Thus I have to assume that these problems exist whenever I have to work with untested code.

If you decide not to write tests, you decide that you won’t know when the feature you are currently implementing breaks in the future. You decide to not having an always up-to-date documentation of your code. You decide to make refactoring harder. You decide to have nothing pointing out tightly coupled parts of your code.

I change my habits and write tests. Working software has no short cuts. Stop taking them.