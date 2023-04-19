![Mind Yer Website](https://mindyerwebsite.co.uk/assets/img/mind_yer_app_primary_logo.svg)

# Back-end Coding Standards and Best Practices

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

==
VERY IMPORTANT! Remember this above all else
==

- Code is a craft - make it your responsibility to ensure it is the best it can be; that it's tested, bug free, and adheres to these guidelines. Testing and QA folks aren't responsible for quality - developers are.

- Don't use testers as bug catchers - testers should find no problems after you have committed your code.  When testers find bugs, tickets need to be opened, developers assigned and scheduled in to fix the problem.  This lengthens the time it takes from identifying to resolving a bug.

- Make sure, as much as possible, you have tested your code on a reasonable number of devices so you can catch problems before you commit to the repo.


### Design

We dont provide designs for all projects, however, when we do, they have been viewed and approved by the client, meaning the work we produce must match that design

We are never going to a build pixel perfect against a design, its just not realistic, however, it needs to be as close as possible.

When you have been provided a design, part of your testing must be to compare the work you have done aginst that design.

To do this, get the design and build up side by side, and visually compare between the two. 


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

# JS

### General guidelines

- Unless the site is already using jQuery, dont use it. Use vanilla Javascript instead.

- Use soft-tabs with a two space indent.

### Naming conventions

- Use descriptive yet concise variable names for long-lived variables e.g. `customer_name`

- Avoid using what might be considered reserved variable names out of context.  For example, `e` in javascript is considered an event object.  Don't use it for anything else.

- For temporary variables, i.e. those which are used to store short-lived values, e.g. variables used for iteration, it is ok to use non-descriptive names, e.g. `i, j, k`.

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

# PHP

### General guidelines

***

# Laravel

### General guidelines

***

# Version Control

All coding done at MYW must be done under Version Control

We use GitHub as our chosen VS system, as it has a native integration with Shopify

- Github 
  - Different edits to be done as different commits
  - Each card on Trello is a seperate branch. 1 branch per card

# Testing
- Proper testing - Check changes havnt affected anything else
  - Browser testign
  - What areas might your code have affected
  - Check other elements that dont comply e.g. if you add/edit a metafield on the PDP, make sure to check products which dont have that metafield to make sure it still works
  - Test all work in https://www.lambdatest.com/. Test latest versions of Chrome, IE, FF, Safari

# Coding Tools

  - VS - Has a bunch of PHP Tools