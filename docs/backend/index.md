![Mind Yer Website](https://mindyerwebsite.co.uk/assets/img/mind_yer_app_primary_logo.svg)

# Back-end Coding Standards and Best Practices

a.k.a. *'How to do webdev at Mind Yer Website'*.

## Overview

These guidelines, principles and standards allow us to:

- produce code of a consistent quality across all projects we undertake
- work concurrently with multiple devs on the same codebase at the same time in the same way
- produce code that is less prone to bugs and regressions, is easier to understand and debug
- write code that supports re-use.

It is required reading for all Back-End devs working on a MYW project.

## Contributing

When considering coding standards we're more interested in **consistency** than **developer freedom**. However this should be considered a living document – it will evolve to reflect the changing needs of the MYW BE dev team and the work we do.

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

When you have been provided a design, part of your testing must be to compare the work you have done aginst that design.

To do this, get the design and build up side by side, and visually compare between the two. 


### Don't Repeat Yourself (DRY)

If you repeat anything that has already been defined in code, refactor it so that it only ever has one representation in the codebase.

If you stick to this principle, you will ensure that you will only ever need to change one implementation of a feature without worrying about needing to change any other part of the code.

### Separation of concerns

Separate *structure* from *presentation* from *behaviour* to aid maintainability and understanding.

- Keep CSS (presentation), JS (behaviour) and PHP (structure) in separate files

- Avoid writing inline CSS or Javascript in PHP

- Avoid writing CSS or HTML in Javascript

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

# PHP

### General guidelines

- Always use <?php ?> to delimit PHP code, not the <? ?> shorthand. This is required for PHP compliance and is also the most portable way to include PHP code on differing operating systems and setups.

- Block of declarations should be aligned.

- There should be only one statement per line unless the statements are very closely related.

- Methods should limit themselves to a single page of code.

- Functions should not keep static variables that prevent a function from being reentrant.

### Indentation

- Your indentation should always reflect logical structure. Use real tabs, not spaces, as this allows the most flexibility across clients.

- Exception: if you have a block of code that would be more readable if things are aligned, use spaces:

### Control Structures

These include if, for, while, switch, etc. Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls. You are strongly encouraged to always use curly braces even in situations where they are technically optional.

    //good
    if ((condition1) || (condition2)) {
      action1;
    }elseif ((condition3) && (condition4)) {
      action2;
    }else {
      default action;
    }

    //good 
    switch (condition) {
      case 1:
          action1;
          break;
      
      case 2:
          action2;
          break;
            
      default:
          defaultaction;
          break;
    }


### Function Definitions

- Function declarations follow the "BSD/Allman style" 

    function fooFunction($arg1, $arg2 = '') {
      if (condition) {
          statement;
      }
      return $val;
    }    

### Function Calls

- Functions should be called with no spaces between the function name, the opening parenthesis, and the first parameter; spaces between commas and each parameter, and no space between the last parameter, the closing parenthesis, and the semicolon.

    $var = foo($bar, $baz, $quux);

### Naming Conventions

- Use all lower case letters in variable, action/filter, and function names (never camelCase).

- Use '_' as the word separator.

- Files should be named descriptively using lowercase letters. Hyphens should separate words.

    my-plugin-name.php

### Commenting

C style comments (/* */) and standard C++ comments (//) are both fine. Use of Perl/shell style comments (#) is discouraged.

### Single and Double Quotes

- Use single and double quotes when appropriate. If you’re not evaluating anything in the string, use single quotes. You should almost never have to escape quotes in a string, because you can just alternate your quoting style.

    echo '<a href="/static/link" class="button button-primary">Link name</a>';
    echo "<a href='{$escaped_link}'>text with a ' single quote</a>";


### Writing include/require statements

- Because include[_once] and require[_once] are language constructs, they do not need parentheses around the path, so those shouldn’t be used. There should only be one space between the path and the include/require keywords.

- It is strongly recommended to use require[_once] for unconditional includes. When using include[_once], PHP will throw a warning when the file is not found but will continue execution, which will almost certainly lead to other errors/warnings/notices being thrown if your application depends on the file loaded, potentially leading to security leaks. For that reason, require[_once] is generally the better choice as it will throw a Fatal Error if the file cannot be found.

    // Correct.
    require_once ABSPATH . 'file-name.php';

    // Incorrect.
    include_once  ( ABSPATH . 'file-name.php' );
    require_once     __DIR__ . '/file-name.php';

### Remove Trailing Spaces

- Remove trailing whitespace at the end of each line. Omitting the closing PHP tag at the end of a file is preferred. If you use the tag, make sure you remove trailing whitespace.

- There should be no trailing blank lines at the end of a function body.

***

# Laravel

### General guidelines

***

# Version Control

All coding done at MYW must be done under Version Control

We use GitHub as our chosen VC system, as it has a native integration with Shopify

- Github 
  - Different edits to be done as different commits
  - Each card on Trello is a seperate branch. 1 branch per card

# Testing
- Proper testing - Check changes havnt affected anything else
  - Browser testign
  - What areas might your code have affected
  - Test all work in https://www.lambdatest.com/. Test latest versions of Chrome, IE, FF, Safari

# Coding Tools

  - VS - Has a bunch of PHP Tools