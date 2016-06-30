# `{compago}`
> Yet another framework with influences from Atomic, BEM, & ITCSS.

Compago (working name) is design to be the ultimate CSS starting point that's
well suited to extensible UI development. It draws influence from several
different methods of managing CSS and brings the best of them all together.

## Contents
- [Installation](#installation)

- [Usage](#usage)

- [Documentation](#documentation)
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
Located in `/configuration/*.scss`

You should place variables for your project in the folder.


##### Utilities
Located in `/utils/*.scss`

Mixins and functions that consume the configs.

##### Generics
Located in `/generics/*.scss`

Resets, third party libs

##### Base
Located in `/base/*.scss`

Element styles e.g. h1, h2, h3, p, ul etc

##### Atomics
Located in `/atomics/*.scss`

Atomic, SRP (single responsibility principle) style classes

##### Objects
Located in `/objects/*.scss`

Re-usable UI patterns

##### Components
Located in `/components/*.scss`

Bespoke UI implementations

##### Immutables
Located in `/immutables/*.scss`

Stuff with !important in it

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

```
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
