# Overview

CSS optimization is important because we, especially as individuals, don’t always write perfectly efficient and maintainable and understandable code.

Writing such code, quality code, however, is what makes us professionals.

CSS optimization does not entail “everything” that can be done in CSS or through tools; it entails what makes it more efficient and maintainable and understandable while achieving a good balance.

As professionals, we benefit from doing one (or two, or three, but not eighty-five) things really, really well; as web developers, it’s not a bad idea if CSS is one of these things.

It’s useful when we know our needs.

It’s practical when we develop for the present.

It makes our work easier when we keep it simple.

There’s nothing wrong with doing less work—by automating it.

There’s nothing wrong, either, with not doing work that is automated.

(There’s much wrong with not doing needed work because we haven’t yet automated it, perhaps.)

Code should be understandable, and for that it’s useful when it’s consistent and simple.

Consistent CSS is footed on alphabetical declaration sorting (everything else is much too complicated) and on a robust order for selector sorting.

Simple CSS uses functional or generic names or avoids IDs and classes altogether.

Simple CSS also likes shorthands (yes).

Speed is important.

In CSS, selector performance doesn’t matter, and inline CSS is a crime in many countries.

(Web development is not software development.)

Some declarations may be slower than others but there’s rarely reason for panic.

Rule hygiene may be most important for CSS performance.

The most basic way to determine quality is through validation, and high error counts unequal high quality scores.

Every piece of code gets at least touched _twice_.

Web Design is a process.

For these last two reasons, maintainability and maintenance are critical.

`!important` is not an obstacle to maintenance; it’s a tool.

One of the most important principles is separation of concerns, and contents, structure, presentation, behavior are all different concerns.

In code, we don’t want to repeat ourselves.

Accordingly, in CSS, we do want to limit the repetition of declarations.

Optimization for production is an important second step, because in production machines use our code, whereas in operation, humans use it.

When we cannot production-optimize automatically, we should do as much as we can manually, as part of our craft.

For production, we remove all unneeded characters. All of them.

We typically want to reference one style sheet that includes all the styles, though there are cases of high complexity in which a different approach can lead to better performance.

(We cannot be absolved from thinking and making decisions about our particular projects.)

(Exceptions prove the rule.)

We regularly review our CSS, both pre-production and in production.

We are professionals and we aim for quality work.

As professionals we are aware of our responsibilities, we hold ourselves accountable, and we set high ethical standards for ourselves.

And, as professionals, we lead by example.

## Tools and References

The following lists a small selection of useful _CSS_ tools, websites, and books. They are geared towards more experienced developers, and they are because the novice developer may learn more and make bigger jumps learning here than staying with beginner materials.

### Tools

A few handy CSS tools, both for manual and automated testing.

* clean-css [package](https://www.npmjs.com/package/clean-css), to optimize and minify CSS
* CSS Minifier [online tool](https://cssminifier.com/), to minify CSS
* CSS Stats [online tool](https://cssstats.com/) and [script](https://github.com/cssstats/cssstats), to analyze and show data about style sheets
* CSS Validation Service [online tool](https://jigsaw.w3.org/css-validator/) and [script](https://github.com/w3c/css-validator), to validate CSS
* css-minify [package](https://www.npmjs.com/package/css-minify), to minify CSS
* CSSCheck [online tool](https://www.htmlhelp.com/tools/csscheck/), to validate CSS
* CSSJanus Left-to-Right-to-Left-ifyer [online tool](https://cssjanus.appspot.com/) and [script](https://code.google.com/archive/p/cssjanus/), to convert CSS directionality (LTR/RTL)
* CSSLint [online tool](http://csslint.net/) and [script](https://github.com/CSSLint/csslint), to identify CSS code issues
* CSSTidy [online tool](https://hell.meiert.org/aux/optimize/css/) and [script](http://csstidy.sourceforge.net/), to reformat and optimize CSS
* Minify [online tool](https://www.minifier.org/) and [script](https://github.com/matthiasmullie/minify), to minify CSS
* pre-commit [script](https://github.com/WouterSioen/pre-commit), to validate syntax errors in CSS (through CSS Lint) and SCSS (through SCSS Lint)
* Purgecss [package](https://www.purgecss.com/), to remove unused CSS
* purifycss [script](https://github.com/purifycss/purifycss), to remove unused CSS
* rm-unused-css [package](https://www.npmjs.com/package/rm-unused-css), to remove unused CSS
* UglifyCSS [package](https://www.npmjs.com/package/uglifycss), to minify CSS
* UnCSS [online tool](https://uncss-online.com/), [script](https://github.com/giakki/uncss), and [package](https://www.npmjs.com/package/uncss), to remove unused CSS
* Unused CSS [online tool](https://unused-css.com/), to remove unused CSS
* YUI CSS Compressor [online tool](https://hell.meiert.org/aux/compress/css/gui/) and [script](https://github.com/tubalmartin/YUI-CSS-compressor-PHP-port), to format and compress (minify) CSS

### Websites

A selection of CSS experts and resources for web development.

* [A List Apart](https://alistapart.com/)
* [Andrew, Rachel](https://rachelandrew.co.uk/)
* [Atkins Jr., Tab](https://www.xanthir.com/blog/)
* [Can I Use](https://caniuse.com/)
* [CSS-Tricks](https://css-tricks.com/)
* [Frain, Ben](https://benfrain.com/)
* [Heilmann, Christian](https://christianheilmann.com/)
* [Kinlan, Paul](https://paul.kinlan.me/)
* [Meiert, Jens Oliver](https://meiert.com/en/blog/categories/development/)
* [Meyer, Eric](https://meyerweb.com/)
* [Roberts, Harry](https://csswizardry.com/)
* [Smashing Magazine](https://www.smashingmagazine.com/)
* [W3C (Cascading Style Sheets)](https://www.w3.org/Style/CSS/)
* [Weyl, Estelle](http://www.standardista.com/)

### Books

An even smaller selection of books (my recommendation: [the specs](https://www.w3.org/TR/)).

* [_CSS Secrets: Better Solutions to Everyday Web Design Problems_ (Lea Verou)](https://www.amazon.com/dp/B0131MQ1NS/?tag=j9t-21-20)
* [_CSS: The Definitive Guide: Visual Presentation for the Web_ (Eric Meyer and Estelle Weyl)](https://www.amazon.com/dp/1449393195/?tag=j9t-21-20)
* [_CSS: The Missing Manual: The Missing Manual_ (David Sawyer McFarland)](https://www.amazon.com/dp/B0026OR2QI/?tag=j9t-21-20)
* [_The Little Book of HTML/CSS Frameworks_ (Jens Oliver Meiert)](https://www.oreilly.com/library/view/the-little-book/9781492048121/)