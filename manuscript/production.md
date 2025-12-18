# Production Optimization

For production, we usually take care of all the things that are good for end users. Software can handle much of this. Some things, however, we benefit from doing ourselves. For example, we can get into the habit of writing more minimal CSS (as with omitting leading `0`’s). Or, in static environments and in small projects, we can work with a single style sheet (to keep the number of requests low and to avoid future HTML changes), without resorting to tools.

## Performance

Performance is one of the primary optimization goals and again, _rendering_ performance is not the subject here. This is due to the so far practical impediments to measure and optimize it, and hence the often comparatively marginal results.

As long as our code is consistent, the steps suggested here can all be taken care of right before production, automatically. They don’t have to find their way back into the operational repository. We’ll start with the exceptions, because they can be covered by our code style guidelines and also be handled manually.

### Character Minimization

To make our style sheets more compact (that is, to make them easier to read and smaller in size), we remove all unneeded characters. That doesn’t refer to whitespace and comments yet. (Both can be covered by the same tool, so let’s make that a separate step.) Instead, it refers to removing CSS that isn’t strictly needed. This includes:

* leading `0`’s (`margin: .1rem`, not `margin: 0.1rem`);
* unneeded trailing `0`’s (`line-height: 1`, not `line-height: 1.0`);
* color notations, to use 3-digit hex where possible (`#fff`, not `#ffffff` or `white`);
* `z-index` values, to be rebased;
* general value shortening (`border: 0` instead of `border: none`, but also—these steps aren’t trivial—`font-family: arial, sans-serif` instead of `font-family: arial, helvetica, sans-serif`, because the fallback font is good practice, but Helvetica would never be used);
* semicolons after the last declaration of each rule.

As noted in the introductory section, these items can be covered by coding guidelines, but they’re also easy to automate and process just before pushing style sheets to production.

### Code Minimization

In the last step, we minimized our CSS code in a way that doesn’t impair understanding. The next step is to remove all characters that aren’t needed for the style sheet to work. This makes it production-ready.

Again, this is only presented as a separate step to illustrate that we can remove certain characters manually. The outcome of full code minimization makes working with style sheets rather cumbersome, if not practically impossible (note the minified style sheet below).

We’re doing two things at this step:

1) removing comments,
2) removing (non-required) whitespace characters.

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

C> _Example: Random, now minified CSS snippet._

As mentioned at the beginning of this book, we benefit from automating our work. As this optimization step is ugly to perform manually, we have a case here that should be and that is almost _always_ automated.

