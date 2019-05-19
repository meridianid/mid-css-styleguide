![alt text][cover]
[![alt text][mission]](http://meridian.id)

# Meridian.id (S)CSS Styelguide

  1. [Overview](#overview)
  2. [General](#general)
      - [Don't](#donts)
      - [Spacing](#spacing)
      - [Formatting](#formatting)
  3. [Nesting](#nesting)
  4. [BEM](#bem)

## Overview

This is a styleguide for styling SCSS files at Meridian.id.

Please strictly follow the rules, unless you are really sure about what you are doing.

---

## General

### Don’ts

- Avoid using HTML tags in CSS selectors
  - E.g. Prefer `.container {}` over `div.container {}`
  - Always prefer using a class over HTML tags (unless you are doing some CSS resets)
- Don't use ids in selectors
  - `#header` is overly specific compared to, for example `.header` and is much harder to override
  - Read more about the headaches associated with IDs in CSS [here](http://csswizardry.com/2011/09/when-using-ids-can-be-a-pain-in-the-class/).
- Don’t nest more than 3 levels deep
  - Nesting selectors increases specificity, meaning that overriding any CSS set therein needs to be targeted with an even more specific selector. This quickly becomes a significant maintenance issue.
- Avoid using nesting for anything other than pseudo selectors and state selectors.
  - E.g. nesting `:hover`, `:focus`, `::before`, etc. is OK, but nesting selectors inside selectors should be avoided.
- Don't `!important`
  - Ever.
  - If you must, leave a comment, and prioritise resolving specificity issues before resorting to `!important`.
  - `!important` greatly increases the power of a CSS declaration, making it extremely tough to override in the future. It’s only possible to override with another `!important` declaration later in the cascade.
- Don’t use `margin-top`.
  - Vertical margins [collapse](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing). Always prefer `padding-top` or`margin-bottom` on preceding elements
- Avoid shorthand properties (unless you really need them)
  - It can be tempting to use, for instance, `background: #fff` instead of `background-color: #fff`, but doing so overrides other values encapsulated by the shorthand property. (In this case, `background-image` and its associative properties are set to “none.”
  - This applies to all properties with a shorthand: border, margin, padding, font, etc.

### Spacing

- Two spaces for indenting code
- Put spaces after `:` in property declarations
  - E.g. `color: red;` instead of `color:red;`
- Put spaces before `{` in rule declarations
  - E.g. `.modal {` instead of `.modal{`
- Write your CSS one line per property
- Add a line break after `}` closing rule declarations
- When grouping selectors, keep individual selectors on a single line
- Place closing braces `}` on a new line
- Add a new line at the end of .scss files
- Trim excess whitespace

### Formatting

- All selectors are lower case, hyphen separated aka “spinal case” eg. `.my-class-name`
- Always prefer Sass’s double-slash `//` commenting, even for block comments
- Avoid specifying units for zero values, e.g. `margin: 0;` instead of `margin: 0px;`
- Always add a semicolon to the end of a property/value declaration
- Use leading zeros for decimal values `opacity: 0.4;` instead of `opacity: .4;`
- Put spaces before and after child selector `div > span` instead of `div>span`

---

## Nesting

- As a general rule of thumb, avoid nesting selectors more than 3 levels deep
- Prefer using nesting as a convenience to extend the parent selector over targeting nested elements. For example:
  ```scss
  .navbar {
      padding: 24px;

      &--small {
          padding: 12px;
      }
  }

  // Will compiled into these
  .navbar {
    padding: 24px;
  }
  .navbar--small {
    padding: 12px;
  }
  ```

Nesting can be really easily avoided by smart class naming (with the help of BEM) and avoiding bare tag selectors.

---

## BEM

Block: Unique, meaningful names for a logical unit of style. Avoid excessive shorthand.
- Good: `.alert-box` or `.recents-intro` or `.button`
- Bad: `.feature` or `.content` or `.btn`

Element: styles that only apply to children of a block. Elements can also be blocks themselves. Class name is a concatenation of the block name, two underscores and the element name. Examples:
- `.alert-box__close`
- `.expanding-section__section`

Modifier: override or extend the base styles of a block or element with modifier styles. Class name is a concatenation of the block (or element) name, two hyphens and the modifier name. Examples:
- `.alert-box--success`
- `.expanding-section--expanded`

### BEM Best practices

Don't `@extend` block modifiers with the block base.
- Good: `<div class="my-block my-block--modifier">`
- Bad: `<div class="my-block--modifier">`

Don't create elements inside elements. If you find yourself needing this, consider converting your element into a block.
- Bad: `.alert-box__close__button`

Choose your modifiers wisely. These two rules have very different meaning:

```scss
.block--modifier .block__element { color: red; }
.block__element--modifier { color: red; }
```

[title]: https://raw.githubusercontent.com/meridianid/mid-css-styleguide/master/docs/title.png "Meridian.id CSS Styleguide"
[cover]: https://raw.githubusercontent.com/meridianid/mid-css-styleguide/master/docs/cover.png "Meridian.id CSS Styleguide"
[mission]: https://raw.githubusercontent.com/meridianid/mid-css-styleguide/master/docs/mission.png "Meridian.id"