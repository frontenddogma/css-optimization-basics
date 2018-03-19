# Introduction

We live in exciting times. Indeed, politically, but particularly, and particularly in the context of this book, technologically. The times are exciting because there has never been a greater wealth of web technologies, tools, and resources to build ever more appealing and performant web sites as well as web apps.

The times are exciting, too, because they are challenging. They are challenging because the wealth of technologies, tools, and resources has led to other types of wealth: of complexity, and of confusion.

The confusion is to be thought of in a sense of focus, precisely: lack of focus, for with all the options we have it has become less apparent what we best pay attention to, whether that’s what we should do in the first place, or how we should work with what we have at our disposal. That relates to the sites and apps we build, to the frameworks and libraries we use, and, and here we get back to why you’re holding this book in your hands, to the code we write, including: the CSS we write.

In this book, then, we’ll look at ways to improve the CSS we write. We’ll go over why that generally matters, and why each method matters. We’ll also talk about what doesn’t matter so much. For example, processors. Much of that will have to do with quality as well as craft. Both I deem important, no less of an idea of web development would I wish to promote. How to best _automate_ such optimization is a great question but first we need to understand what to optimize for exactly—and though I encourage everyone to automate as much as possible, whether optimization is to be done manually or automatically is not a concern of this book.

## Why Optimization Is Important

Sometimes I find it difficult to answer legitimate questions. Why is optimization important? Why is breathing useful? Why should we eat?

Optimization is important because quality is important; and quality (and quality control) is important because, as I’ve established in [_The Little Book of Website Quality Control_](http://www.oreilly.com/web-platform/free/the-little-book-of-website-quality-control.csp), “without it we have no robust way of determining whether what we do and produce is any good. Quality control, therefore, is a key differentiator between professional and amateur work. Consistent quality is the mark of the professional. Quality control, finally, saves time and money and sometimes nerves, particularly in the long run.”

That spontaneous definition, aiming at ways to check our work, does not yet make the beneficiary clear: the user or customer. It’s the end user who benefits and who we want to benefit from great quality work.

As such, optimization, code optimization, CSS optimization all represent a striving to deliver better quality work to the benefit of our users, and to our benefit of becoming greater professionals.

Optimization has a touch of perfectionism, but it’s truly a means, and not an end; with optimization we acknowledge that our initial work can be improved.

## What’s Not Covered by Optimization

In this book, then, we won’t cover _all_ things relating to CSS development these days. The reason for this is simple: Not all of this relates to _optimization_. And so one thing I won’t cover here are CSS preprocessors. Personally, I’ve sided with [@@](@@) and outlined [reasons for not using preprocessors](https://meiert.com/en/blog/no-css-preprocessors/), but the little there is to optimize through them is already going to be covered in this book in other ways: for example, through repeat emphasis on coding and formatting standards.

On top of that comes that I regard it more useful to stay close to core technologies, and not get bogged down by abstractions, abstractions like preprocessors. In the short run we may benefit from knowing well how to handle abstractions; but in the long run we get much greater rewards from knowing the underlying systems and technologies. And therefore we’ll focus on standard CSS rather than non-standard Sass, Less, Stylus, and whatnot.

The same applies to other forms of abstraction, and so we’ll look and point at CSS tools, but not discuss optimization of use of these tools, their workflows, nor how to improve those tools themselves.

C> ⁂

The code in this book follows [Google’s HTML/CSS style guide](https://google.github.io/styleguide/htmlcssguide.html). (For an introduction to coding guidelines and notes on the Google style guide, see [_The Little Book of HTML/CSS Coding Guidelines_](http://www.oreilly.com/web-platform/free/little-book-html-css-coding-guidelines.csp).)

Before we begin, this is a self-published book made with little extra help. If you find mistakes in it, you have all reason to blame me as the author—but also a great opportunity to help make the book a little better as a contributor (who are all mentioned unless they choose not to be named). Please [file an issue](https://github.com/j9t/css-optimization-basics/issues/new) for every problem you find, or [submit a pull request](https://github.com/j9t/css-optimization-basics/pulls) for specific fixes and suggestions. If you bought the book [through Leanpub](https://leanpub.com/css-optimization-basics) you should get updates containing your and other people’s fixes automatically. (Otherwise there’s always [the original source](https://github.com/j9t/css-optimization-basics).)

Thank you for your support, your understanding, and your help.