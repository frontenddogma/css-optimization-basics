# Production Optimization

For production, we usually take care of all the things that are good for machines. I’ve organized this section so that it also contains the things that can be done _by_ machines (tools)—without, again with an eye on us as professionals, including anything that, if we were to miss it, would make us produce significantly worse code.

It turns out, then, that we do again benefit from trying to follow some of the (human-friendly) ideas ourselves. For example, we can well try to write minimal CSS (like omitting leading `0`’s), or to only link one style sheet (to keep the number of requests low and to avoid future HTML changes), without leaving this to tools.

## Performance

Performance is one of the primary optimization goals, and again _rendering_ performance is not the subject here for its often marginal achievements and yet grave practical impediments.

As long as our code is consistent, the steps suggested here can all be taken care of right before production, automatically, and they don’t have to find their way back into the operational repository. The exception is what we’ll start with, because it can first be covered by our code style guidelines and all get handled manually.

### Character Minimization

To make our style sheets more compact, that is, make them easier to read and smaller in size, we remove all unneeded characters. That doesn’t refer to whitespace and comments yet—let’s make this a separate step, although both can be covered by the same tool—, but to removing any CSS that isn’t strictly needed. This entails:

* semicolons after the last declaration of each rule;
* leading `0`’s (`margin: .1em`, not `margin: 0.1em`);
* unneeded trailing `0`’s (`line-height: 1`, not `line-height: 1.0`);
* color notations to use 3-digit hex, where possible (`#fff`, not `#ffffff` or `white`);
* value shortening (`border: 0` instead of `border: none` but also (these steps aren’t trivial!) `font-family: arial, sans-serif` instead of `font-family: arial, helvetica, sans-serif`—the fallback font is good practice but Helvetica, here, would never be used).

As noted in the introductory section, these items can well be covered by coding guidelines but they’re also easy enough to automate and run through just before pushing style sheets to production.

### Code Minimization

After we’ve minimized our style sheet code without impairing understandability, the next steps means to remove all the characters that aren’t needed for the style sheet to work—this makes it production-ready.

Note again that this is only presented as a separate step here to _illustrate_ that we can remove certain characters manually—perhaps our style guide requires us to, where possible, use 3-digit hex color values—and still are able to work with our style sheets. As a true manual task it would make style sheet maintenance rather cumbersome if not practically impossible.

What’s done here are typically two things:

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

As mentioned in the beginning of this book, we benefit from automating our work—as this optimization step is ugly to do and ugly to work with we actually have something here that is almost _always_ automated.

