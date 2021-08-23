# Overview

CSS optimization is important because we, especially as individuals, don’t always write perfectly efficient, understandable, and maintainable code.

Writing quality code, however, is what makes us professionals.

CSS optimization does not entail “everything” that can be done with a style sheet; it entails what makes it more efficient, understandable, and maintainable, while looking for a good balance.

As professionals, we benefit from doing one (or two, or three, but not eighty-five) things really, really well; as web developers, it’s a good idea if CSS is one of those things.

It’s useful when we know our needs.

It’s sound when we develop for the present.

It makes our work easier when we keep it simple.

There’s nothing wrong with doing less work—by automating more of it.

There’s nothing wrong, either, with not doing any work, of a certain type—by automating all of it.

(There’s much wrong with not doing important work because we haven’t yet managed or automated the unimportant work.)

Code should be understandable and for that, it’s useful when it’s consistent and simple.

Consistent CSS is founded on alphabetical declaration sorting (everything else is too complicated) and on a robust order for selector sorting.

Simple CSS uses functional or generic names or avoids IDs and classes altogether.

Simple CSS also likes shorthands (yes).

Speed is important.

Selector performance doesn’t matter and inline CSS is a crime.

(Web development is not software development.)

Some declarations may be slower than others but there’s rarely reason for panic.

Rule hygiene may be most important for CSS performance.

The most basic way to determine quality is through validation, and high error counts mean low quality scores.

Every piece of code gets at least touched _twice_.

Web Design is a process.

For these last two observations, maintainability and maintenance are critical.

`!important` is not an obstacle to maintenance; it’s a tool.

One of the most important principles is separation of concerns. Content, structure, presentation, behavior are different concerns.

In code, we don’t want to repeat ourselves.

Accordingly, in CSS, we want to limit the repetition of declarations.

Optimization for production is an important second step because, in production, machines use our code whereas, in operation, humans use it.

When we cannot production-optimize automatically, we should do as much as we can manually, as part of our craft.

For production, we remove all unneeded characters. All of them.

We typically want to reference one style sheet that includes all styles, though there are cases of high complexity where a modular approach leads to better performance.

(We cannot be absolved from thinking and making decisions about our projects.)

(Exceptions prove the rule.)

We regularly review our CSS, both pre-production and in production.

We are professionals.

As professionals, we feel responsible, we hold ourselves accountable, and we set high ethical standards for ourselves.

And, as professionals, we lead by example.