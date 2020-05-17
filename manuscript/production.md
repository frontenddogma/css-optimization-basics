# Production Optimization

For production we usually take care of all the things that are good for end users, of which much can be handled by software. Some of this, however, we benefit from doing ourselves. For example, we can get into the habit of writing more minimal CSS (as with omitting leading `0`’s), or, in static environments, of only working with one style sheet (to keep the number of requests low and to avoid future HTML changes), without leaving this to tools.

## Performance

Performance is one of the primary optimization goals, and again _rendering_ performance is not the subject here for the often comparatively marginal results and the practical impediments to measure and work with it effectively.

As long as our code is consistent, the steps suggested here can all be taken care of right before production, automatically, and they don’t have to find their way back into the operational repository. We’ll start with the exceptions, because they can be covered by our code style guidelines and also be handled manually.

### Character Minimization

To make our style sheets more compact, that is, make them easier to read and smaller in size, we remove all unneeded characters. That doesn’t refer to whitespace and comments yet—let’s make this a separate step, although both can be covered by the same tool—, but to removing any CSS that isn’t strictly needed. This affects:

* leading `0`’s (`margin: .1em`, not `margin: 0.1em`);
* unneeded trailing `0`’s (`line-height: 1`, not `line-height: 1.0`);
* color notations to use 3-digit hex, where possible (`#fff`, not `#ffffff` or `white`);
* `z-index` values to be rebased;
* general value shortening (`border: 0` instead of `border: none`, but also—these steps aren’t trivial—`font-family: arial, sans-serif` instead of `font-family: arial, helvetica, sans-serif`, because the fallback font is good practice, but Helvetica would never be used);
* semicolons after the last declaration of each rule.

As noted in the introductory section, these items can be covered by coding guidelines but they’re also easy enough to automate and run through just before pushing style sheets to production.

### Code Minimization

After we’ve minimized our CSS code in a way that doesn’t impair understandability, the next step means to remove all the characters that aren’t needed for the style sheet to work—this makes it production-ready.

Note again that this is only presented as a separate step to illustrate that we can remove certain characters manually—perhaps our style guide requires us to, where possible, use 3-digit hex color values—but are still able to work with our style sheets. As a true manual task code minimization would make style sheet maintenance rather cumbersome, if not practically impossible.

What’s being done are typically two things:

1) remove all comments,
2) remove all (non-required) whitespace characters.

```css
html {
  font: 87.5%/1.5 'helvetica neue', helvetica, sans-serif;
  max-width: 600px;
  padding: 1em;
}

footer {
  border-top: 1px solid #eee;
  margin: 2.5em 0 0;
  padding: 3px 0 0;
}

footer small,
label {
  display: block;
}
```

C> _Example: Random non-minified CSS snippet._

```css
html{font:87.5%/1.5 'helvetica neue',helvetica,sans-serif;max-width:600px;padding:1em}footer{border-top:1px solid #eee;margin:2.5em 0 0;padding:3px 0 0}footer small,label{display:block}
```

C> _Example: Random now minified CSS snippet._

As mentioned in the beginning of this book, we benefit from automating our work. As this optimization step is ugly to do and ugly to work with we actually have something here that’s almost _always_ automated.