I> For both character and code optimization there are several tools and scripts on the market, for example:
I> 
I> * [minifier.org](http://www.minifier.org/) based on Matthias Mullie’s [Minify](https://github.com/matthiasmullie/minify)
I> * [YUI CSS Compressor](https://hell.meiert.org/aux/compress/css/gui/) based on Yahoo’s [YUI CSS Compressor PHP port](https://github.com/tubalmartin/YUI-CSS-compressor-PHP-port)
I> * [CSS Minifier](https://cssminifier.com/) by Andrew Chilton

### File Normalization

Although it makes it more difficult to avoid declaration repetition (see “Using Declarations Just Once”), we can work with as many CSS or preprocessor files as we want. However, at the end, for production, we should make sure to combine them to a single file to load. That’s important for more effective compression and even more so for fewer HTTP requests. ([HTTP/2 alleviates](https://http2.github.io/faq/#what-are-the-key-differences-to-http1x) here but for this first edit, I wish to stick to advising for fewer requests.)

That’s simplified but the basic idea behind this is that HTTP request overhead makes for 500–700 bytes (based on work from Steve Souders and Kyle Simpson) costing “about 100&nbsp;ms” (Kyle Simpson).

This data has led others to recommend that files smaller than 1&nbsp;KB should be inlined, and to avoid inlining of files that are bigger than 4&nbsp;KB (Guy Podjarny).

We may say that most sites that use several style sheets (to then be combined to a single one for production) do work with files that are larger than 1&nbsp;KB. As such it’s useful to have these as individual files (and not inline), but for each style sheet we get rid of and merge we save roughly half a kilobyte and 10&nbsp;ms. This leads to the general recommendation to merge all styles into one file and link that from our documents.

As we can tell, there must be something else here. What about tiny sites, and what about overall file size and caching?

Tiny sites, particularly one-pagers with just a few rules, may be under the threshold. If the site is and will be a one-pager forever we have a stronger incentive to inline all code, both styles and scripts. But that also depends on the page itself and our ideas about true separation of concerns. If the page resources are so few and so small that the extra CSS request is not felt anyway, then it may well be fine to stick with separation. Likewise if we strongly believe in separation of concerns, we might just always go for that separation (and what may sound a little rigid here I consider useful for its simplicity).

File size and caching are normally the issues that are of more concern now. The concern boils down to the following two questions:

1) If all our styles are in one style sheet, but a user visits just one page, how can we justify pushing all the unused styles onto them?

(Per RocketFuel and Kissmetrics, the average bounce rate on the Web is around 50%—just to provide some number, as bounce rates actually vary heavily per field as well as per type of content.)

2) Same scenario, if all our styles are in one style sheet, what is a good balance to make sure that the style sheets get cached but we can swiftly roll out updates?

I set out to go over both questions in detail but I believe it to be more useful to leave them to everyone to decide on their own. This should be useful, too, to remind ourselves that even though technical questions often beg quite definite answers, there are questions that don’t lead to a strict “right” or “wrong”—the answers often still depend on our priorities.

What’s there to consider for our decision?

* For performance in terms of efficiency and file size, each page should only come with the styles it uses.
* For performance in terms of caching, each style sheet should be cacheable.
* For performance in terms of efficiency and file size if a user visits many pages (low bounce rate with visitors covering a high percentage of needed styles), a single style sheet is fastest.
* For HTML maintainability, style sheets should not be versioned manually (we don’t want to update HTML code every time we update CSS code).
* For CSS maintainability, style sheets should not be broken up manually (we don‘t want to merge style sheets every time we update CSS code).
* For general maintainability, code should be kept simple.

et cetera.

I’ll still offer a view. There are a few reasons for only providing the styles that are used on each page. This approach should be taken if 1) the project is large (perhaps >10,000 pages, or >10,000 declarations) _and_ 2) it can be automated.

* index.css (or)
* contact.css (or)
* search.css (or)
* …

C> _Example: Page-oriented, automated, cacheable style sheets carrying everything each page needs. (Bonus exercise not covered here: Dynamically load only the styles needed on subsequent page visits.)_

In other cases it seems most effective to go for a single style sheet, whether to begin with (easiest to set up) or for production (in which case the merging of files should be automated, which can happen through something as simple as PHP-importing sub style sheets into a default.css—processed as PHP but returned as `text/css`, of course).

* default.css

C> _Example: Just one style sheet._

And there are compromises (aka exceptions) to be used sparingly and wisely, like [the approach taken with Google’s Go framework](https://meiert.com/en/blog/google-web-frameworks/): Provide a small core style sheet sufficient for basic pages, a bigger one for more complex pages, and individual style sheets for custom sub sites and pages.

* go.css (or)
* go-x.css (or)
* default.css (importing either go.css or go-x.css)

C> _Example: The approach taken by the Go framework._

At the end of the day there is no single answer for optimal CSS file management. Complexity is an important aspect, automation is an important approach, simplicity is an important criterion.

## Output Control

As the final step as per this basic treatise, it’s important to check what we’re finally shipping. Did all our other optimization steps work? Have we missed anything?

### Reviews and Sanity Checks

For the finishing optimization step we want to regularly employ code reviews and tests, and to run _both_ manual and automated checks.

The reason to do automated checks is efficiency, as we don’t want to spend any human time on constantly validating or otherwise confirming the quality of our style sheets.

The reason to do manual checks is not to miss anything glaring, issues that fly under the radar because we missed how, say, a preprocessor may have had a flag that left in comments, or that otherwise generates production output that isn’t desirable.

* Automated tests: daily and on deployment
* Manual tests: weekly

C> _Example: CSS routines._

The manual checks can be swift; gloss over the output, perhaps re-formatted to be legible again (tools like [CSSTidy](https://hell.meiert.org/aux/optimize/css/) allow to throw a CSS URL at them to be “uncompressed”).

The automated checks ask for time to be set up properly and depend on one’s priorities and needs; one popular way is to use [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) to validate and lint on commit, as through scripts like Wouter Sioen’s [pre-commit](https://github.com/WouterSioen/pre-commit).

These reviews wrap a nice tie around much of what we’ve discussed so far: We enforce our desire for quality (the reason why we optimize in the first place) through our development mindsets (like doing our work really well and automating it so to focus on the things that matter).

C> ⁂

This concludes the overview on CSS optimization basics. We’ve covered the most important aspects, and more than basics; and I don’t say that so to inflate the idea of “basics” but because pretty much everything else now depends on development paradigms, priorities, and the big picture.

That, then, I’m willing to put to the test: Please share your thoughts on what should also be _required_ optimization steps. Share them privately, by [contacting me](https://meiert.com/en/contact/), or share them publicly, perhaps tagging them so that others can find your views. Although my own shortcut was `#csso` I’ll propose the more verbose and more clear `#cssoptim`.

Other than that, it’s my wish that everyone, the aspiring CSS developer as well as the senior CSS wizard, could take something out of this book. Its value is surely related to how much you can take with you. To compound that value we’ll finish with an overview and a selection of tools and references.