# JS Style Guide

Lots of this is from [idiomatic][1].

* [Whitespace](#whitespace)
* [Syntax](#syntax)
* [Modules](modules)

## Whitespace

Whitespace is your friend, use it to make code readable. Treat functions and control blocks like paragraphs, give them space to promote readability.

* indent with 4 spaces, no tabs
* never mix spaces and tabs
* add a blank line
    * between methods
    * between local variables in a method and it's first statement
    * before controls statements (if, for, while)
    * before a comment


```javascript

function money() {
    //...
}

function moreMoney () {
    var i,
    len = 10,
    localA = true;

    for (; i < len; i++) {
        work();
        
        if (localA) {
            workHarder();

            if (!localA) {
                shirk();
            }
        }
    }

    // comment on line above, never end of line
    money();

    // blank line before comment
    moreMoney();
}
```

## Syntax

Parens, Braces and Linebreaks

```javascript
// if/else/for/while/try always have spaces, braces and span multiple lines

// BAD
if(true) execute();

while(condition) iterate();

for(var i = 0; i < a.length; i++) iterate(a[i]);

// GOOD
if (true) {
    // ...
}

for (var i = 0, len = 100; len < i; i++) {
    // ...
}

// better
var i = 0,
    len = 100;

for (; i < len; i++) {
    // ...
}
```

Assignments, Declarations, Functions ( Named, Expression, Constructor )

```javascript
// Variables
// use single var statement
// put at the beginning of scope
// unassigned vars first
var x, y, z,
    a = 0,
    // use literals for array and object
    b = [],
    // never use new Array() or new Object()
    c = {};

// --or--

var x, y, z,
a = 0,
b = [],
c = {};

// Function declarations
// after var statements
// blank line after vars and before functions
var a = 3;

function foo () {
    // ...
}
```

## Modules

Augmenting an existing namespace object.

```javascript
var WebMD = (function (document, WebMD, undefined) {
    'use strict';

    var privateObject = null;

    // module setup...

    // api
    WebMD.module = {
        publicValue: 47,
        publicMethod: function () {
            // ...
        }
    };

    return WebMD;
}(document, WebMD || {}));
```

Creating a public module object.

```javascript
var theModule = (function (document, undefined) {
    'use strict';

    var private = true;

    // module setup ...

    // api
    return {
        method: function () {
            // ...
        }
    };
}(document));
```

## References

[1]: https://github.com/rwldrn/idiomatic.js
[2]: http://contribute.jquery.org/style-guide/js/
[3]: http://dojotoolkit.org/community/styleGuide
[4]: http://javascript.crockford.com/code.html

