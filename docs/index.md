![Mind Yer Website](https://mindyerwebsite.co.uk/assets/img/mind_yer_app_primary_logo.svg)

# Front-end Coding Standards and Best Practices

a.k.a. *'How to do webdev at Mind Yer Website'*.

## Overview

These guidelines, principles and standards allow us to:

- produce code of a consistent quality across all projects we undertake
- work concurrently with multiple devs on the same codebase at the same time in the same way
- produce code that is less prone to bugs and regressions, is easier to understand and debug
- write code that supports re-use.

It is required reading for all Front End devs working on a MYW project.

## Contributing

When considering coding standards we're more interested in **consistency** than **developer freedom**. However this should be considered a living document – it will evolve to reflect the changing needs of the MYW FE dev team and the work we do.

### How to contribute

- Branch the repo and submit your changes as a Pull Request. These changes will be reviewed by a senior developer, and if agreed, will be merged into the main branch

***

## Global Development Guidelines

### Testing and QA should find no problems

==VERY IMPORTANT! Remember this above all else==

- Code is a craft - make it your responsibility to ensure it is the best it can be; that it's tested, bug free, and adheres to these guidelines. Testing and QA folks aren't responsible for quality - developers are.

- Don't use testers as bug catchers - testers should find no problems after you have committed your code.  When testers find bugs, tickets need to be opened, developers assigned and scheduled in to fix the problem.  This lengthens the time it takes from identifying to resolving a bug.

- Make sure, as much as possible, you have tested your code on a reasonable number of devices so you can catch problems before you commit to the repo.

### Don't Repeat Yourself (DRY)

If you repeat anything that has already been defined in code, refactor it so that it only ever has one representation in the codebase.

If you stick to this principle, you will ensure that you will only ever need to change one implementation of a feature without worrying about needing to change any other part of the code.

### Separation of concerns

Separate *structure* from *presentation* from *behaviour* to aid maintainability and understanding.

- Keep CSS (presentation), JS (behaviour) and HTML (structure) in separate files

- Avoid writing inline CSS or Javascript in HTML

- Avoid writing CSS or HTML in Javascript

- Don't choose HTML elements to imply style e.g. <b>, <i> etc

- Where appropriate, use CSS rather than Javascript for animations and transitions

- Try to use templates when defining markup in Javascript

### Write code to be read

> Debugging is twice as hard as writing the code in the first place.  Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it. - Brian Kerninghan.

Follow the principles of ['Keep It Simple, Stupid'](http://en.wikipedia.org/wiki/KISS_principle) (KISS); hard to read or obfuscated code is difficult to maintain and debug.  Don't be too clever; write code to be read.

### Commenting

Your code should be easy to read and understand on its own, but its also important to comment your code.

Rather than commenting every line of code, add a code block at the top of the function. If there is a specific set of code that is especially complex, then you can comment line by line for that code only.

Be verbose with your comments but ensure:

- Your comments add something to the code, they don't just repeat what is there

- They are kept up to date, if you change something that has been commented, ensure you up date the comment as well

- If code needs extensive commenting, can it be refactored to make it less complex / easier to understand?

- You focus on *why* rather than *how* - unless your code is too complex, it should be self documenting

Don't leave commented out chunks of code in the codebase. It makes the code look unfinished, and can be confusing for other developers.

***
# CSS

CSS should be modular and reusable. Its always best to extend off the existing code and overwrite the bits that need to be changed, than recreating the same styles over and over again.

### General Guidelines

- Utilise [BEM's](http://coding.smashingmagazine.com/2012/04/16/a-new-front-end-methodology-bem/) 'Block', 'Element', 'Modifier' methodology

- Everything we do is responsive. Code needs to work and look good across all screen sizes, not just desktop and mobile.

- Use `id` selectors only when explicitly required – they prohibit re-use, and may need to be re-written during further code changes.

- Use short hex values where applicable, e.g. `#fff` instead of `#ffffff`

- Use CSS variables appropriately to ensure you code is kept DRY

    ```
    // no
    h3 {
      color: white;
    }

    // yes
    --color-white: #fff;

    h3 {
      color: var(--color-white);
    }

    ```

- Each selector and style declaration should be on its own line to help with Git diffs and error reporting.

    ```
    // good
    h3,
    .gamma,
    %gamma {
      font-size: var(--h3-font-size);
      line-height: var(--heading-line-height);
    }

    // not good
    h3, .gamma, %gamma {
      font-size: var(--h3-font-size);
      line-height: var(--heading-line-height);
    }
    ```

- Don't specify units for zero values, e.g. `margin: 0;` instead of `margin: 0px;`

- Use `0` instead of `none`, e.g. `border: 0;` rather than `border: none;`.

- Avoid inline CSS.

- Use shorthand properties:

    ```
    // no
    margin: 1px 1px 1px 1px;

    // yes
    margin: 1px;

    // no
    margin: 0 0 20px 0;

    // yes
    margin: 0 0 20px;
    ```

- Write colours in uppercase:

    ```
    // yes
    color: #1AB2C0

    // no
    color: #1ab2c0

    ```

- Omit protocols from external resources to prevent unintended security warnings through accidentally mixing protocols, and for small file size savings:

    ```
    // nope
    .main-navigation {
      background: url(http://d111111abcdef8.cloudfront.net/images/image.jpg);
    }

    // yes
    .main-navigation {
      background: url(//d111111abcdef8.cloudfront.net/images/image.jpg);
    }
    ```

- Use whitespace to aid readability. Anything which modifies the context such as a selector or a media query should be preceded with a blank line.

  ```
  // bad
  .foo {
    color: $blue;
    @media screen and (min-width: 1000px) { 
      color: $yellow;
    }
    .bar {
      color: $red;
      @media screen and (min-width: 1000px) { 
        color: $green;
      }
    }    
  }
  ```

  ```
  // good
  .foo {
    color: $blue;

    @media screen and (min-width: 1000px) { 
      color: $yellow;
    }

    .bar {
      color: $red;

      @media screen and (min-width: 1000px) { 
        color: $green;
      }
    }
  }
  ```

### Depth of applicability

Don't over-specify CSS selectors. Overly specified selectors are difficult to understand and lead to subsequent selectors needing to be of an even higher specificity. (See SMACSS' [depth of applicability](http://smacss.com/book/applicability)):

```
// nope
#sidebar div ul > li {
  margin-bottom: 5px;
}
```

The above example is tightly coupled to the HTML structure which prevents re-use and is brittle - if the HTML needs changing, then the style will break.

### Commenting

Use comments to:

- Explain design or architectural decisions, to make notes so that any developers modifying, extending or debugging the code can do so understanding your original decisions.

- Divide up groups of declarations using standard block and single line comment formats.

    ```
    /*
     * This is a "block" comment carrying a bit more weight
     * Maybe it has multiple lines
     * It often announces a new section of some kind
     */
    
    // Single line explanation of something
    ```
### Unit sizing

Use `rem`s to size fonts. These will take into account the user's font size setting ([this research from 2006 suggests around 10% of people have changed it](http://archive.oreilly.com/pub/post/more_statistics_on_user_clicks.html)). 

Use unitless line-heights.

Use flexbox to create layouts and grids

Use `pixels` to specify the following properties unless percentages make sense (but as above, exercise good judgement): `margin`, `padding`, `top`, `left`, `bottom`, `right`.

```
//  This makes sense
.dropdown-toggle:hover > .dropdown-menu {
  display: block;
  top: 100%; // display just below dropdown-toggle
}

//  This doesn't (magic number alert! - http://csswizardry.com/2012/11/code-smells-in-css/#magic-numbers)
.dropdown-toggle:hover > .dropdown-menu {
  display: block;
  top: 62px; // height of dropdown-toggle at present
}
```

***

# HTML Markup

### General Guidelines

- Use well-structured, semantic markup.

- Use double quotes on all attributes.

- Use soft tabs, 2 space indents.

- Ensure you write valid HTML.

- Omit protocols from external resources to prevent unintended security warnings through accidentally mixing protocols:

    ```
    <!-- Don't do -->
    <script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>

    <!-- Do -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
    ```

### Write semantic markup

Ensure the markup you write is relevant and has meaning in the context of the content it is being applied to. Don't use markup to infer style.

```
<!-- bad: -->
<div class="mainHeading">My Blog</div>
<br /><br />
... content ...
<br /><br />

<!-- bad: -->
<h1>I want to draw attention to this as I am important</h1>
<h1>and so am I</h1>

<!-- good: -->
<h1>My Blog</h1>
<p>
   ... content ...
</p>
```

### Input labels

Use `label` tags for `input` fields so that the input element acquires focus when the label is clicked.

When using labels, try to use the wrapping pattern rather than the `for` attribute so we can avoid using  `id`s which may interfere with integration with backend systems:

```
<label>Address
  <input type="text" name="address" />
</label>

<label for="address">Address</label>
<input type="text" id="address" name="name" />
```

### Boolean attributes

Use the single word syntax for boolean attribute values to aid readability, reduce clutter and prevent unnecessary bytes going down the wire.

The presence of the attribute itself implies that the value is "true", an absence implies a value of "false":

```
// no
<option selected="selected">value 1<option>

// yes
<option selected>value 1<option>
```

***

# JS

### General guidelines

- Unless the site is already using jQuery, dont use it. Use vanilla Javascript instead.

- Use soft-tabs with a two space indent.

- Avoid applying styles with Javascript, it is better practice to add or remove classes.  Keep style in CSS to make it easier to maintain and debug.

    ```
    //  no good
    <span style="display:none;" name="address_1">Icon label text</span>
    ```

- Use `is-*` or `has-*` state rules to apply state to elements, for example `class='is-visually-hidden'` `class='has-icon'`.

    ```
    //  all good
    <span class="is-visually-hidden has-icon">Icon label text</span>
    ```

- Don't recreate functionality that may already be present in a utility library that is already in use.

- Always use parentheses in blocks to aid readability:

    ```
    // good...
    while (true) {
      shuffle()
    }

    // not good...
    while (true)
      shuffle()

    // also not good...
    while (true) shuffle()
    ```

- Use the `===` comparison operator to avoid having to deal with type coercion complications.

- Use quotation marks consistently, e.g. only use single or double quotes throughout your code, don't mix. Unless there is a valid reason not to, prefer single quotes such that HTML contained therein does not need to be escaped. For example:

      ```
    // good...
    const foo = 'Just a normal string'

    // good...
    const foo = '<a href="/bar">Nice clean HTML string</a>'

    // not good...
    const foo = "<a href=\"/bar\">HTML string with escaped double quotes</a>"

    ```

- Use `event.preventDefault()` instead of `return false` to prevent default event actions. Returning a boolean value is semantically incorrect when considering the context is an event.

    ```
    //  returning false doesn't make sense in this context
    htmlElement.addEventListener('click', (e) => {
      // do stuff
      return false
    })

    // use preventDefault
    htmlElement.addEventListener('click', (e) => {
      e.preventDefault()
      // do stuff
    })

    ```

- Don't use `var` any more - use `let` In JavaScript, `const` means that the identifier can’t be reassigned. `let` is a signal that the variable may be reassigned, it also signals that the variable will be used only in the block it’s defined in.

- single let pattern:

    ```
    // single let pattern:
    let mylet1 = 1,
        anotherlet2 = 'test',
        andAnotherlet = true;

    // good old dependable multiple let pattern:
    let myLet = 1;
    let anotherLet2 = 'test';
    let andAnotherLet = true;

    ```
### Avoid excessive function arguments

If a function requires more than three arguments, considering refactoring to use a configuration object:

```
// bad
let myFunction1 = function(arg1, arg2, arg3, arg4) {}

myFunction1('firstArgument', argument2, true, 'My Third Argument')

// good
let myFunction2 = function(config) {}

myFunction2({
  arg1: 'firstArgument',
  arg2: argument2
  arg3: true,
  arg4: 'My Third Argument'
})
```

Configuration objects:

- allow for optional parameters,

- are easier to read,

- are easier to maintain.

### Naming conventions

Use descriptive yet concise variable names for long-lived variables e.g. `customer_name`

Avoid using what might be considered reserved variable names out of context.  For example, `e` in javascript is considered an event object.  Don't use it for anything else.

For temporary variables, i.e. those which are used to store short-lived values, e.g. variables used for iteration, it is ok to use non-descriptive names, e.g. `i, j, k`.

### Commenting

Comment your code.  There are two reasons why you should comment:

- Inline comments explain design or architectural decisions that cannot be conveyed in code alone.  These are mainly for the benefit of other developers modifying, extending or debugging the code, but also for you - you may return to the code a week later and wonder how it works.

    ```
    /**
     * I am a nicely formatted comment
     */

    // I am a nicely formatted brief one-line comment

    for ( let i=0; i<10; i++); // uh-oh don't put comments at the end of lines

    /* ===================================================
     * uh-oh don't make up your own comment format
     * ==================================================*/

    //  This is a long comment
    //  that shouldn't really
    //  be using the one-line
    //  comment syntax.

    ```
### Break code into separate lines

Where applicable, ensure code is written on separate lines to aid Git diffs and error reporting:

     // good
    page.setViewport({
      width: 1280,
      height: 1024
    })

     // not so good
    page.setViewport({width: 1280, height: 1024})


***

- Seperate into HTML, CSS, JS
- Dont edit existing styles, overwrite so can be easily removed in future if needed
- Never use inline styles. Styles should always go into a CSS file ( or if using Dawn, less than 3 styles can go into the "styles" block )
- Proper testing - Check changes havnt affected anything else
  - Browser testign
  - What areas might your code have affected
  - Check other elements that dont comply e.g. if you add/edit a metafield on the PDP, make sure to check products which dont have that metafield to make sure it still works
  - Test all work in https://www.lambdatest.com/. Test latest versions of Chrome, IE, FF, Safari
- Where a design is provided, testing needs to be done to check that the work you have done matches that design as closely as possible
- Shopify specific rules
- Github 
  - Different edits to be done as different commits
  - Each card on Trello is a seperate branch. 1 branch per card

