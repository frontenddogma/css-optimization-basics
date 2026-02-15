# Development Mindsets

We all know the adage, “Give a man a fish, and you feed him for a day; teach a man to fish, and you feed him for a lifetime.” To me, we feed developers for a lifetime by teaching and cherishing certain tenets or _mindsets_. By themselves, they aren’t enough, but I view them as the foundation that shapes our work and our careers. They’re not all related to CSS optimization—that would be odd given that we’re dealing with so many different technologies—, but they’re generally useful. Let’s look at the key ones.

## Do One Thing Really, Really Well

Out of [the Google book](https://about.google/philosophy/), one guiding idea is to “do one thing really, really well.” We do end up with more than one thing, but for us as web developers, this thing should be _web development_.

To do one thing really well means to immerse ourselves in web development, to practice it, to understand it, to practice it more, to master it. Optimizing CSS is part of writing CSS well which is part of doing web development well, and that’s why this mindset is important for us. The goal to do web development well is an idea that serves us in our work.

## Know Your Needs

An idea occasionally forgotten, and not strictly followed, is the one of knowing our project needs—and of knowing these needs well. It’s also the idea of knowing our _goals_, or having goals in the first place—because our goals determine the specific needs we have.

Knowing our goals and needs is important because it’s difficult to meet a goal when we don’t know it, and to satisfy a need that we’re ignorant of. In the web development world, there are many goals and needs we may have. They go from our fundamental understanding of maintenance (shall it be [“fire and forget”](https://meiert.com/blog/fire-and-forget/) or an iterative process?) to our preferences around frameworks (which ones [help us without introducing bloat](https://www.oreilly.com/library/view/the-little-book/9781492048121/)?) to our ambitions for output quality.

## Stay in the Present

Without becoming philosophical, another useful mindset is to [stay in the present](https://meiert.com/blog/develop-for-what-is/), to stay in the now. This means both a keen eye to get rid of everything (documentation, design patterns, code snippets, libraries, &c.) that we don’t need and use anymore (“Know Your Needs”), as well as not to bother coding something that we don’t know is needed _with certainty_.

This mindset matters because it keeps our codebase and our documentation clean, and hence contributes to our focus (“Do One Thing Really, Really Well,” “Keep It Simple”).

## Keep It Simple

The idea to keep it simple has a lazy touch, yet requires a high level of skill. Keeping it simple means to _focus_, to know what’s important, and through that, to be efficient. Keeping it simple does not mean to do less; it means to _do what matters_.

As such, keeping things simple requires that we thoroughly understand our field—the core technologies, first and foremost, but everything in between and to the sides as well. And it means economy of motion, because we don’t want to engage in something we don’t need to do.

As a mindset, keeping it simple is truly grandiose. To dive deeper, you may not need to start with a book on simplicity or minimalism, but rather one about focus—my recommendation is Gary Keller’s [_The One Thing_](https://www.the1thing.com/).

## Automate

Lastly, a most powerful mindset is the one to automate. Every step of our work should, if possible, be automated. Sometimes that will be obvious—every time after we made a CSS change we run an optimization script, so let’s automate this step. Sometimes that will require a bit of listening—a team member mentions how they manually update documentation each time someone reports a downtime issue. At other times it will be obscure—no one on the team realized there was the option to automate visual regression testing.

Whenever we repeat something in our work, we should look into whether that repeat work can be automated: Is there a tool for this task? Can we script this?

Automation is powerful because it makes us more efficient and allows us to tackle more important priorities. However, automation also requires vigilance. Personally, I work with a recurring reminder to review work processes for automation options. Everything that keeps us mindful of automation, helps.