I> For both character and code optimization there are several web-based tools and scripts, for example:
I> 
I> * [minifier.org](https://www.minifier.org/) based on Matthias Mullie’s [Minify](https://github.com/matthiasmullie/minify)
I> * [YUI CSS Compressor](https://hell.meiert.org/aux/compress/css/gui/) based on Yahoo’s [YUI CSS Compressor PHP port](https://github.com/tubalmartin/YUI-CSS-compressor-PHP-port)
I> * [CSS Minifier](https://cssminifier.com/) by Andrew Chilton
I>
I> For the Node ecosystem, some of the more popular packages for CSS compression include:
I>
I> * [clean-css](https://www.npmjs.com/package/clean-css)
I> * [css-minify](https://www.npmjs.com/package/css-minify)
I> * [UglifyCSS](https://www.npmjs.com/package/uglifycss)

### File Normalization

Although it makes it more difficult to avoid declaration repetition (see “Using Declarations Just Once”), we can work with as many style sheet or preprocessor files as we want. However, in the end, for production, we should make sure to combine them into a single file to load. That’s important for more effective compression and even more so for fewer HTTP requests. ([HTTP/2 alleviates](https://http2.github.io/faq/#what-are-the-key-differences-to-http1x) but at the moment I stick to advising for fewer requests.)

The basic idea behind this is that HTTP request overhead makes for 500–700 bytes (according to work by Steve Souders and Kyle Simpson), costing “about 100&nbsp;ms” (Kyle Simpson).

This data has led others to recommend that files smaller than 1&nbsp;KB should be inlined, and to avoid inlining of files that are bigger than 4&nbsp;KB (Guy Podjarny).

We may say that most sites that use several style sheets (to then be combined to a single one for production) do work with files that are larger than 1&nbsp;KB. As such it’s useful to have these as individual files (and not inline), but for each style sheet we get rid of and merge we save roughly half a kilobyte and 10&nbsp;ms. This leads to the general recommendation to merge all styles into one file and link that from our documents.

Yet, there must be something else. What about tiny sites, and what about overall file size and caching?

Tiny sites, particularly one-pagers with just a few rules, may be under the threshold. If the site is and will be a one-pager forever we have a stronger incentive to inline all code, both styles and scripts. But that also depends on the page itself and our ideas about true separation of concerns. If the page resources are so few and so small that the extra CSS request is not noticeable, then it may well be fine to stick with separation. Likewise if we strongly believe in separation of concerns, we might just always go for that separation (and what may at first sound rigid then just becomes consistent and simple).

File size and caching are normally the issues that are of biggest concern. The concern boils down to the following two questions:

1) If all our styles are in one style sheet, but a user visits just one page, how can we justify pushing all the unused styles onto them?

(Per RocketFuel and Kissmetrics, the average bounce rate on the Web is around 50%—just to provide some number, as bounce rates vary per field as well as per type of content.)

2) Same scenario, if all our styles are in one style sheet, what is a good balance to make sure that the style sheets get cached but we can swiftly roll out updates?

I set out to go over both questions in detail but I believe it more useful to leave them to everyone to decide on their own. This should be useful also to remind ourselves that even though technical questions often beg quite definite answers, there are questions that don’t lead to a strict “right” or “wrong”—the answers often still depend on our priorities.

What’s there to consider for a decision?

* For performance in terms of efficiency and file size, each page should only come with the styles it uses.
* For performance in terms of caching, each style sheet should be cacheable.
* For performance in terms of efficiency and file size if a user visits many pages (low bounce rate with visitors covering a high percentage of needed styles), a single style sheet is fastest.
* For HTML maintainability, style sheets should not be versioned manually (we don’t want to update HTML code every time we update CSS code).
* For CSS maintainability, style sheets should not be broken up manually (we don‘t want to merge style sheets every time we update CSS code).
* For general maintainability, code should be kept simple.

et cetera.

I’ll still offer a view. There are a few reasons for only providing the styles that are used on each page. This approach, [CSS tree shaking](https://survivejs.com/webpack/styling/eliminating-unused-css/), should be taken if 1) the project is large (perhaps >10,000 pages, or >10,000 declarations) _and_ 2) it can be automated.

* index.css (or)
* contact.css (or)
* search.css (or)
* …

C> _Example: Page-oriented, automated, cacheable style sheets carrying everything each page needs. (Bonus exercise not covered here: Dynamically load only the styles needed on subsequent page visits.)_

In other cases it seems most effective to go for a single style sheet, whether to begin with (easiest to set up) or for production (in which case the merging of files should be automated, which can happen through something as simple as PHP-importing sub style sheets into a default.css—processed as PHP but returned as `text/css`, of course).

* default.css

C> _Example: Just one style sheet._

Compromises and exceptions should be made sparingly and wisely, as with [the approach taken by Google’s Go framework](https://meiert.com/en/blog/google-web-frameworks/): Provide a small core style sheet sufficient for basic pages, a bigger one for more complex pages, and individual style sheets for custom subsites and pages.

* go.css (or)
* go-x.css (or)
* default.css (importing and extending either go.css or go-x.css)

C> _Example: The approach taken by the Go framework._

At the end of the day there is no single answer for optimal CSS file management. The solution benefits from being simple, but the approach depends on project complexity as well as our options to automate.

## Output Control

As the final step as per this basic treatise, it’s important to check what we’re ultimately shipping. Did all our other optimization steps work? Have we missed anything?

### Reviews and Sanity Checks

At the finishing optimization step we want to regularly employ code reviews and tests, and to run _both_ manual and automated checks.

The reason to do automated checks is efficiency, as we don’t want to spend human time on constantly validating or otherwise confirming the quality of our style sheets.

The reason to do manual checks is to make sure that nothing went wrong and that we didn’t miss an optimization step, a configuration option, or something else that could have improved the output. 

* Automated tests: daily and on deployment
* Manual tests: weekly

C> _Example: CSS routines._

Manual checks can be swift; gloss over the output, perhaps re-formatted to be legible again (tools like [CSSTidy](https://hell.meiert.org/aux/optimize/css/) allow to throw a CSS URL at them to be “uncompressed”).

Automated checks ask for time to be set up properly and depend on one’s priorities and needs. One popular way is to use [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) to validate and lint on commit, as through scripts like Wouter Sioen’s [pre-commit](https://github.com/WouterSioen/pre-commit).

These reviews wrap a nice tie around much of what we’ve discussed so far: We enforce our desire for quality (the reason why we optimize in the first place) through our development mindsets (like doing our work really well and automating it, to focus on the things that matter).

C> ⁂

This concludes the overview on CSS optimization basics. We’ve covered the most important aspects, and more than basics; and I don’t say that to inflate the idea of “basics” but because pretty much everything else now depends on development paradigms, priorities, and the big picture.

That, then, I’m willing to put to the test: Please share your thoughts on what should be _required_ optimization steps. Share them privately, by [contacting me](https://meiert.com/en/contact/), or share them publicly, perhaps tagging them so that others can find your views. Although my own shortcut was `#csso` I’ll propose the more verbose and more clear [`#cssoptim`](https://twitter.com/search?q=%23cssoptim).

Other than that, it’s my wish that everyone, the aspiring CSS developer as well as the senior CSS tech lead, could take something out of this book. Its value is surely related to how much you can take with you. To compound that value we’ll finish with an overview and a selection of tools and references.