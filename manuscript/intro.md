{sample: true}
# Introduction

We live in exciting times; indeed politically, and in the context of this book, technologically. The times are exciting because there has never been a greater wealth of web technologies, tools, and resources to build ever more appealing and performant web sites and web apps.

The times are also exciting because they are challenging. They are challenging because the wealth of technologies, tools, and resources has led to complexity and confusion.

We can think of the confusion in terms of focus. Precisely, lack of focus, for with all the options we have it has become less apparent what we best pay attention to. This includes what we should do in the first place, and how we should work with what we have at our disposal. It relates to the sites and apps we build, to the frameworks and libraries we use, and—here we get back to why you’re holding this book in your hands—to the code and CSS we write.

In this book we’ll look at ways to improve our CSS. We’ll go over why that generally matters, and why each method matters. We’ll also talk about what doesn’t matter so much. For example, processors. Much of that will have to do with quality as well as craft. Both I deem important, no less of an idea of web development would I wish to promote. How to best _automate_ such optimization is a great question, but first we need to understand what to optimize for exactly—and though it’s encouraged to automate as much as possible, whether optimization is to be done manually or automatically is not a concern of this book.

## Why Optimization Is Important

Sometimes it can be difficult to answer legitimate questions. Why is optimization important? Why do we need the Web? Why should we breathe?

Optimization is important because quality is important. Quality (and quality control) is important because, as I’ve established in [_The Little Book of Website Quality Control_](https://www.oreilly.com/library/view/the-little-book/9781492042860/), “without it, we have no robust way to determine whether what we do and produce is any good. Quality control, therefore, is a key differentiator between professional and amateur work. Consistent quality is the mark of the professional. Quality control, finally, saves time and money and sometimes nerves, particularly in the long run.”

That spontaneous definition, aimed at ways to check our work, doesn’t yet make the beneficiary clear: the user or customer. It’s the end user who benefits and who we want to benefit from great quality work.

As such, optimization, code optimization, CSS optimization all represent a striving to deliver better quality work to the benefit of our users, and to our benefit of becoming greater professionals.

Optimization has a touch of perfectionism, but it’s truly a means and not an end; with optimization, we acknowledge that our initial work can improve.

## What’s Not Covered by Optimization

On the pages that follow, I won’t cover _all_ things relating to CSS development these days. The reason for this is simple: Not all of this relates to _optimization_. And so one thing I won’t cover are CSS preprocessors. Personally, I’ve sided with [Roger Johansson](https://www.456bereastreet.com/archive/201603/why_i_dont_use_css_preprocessors/) and outlined [reasons for not using preprocessors](https://meiert.com/en/blog/no-css-preprocessors/). The little there is to optimize through them is already going to be covered in other ways: for example, through repeat emphasis on coding and formatting standards.

On top of that, I regard it useful to stay close to core technologies and not get distracted by abstractions. In the short run, we may benefit from knowing how to work with abstractions; in the long run, we get greater rewards from knowing the underlying technologies. Therefore, we’ll focus on standard CSS rather than preprocessors, like Sass, Less, or Stylus. And when we look at other CSS tools, we won’t discuss optimization of the use of these tools, their workflows, or how to improve the tools themselves, either.

C> ⁂

The code in this book follows [Google’s HTML/CSS style guide](https://google.github.io/styleguide/htmlcssguide.html). (For an introduction to coding guidelines and commentary on the Google style guide, see [_The Little Book of HTML/CSS Coding Guidelines_](https://www.oreilly.com/library/view/the-little-book/9781492048459/).)

Before we begin, this is a self-published book made with little extra help. If you find mistakes in it, you have all reason to blame me, the author—but also an opportunity to help make the book a little better as a contributor (who are all acknowledged unless chosen otherwise). Please [file an issue](https://github.com/j9t/css-optimization-basics/issues/new) for problems you find, or [submit a pull request](https://github.com/j9t/css-optimization-basics/pulls) for specific fixes and suggestions. If you bought the book [through Leanpub](https://leanpub.com/css-optimization-basics) or [Google Play Books](https://play.google.com/store/books/details/Jens_Oliver_Meiert_CSS_Optimization_Basics?id=xgTfDwAAQBAJ) you should get updates containing your and other people’s fixes automatically. (Otherwise, there’s always [the original source](https://github.com/j9t/css-optimization-basics).)

Thank you for your support.