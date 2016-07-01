# `{compago}`
> Yet another framework with influences from Atomic, BEM, & ITCSS.

Compago (working name) is designed to be a starting point that's well
suited to extensible UI development. It draws influence from several
different methods of managing CSS and brings the best of them all together.

## Contents
- [Installation](#installation)

- [Usage](#usage)

- [Documentation](#documentation)
  - [Namespaces](#namespaces)
  - [Structure](#structure)
  - [Configuration](#configuration)
  - [Utilities](#utilities)
  - [Generics](#generics)
  - [Base](#base)
  - [Atomics](#atomics)
  - [Objects](#objects)
  - [Components](#components)
  - [Immutables](#immutables)


- [Influences](#influences)

---

### Installation
Currently, just clone this repository & copy it into your styles
folder. In the future, a version of this framework will be distributed that
doesn't contain this README and other non-relevant files to save you from
having to do so yourself.

---

### Usage

###### Customisation
Any given layer of Compago can be added or removed at will. However, regardless
of the structure you decide on, you should order your styles in specifity order,
like [ITCSS](http://csswizardry.net/talks/2014/11/itcss-dafed.pdf) would have
you do.

###### Assumptions
Compago assumes that you'll be writing in SCSS. This is *not* a requirement;
you could use LESS, SASS, Stylus, or even vanilla CSS (it is recommended
that you use a pre-processor or at the very least, a minifier) so long as you
add and remove layers from Compago where necessary.

###### Style composure
As long as you're not writing an [atomic](#atomics) or a [generic](#generics),
you should use [BEM](#bem) to compose your styles.

###### Variables & private variables
A good starting point would be the `config/_vars` file. You should place all
your variables that you'll need global access to in here.

In some cases, you will need to define private variables on a per-file basis.
You should try and avoid using too many of these as they will make your
components less re-usable.

---

### Documentation

##### Namespaces

Namespacing your styles is important. It provides instant feedback about what a
given classname does and what it is likely to affect.

- `a-` - Atomic style
- `o-` - Object
- `c-` - Component
- `i-` - Immutable
- `is-, has-` - Stateful (used for stateful styling)
- `js-` - JS binding (for targeting with JavaScript)

One added bonus you get from namespacing your classnames is that while you are
authoring your UI, most auto-complete features in editors will hint all classes
belonging to a given namespace.

##### Structure
The structure of Compago is as follows.

```
compago/
├─ atomics/
├─ base/
├─ components/
├─ config/
   ├─ _vars.scss
├─ generics/
├─ immutables/
├─ objects/
├─ utils/
├─ .scss-lint.yml
```

Included with compago is a `.scss-lint.yml` file for use with [scss-lint](https://github.com/brigade/scss-lint). You should distribute this file amongst your team and use `scss-lint` so you all write consistent styles.

##### Configuration
> `/configuration/*.scss` - *Variables 'n such*

You should place variables for your project in this folder. If you have lots of
sets of similar data, for example a colour palette, or margins/paddings, then
it's a good idea to define them as a map;

``` scss
$cfg-palette: (
  'primary': #2dd3d3,
  'negative': #b3343a,
  'positive': #5ada55
)
```

Maps in SCSS are iterable, which makes generating styles with an `@each`
possible. Accessing values by key using `map-get` is also good practice.

##### Utilities
> `/utils/*.scss` - *Mixins and functions that consume the configs*

Most of the mixins/functions that you write should help retrieve values from
your configuration files. Try and avoid writing a mixin if it exposes very
few styles. An [atomic](#atomics) would be better in that case.

##### Generics
> `/generics/*.scss` - *Resets & third party libs*

Generics have the possibility of imposing very
greedy styles and should be added as little as possible. A reset is perhaps
the only acceptable use case where far-reaching & greedy styles are acceptable.
Grid systems are also classed as a generic.

##### Base
> `/base/*.scss` - *Element styles e.g. h1, p, ul*

Base styles should also be used at a minimum, as most of your base element
styling should take place in your reset, with the exception of typography.
Attaching styles to base elements can severely reduce their re-usability.

##### Atomics
> `/atomics/*.scss` - *Atomic style classes, without the terseness*

*Namespace:* `a-`

This is where you should write classes that do one thing and one thing only.
It is a good idea to generate your atomics based on the contents of your
configuration files, using mixins & functions that you author in the utils
folder.

##### Objects
> `/objects/*.scss` - *Re-usable UI patterns*

*Namespace:* `o-`

Objects represent a repeatable UI pattern that should work in any given
context, regardless of its scope. You should author objects with immutability
and extensibility in mind. Once you have authored an object, you should never
modify the core styles related to it, as refactoring an object that is already
widely used will most likely cause unexpected behaviour.

You should only extend an object using a BEM modifier
(`--` delimited classname). This way you can change the behaviour of an
object class without worrying about it affecting the base object.

##### Components
> `/components/*.scss` - *Bespoke UI implementations*

*Namespace:* `c-`

Components are bespoke, implementation-specific pieces of UI. In most cases,
you should use component classes to structure the layout of a given piece of
UI. Components can be used in conjunction with [atomics](#atomics) and
[objects](#objects) to add context-specific modifications.

An example:

``` html
<div class="o-avatar c-profile-avatar">
  This is a base avatar layout (.o-avatar) with additional modifications
  imposed by the component-specific implementation (.c-profile-avatar).
</div>
```

##### Immutables
> `/immutables/*.scss` - *Stuff with `!important` in it.*

*Namespace:* `i-`

It's pretty common knowledge that using `!important` is bad practice, as it
is a very ham-fisted way of ensuring that a property does exactly what you
want. There is however, one use-case for `!important` being acceptable, and
this is for proactive use, as opposed to reactive use.

An almost painfully simple example:

``` css
.i-hidden {
  display: none !important;
}
```

A class of `i-hidden` should absolutely hide the element you apply it to every
single time. This is an example of proactive usage of `!important`.

---

### Influences
##### Atomic
Atomic's style presents you with many classes that all serve a single
purpose. They obey the [single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)
(SRP), which is a paradigm of good-practice programming. Using this in CSS
seems absolutely sensible.

This framework's [atomics](#atomics) are inspired by Atomic and also follow
the SRP, but does away with the extremely terse nature of their classnames,
which make readability and their implied effects difficult to read at a glance.

##### BEM
BEM is [Block, Element, Modifier](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).
Acceptable classname composure is below;

``` css
.block {}
.block--modifier {}
.block__element {}
.block__element--modifier {}
```

BEM is used when building components & objects, but does not apply to atomics
within the purview of this framework. BEM-built class composure is still
very re-usable, but doesn't come close to the re-usability of
[atomics](#atomics).

##### ITCSS
The structure of this framework is greatly influenced by Harry Roberts'
[ITCSS](http://csswizardry.net/talks/2014/11/itcss-dafed.pdf).

---