T> For both character and code optimization there are several web-based tools and scripts, for example:
T>
T> * [minifier.org](https://www.minifier.org/) based on Matthias Mullie’s [Minify](https://github.com/matthiasmullie/minify)
T> * [YUI CSS Compressor](https://web.archive.org/web/20210922145733/https://hell.meiert.org/aux/compress/css/gui/) based on Yahoo’s [YUI CSS Compressor PHP port](https://github.com/tubalmartin/YUI-CSS-compressor-PHP-port)
T> * [CSS Minifier](https://cssminifier.com/) by Andrew Chilton
T>
T> For the Node.js ecosystem, some of the more popular packages for CSS compression include:
T>
T> * [clean-css](https://www.npmjs.com/package/clean-css)
T> * [css-minify](https://www.npmjs.com/package/css-minify)
T> * [CSSO](https://www.npmjs.com/package/csso)
T> * [Minify](https://www.npmjs.com/package/minify)
T> * [UglifyCSS](https://www.npmjs.com/package/uglifycss)

### File Normalization

We can work with as many style sheet and preprocessor files as we want, even though that makes it more difficult to avoid declaration repetition (see “Using Declarations Just Once”). However, for production, we should make sure we combine them into a single file to load. That’s important for more effective compression and, even more so, to reduce the number of HTTP requests. ([HTTP/2 alleviates](https://http2.github.io/faq/#what-are-the-key-differences-to-http1x) but at the moment I still advise to limit the number of requests.)

The idea behind this is that HTTP request overhead makes for 500–700 bytes, costing “about 100 ms” (Steve Souders, Kyle Simpson).

This data has led to the recommendation to inline files smaller than 1 KB, but not bigger than 4 KB (Guy Podjarny).

Let’s assume that most sites that use several style sheets (to then be combined to a single one for production) work with files that are larger than 1 KB. As such, it’s useful to have these as individual files (and not inline). For each style sheet that we get rid of and merge, we save roughly half a kilobyte and 10 ms. This leads to the general recommendation to merge all styles into one file and link that from our documents.

Yet, there must be something else. What about small sites, and what about overall file size and caching?

Small sites, particularly one-pagers with just a few rules, may be under the threshold. If the site is and will be a one-pager forever, we have a stronger incentive to inline all code, both styles and scripts. But that also depends on the page itself and our ideas about separation of concerns. If the page resources are so few and light that an extra CSS request is not noticeable, it may well be fine to stick with a separate style sheet. If we strongly believe in separation of concerns, we might just always go for that separation (and what may at first sound rigid then becomes consistent and simple).

File size and caching are normally the issues of biggest concern. They’re linked with the following two questions:

1) If all our styles are in one style sheet, but a user visits just one page, how can we justify pushing all the unused styles onto them?

(Per RocketFuel and Kissmetrics, the average bounce rate on the Web is around 50%—just to provide a number, as bounce rates vary per field as well as per type of content.)

2) Same scenario—if all our styles are in one style sheet, what is a good balance to make sure that the style sheet gets cached but we can swiftly roll out updates?

I set out to go over both questions in detail, but believe it to be more useful now to leave them open. This should remind us that, even though technical questions often beg definite answers, there are questions that don’t lead to a strict “right” or “wrong”—the answers often depend on our priorities.

What’s there to consider for a decision?

* For performance, in terms of efficiency and file size, each page should only come with the styles it uses.
* For performance, in terms of caching, each style sheet should be cacheable.
* For performance, in terms of efficiency and file size when a user visits many pages (low bounce rate with visitors covering a high percentage of needed styles), a single style sheet is fastest.
* For HTML maintainability, style sheets should not be versioned manually (we don’t want to update HTML code every time we update CSS code).
* For CSS maintainability, style sheets should not be broken up manually (we don’t want to merge style sheets every time we update CSS code).
* For general maintainability, code should be kept simple.
* Tooling helps.

et cetera.

I’ll offer a perspective. There are a few reasons for only providing the styles that are actually used on each page. This approach, [CSS tree shaking](https://survivejs.com/webpack/styling/eliminating-unused-css/), should be taken if 1) the project is large (perhaps >10,000 pages, or >10,000 declarations) _and_ 2) it can be automated.

```
┣ index.css (or)
┣ contact.css (or)
┣ search.css (or)
┣ …
```

C> _Example: Page-oriented, automated, cacheable style sheets carrying everything each page needs. (Not covered: Dynamic loading of styles needed on subsequent page visits.)_

In other cases it seems most effective to go for a single style sheet. That holds both for fresh starts (easiest to set up, especially in small projects) as well as for production (in which case the merging or bundling of style sheets should be automated).

```
┣ default.css
```

C> _Example: Just one style sheet._

Compromises and exceptions should be made sparingly and wisely, as I may demonstrate with an approach I took in [Google’s Go framework](https://meiert.com/blog/google-web-frameworks/): Provide a small core style sheet sufficient for basic pages, a bigger one for more complex pages, and individual style sheets for custom subsites and pages.

```
┣ go.css (or)
┣ go-x.css (or)
┣ default.css (extending either go.css or go-x.css)
```

C> _Example: The approach taken by the Go framework._

Ultimately, there’s no single answer for CSS file management. The solution we choose benefits from being simple, but the approach depends on project complexity and our options to automate. And sometimes, as of recent years, our frameworks and tooling answer this for us.

## Output Control

As the final step, it’s important to check what we’re shipping. Did all our optimization steps work? Have we missed anything?

### Reviews and Sanity Checks

At the finishing optimization step, we want to regularly employ code reviews and tests, and to run both manual and automated checks.

The reason to do automated checks is efficiency, as we don’t want to spend human time on constantly validating or otherwise confirming the quality of our style sheets.

The reason to do manual checks is to make sure that nothing went wrong and that we didn’t miss an optimization step, a configuration option, or something else that could have improved the output.

Accordingly, CSS routines may look like this:

* Automated tests: on deployment, daily
* Manual tests: on major updates, weekly

Manual checks can be swift—scan the output, perhaps re-formatted to be more readable. (If browser developer tools don’t suffice for an in-depth look, web-based services like [CSSTidy](https://www.codebeautifier.com/) allow us to “uncompress” a style sheet.)

Automated checks take time to be set up properly and depend on needs and priorities. Solutions include free and paid services used in conjunction with task runners or hooked up to the respective CI pipeline. A simple setup may involve making use of [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) to use a script like [pre-commit](https://github.com/WouterSioen/pre-commit) to validate and lint on commit. Nowadays there are more elegant options, notably [stylelint](https://stylelint.io/).

The topic of reviews brings together much of what we’ve discussed so far: We enforce our desire for quality (the reason why we optimize in the first place) through our development mindsets (like doing our work really well and automating it in order to focus on the things that matter).

C> ⁂

This concludes the basics of CSS optimization. We’ve covered the most important parts, and more than basics. I don’t say that to inflate the idea of “basics” but because pretty much everything else now depends on development paradigms, priorities, and the big picture.

That, then, I’m willing to put to the test: Please share your thoughts on what else should be _required_ optimization steps. Share them privately by [contacting me](https://meiert.com/contact/), or share them publicly, perhaps tagging them so that others can find your views. For this, I propose the hashtag [`#cssoptim`](https://nitter.net/search?f=tweets&q=%23cssoptim).

Other than that, it’s my wish that everyone, the aspiring CSS developer as well as the senior CSS tech lead, could take something from this book. Its value is surely related to how much you can take with you. To compound that value, we’ll finish with an overview and a selection of resources.