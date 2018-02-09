# Production Optimization

For production, we usually take care of all the things that are good for machines. I’ve organized this section so that it also contains the things that can be done _by_ machines (tools)—but not, again with an eye on us as professionals, that it does contain nothing that, if we were to miss it, would make us produce significantly worse code.

However, we do benefit again from diligence and discipline by trying to follow some of the human-friendly ideas ourselves. For example, we can well try to write minimal CSS (like omitting leading 0s), or to only link one style sheet anyway (to eventually keep the number of requests low and to avoid future HTML changes). If there’s something of particular interest to us even if we cannot readily automate it, I’ll point that out.

## Performance

Performance is one of the primary optimization goals, and again _rendering_ performance is not the subject here for its often marginal achievements for grave practical impediments.

As long as our code is consistent, the steps suggested here can all be taken care of just before production, automatically, and they don’t have to find their way back into the production repository. The exception is perhaps what we’ll start with because these items can well be handled manually, and get covered by our code style guides.

### Character Minimization

To make our style sheets more compact, that is, make them easier to read and smaller in size, we remove all unneeded characters. That does not refer to whitespace and comments yet—let’s make this a separate step, although both can be covered by the same tool—, but to removing anything CSS that is not strictly needed. This entails:

* semicolons after the last declaration of each rule;
* leading `0`’s (`margin: .1em`, not `margin: 0.1em`);
* unneeded trailing `0`’s (`line-height: 1`, not `line-height: 1.0`);
* color notations to use 3-digit hex, where possible (`#fff`, not `#ffffff` or `white`);
* value shortening (`border: 0` instead of `border: none` but also (these steps aren’t trivial!) `font-family: arial, sans-serif` instead of `font-family: arial, helvetica, sans-serif`—the fallback font is good practice but Helvetica, here, would never be used).

As noted in the introductory section, these items can well be covered by coding guidelines but they’re also easy enough to automate and run through just before pushing our style sheets to production.

@@