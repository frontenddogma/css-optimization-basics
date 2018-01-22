# Operational Optimization

In this first part of optimization, operational optimization, we’re going to talk about the options we have to write higher quality CSS while we’re right at them—in operation. (The second part will deal with options to optimize for production, that is, for release.)

Just as it didn’t seem useful to cover preprocessors so to get a clear look at CSS itself, we’re not going to discuss documentation, as with in-file comments, nor (most) guidelines that we can put in effect automatically. Documentation is an entirely different topic that has more to do with maintenance than with optimization, and coding guidelines, as important as they are and as many of them we can set up, are often a matter of preference that does not have a bearing on quality (also see: [_The Little Book of HTML/CSS Coding Guidelines_](http://www.oreilly.com/web-platform/free/little-book-html-css-coding-guidelines.csp)). We’re hence already applying two of our mantras: to keep it simple, and to automate.

## Understandability

In operation, we need to make sure our work is understandable. This does not only refer to multi-person environments in which we’re not alone working on a project; with consistency, for example, there’s at least individual consistency, which means to write code consistent with ourselves.

This understandability, as we just established for documentation and comments, can in parts be achieved automatically. But some pieces, and ironically we’ll right start with one (consistent declaration sorting), just from the go, are so important and useful to learn how to do manually, that we’ll still go over them. And so we’ll look at consistency and simplicity now as the two pillars for more understandable, for simplistically optimized CSS code.

### Consistency

Consistency in the case of code means to write and format things the same way every time. With individual or [“level 1” consistency](https://meiert.com/en/blog/consistency-levels/), this means to be consistent with how we ourselves write code. With collective consistency, we strive to stay consistent within the realm that we work in, as when we touch third party code and stick to their code style. And then there’s institutional or “level 3” consistency, referring to being consistent to coding standards put up by our organization.

Consistency is a _foundational_ part of optimization; it’s the first step of optimization. Without any sort of consistency, our optimization attempts are a lot harder.

```css
.feeds ul,
.posts ul ,
.events ul {
  list-style: none;
  margin: 0
}

.feeds li,
.posts li,
.events li {
  border-top: 1px solid #eeeeee;
  border-top: 1px solid rgba(238, 238, 238, 0.1);
  padding: 0.7667em 0;
}

.feeds li:first-child,
.posts li:first-child,
.events li:first-child {
  border-top: 0;
  padding-top: 0;
}

.feeds li:last-child,
.posts li:last-child,
.events li:last-child {
  padding-bottom: 0;
}

.authors > ul > li > a {
  margin-bottom: 1em;
  display: inline-block;
}

.authors ul {
  list-style: none;
  margin:0;
}

.authors li {
  padding: .7667em 0;
  border-top: 1px solid #eee;
  border-top: 1px solid rgba(238, 238, 238, 0.1);
}

.authors li:first-child {
   border-top: 0;
   padding-top: 0;
}

.authors li:last-child {
  padding-bottom: 0;
}

.contributors {
  color: #eee;
  border-top: 1px solid;
}

.contributors:first-child {
  border-top: none;
}
```

Example: Optimize this code by removing all the duplicates.

```css
.feeds ul,
.posts ul ,
.events ul {
  list-style: none;
  margin: 0;
}

.feeds li,
.posts li,
.events li {
  border-top: 1px solid #eeeeee;
  border-top: 1px solid rgba(238, 238, 238, 0.1);
  padding: .7667em 0;
}

.feeds li:first-child,
.posts li:first-child,
.events li:first-child {
  border-top: 0;
  padding-top: 0;
}

.feeds li:last-child,
.posts li:last-child,
.events li:last-child {
  padding-bottom: 0;
}

.authors > ul > li > a {
  display: inline-block;
  margin-bottom: 1em;
}

.authors ul {
  list-style: none;
  margin: 0;
}

.authors li {
  border-top: 1px solid #eee;
  border-top: 1px solid rgba(238, 238, 238, 0.1);
  padding: .7667em 0;
}

.authors li:first-child {
  border-top: 0;
  padding-top: 0;
}

.authors li:last-child {
  padding-bottom: 0;
}

.contributors {
  border-top: 1px solid #eee;
}

.contributors:first-child {
  border-top: 0;
}
```

Example: Now optimize this code.

Consistency is reasonably easy to achieve. We [establish coding guidelines](http://www.oreilly.com/web-platform/free/little-book-html-css-coding-guidelines.csp), we use (or build) tools to help follow and test for the guidelines, and then we enforce the guidelines. This goes as far as that many guidelines can be enforced right after writing and editing our CSS, and then again for production, where we may apply slightly different rules particularly geared towards production.

We’ll cover this last step in the chapter, “Production Optimization” and go over some tools under “Tools and Resources”—but we’ll spare ourselves from going over often subjective coding guidelines and how to automate their implementation and enforcement. What we’ll do is cover select aspects of consistency that are of particular import to CSS optimization. One is automatable; the other isn’t: declaration sorting and selector sorting.

#### Declaration Sorting

This is trivial and at the same time automatable: _Sort declarations alphabetically._ As Google advocates—disclaimer: I’ve worked on setting up respective guidelines—, the only exception are vendor-specific extensions (self-destructing declarations that start with hyphens) which are located right before respective declaration to complement.

```css
.example {
  background: none;
  border: 1em dotted #069;
  color: #096;
  display: block;
  float: none;
  font-size: 1em;
  font-style: italic;
  height: 100px;
  margin-top: 1em;
  max-width: calc(100vw - 10em);
  outline: 2em solid #609;
  overflow: auto;
  padding: 1em;
  position: relative;
  text-align: center;
  top: 1em;
  white-space: pre-wrap;
  width: 100%;
  z-index: 1;
  filter: blur(33.35px) sepia(0.34);
  -webkit-filter: blur(33.35px) sepia(0.34);
  -moz-filter: blur(33.35px) sepia(0.34);
}
```

Example: Quick, where do we add `transform: rotateY(10deg);` so that quick, someone else can immediately spot it?

This is trivial and automatable but still, in my eyes, one of the key optimization methods. That is so because an almost failsafe, easily repeatable, soon habitual, quickly communicable, and quite universal method to structure our code is something that has tremendous value. A simple and robust sorting scheme like the alphabetical ordering of declarations will at once make our code more understandable and help anyone touching it navigate in it.

I intentionally raise alphabetical sorting to “optimization status” because of its many benefits; our code will be better once we structure it, and we will write better code once we can do it ourselves, and not meed some processor to do that for us. (Not all CSS we’ll touch will have a script behind it that sorts for us, so we do benefit from engraining this way of sorting.)

[Sort declarations alphabetically.](https://meiert.com/en/blog/on-declaration-sorting/)

@@