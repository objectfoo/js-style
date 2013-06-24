# JS Style Guide

Lots of this is from [idiomatic][1].

* [Whitespace](#whitespace)
* [Syntax](#syntax)
* [Code quality](#code quality)
* [Variables](#variables)
* [Modules](#modules)


## Whitespace

Whitespace is your friend, use it to make code readable. Treat functions and control blocks like paragraphs, give them space to promote readability.

* indent with 4 spaces, no tabs
* never mix spaces and tabs
* add a blank line
    * between methods
    * between local variables in a method and it's first statement
    * before controls statements (if, for, while)
    * before a comment

Put comments above never at the end of a line.


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

Parenthesis, Braces and Line-breaks.

if, else, for while and try block always have spaces, braces and span multiple lines.

```javascript

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

Assignments, Declarations, Functions (Named, Expression, Constructor)

Use a single variable statement, put all variables at the beginning of the scope, right after your `'use strict';` statement, plain variable declarations first then variables with assignments.

Always use literals to create new Arrays or Objects. Prefer regular expression literal`/test/.test('testable')` to new Regexp();

```javascript
'use strict';
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
```

Include a blank line between variable assignments and other statements.

```javascript
var a = 3;

function foo () {
    // ...
}
```


## Code quality

Use strict mode for as much new code as possible and make sure your code passes [JsHint](http://www.jshint.com/), if it doesn't pass, and you must go against a hint, add the appropriate [JsHint option](#enforcing_options) to make it pass.

```javascript
/*global jQuery*/
(function ($) {
    'use strict';
    var module = {
        prop: false
    };

    function toggleProp() {
        /*jshint validthis: true*/  // <-- using 'this' ok for this function
        this.prop = !!this.prop;    // <-- jshint: possible strict mode violation
    }

    toggleProp.apply(module);
}(jQuery));
```

## Variables

Use a single variable statement at the beginning of a scope. Organize variables with declarations first, declarations with assignments second. Avoid meaningless variable names, function names should begin with a verb and variable names should begin with a noun.

## Modules

Augmenting an existing name space object or module.

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

Creating a standalone module.

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

Making a module testable.

We use QUnit, so if QUnit is defined then we probably don't want to run our normal initialization function.

```javascript
var theModule = (function (document, my, QUnit, undefined) {
    'use strict';
    var helper = function () {
        // be helpful
    },

    initialize = function () {
        // initialize
    };

    if (!QUnit) {
        // initialize as normal if no QUnit
        initialize();
    } else {
        // expose normally private functions for testing
        my.helper = helper;
        my.initialize = initialize;
    }

    return my;
}(document, theModule || {}, QUnit));
```
