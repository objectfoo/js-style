# Guide

* [Style](#style)
    * [Whitespace](#whitespace)
    * [Syntax](#syntax)
* [Best Practices](#best-practices)
    * [Code quality](#code-quality)
    * [Variables](#variables)
    * [Modules](#modules)

---

## Style

### Whitespace

use whitespace to make code readable. Treat functions and control blocks like paragraphs.

* indent with 4 spaces, no tabs
* never mix spaces and tabs

Blank lines

* between methods
* between local variables in a method and it's first statement
* before controls statements (if, for, while)
* before a comment

```javascript

// Blank lines promote readability
function money() {
    var truth = true;

    function foo () {
        // ...
    }
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
}
```

Put comments above, not at end.

``` javascript

// comment above
money();

```

### Syntax

Parenthesis, Braces and Line-breaks.

if, else, for while and try block always have spaces, braces and span multiple lines. Place opening parenthesis on same line. Always include semi-colons.

```javascript

// BAD
if (true) execute();
while (condition) iterate();
for (var i = 0; i < array.length; i++) process(a[i]);

// GOOD
if (true) {
    // ...
}

for (var i = 0, len = array.length; len < i; i++) {
    // ...
}

// better
var i = 0,
len = array.length;

for (; i < len; i++) {
    // ...
}
```

Assignments, Declarations, Functions (Named, Expression, Constructor)

```javascript
// ...
```
---

## Best practices

### Code quality

Use strict mode for new code and make sure your code passes [JsHint](http://www.jshint.com/), if it doesn't pass, and you must go against a hint, add the appropriate [JsHint option](http://jshint.com/docs/#enforcing_options) to make it pass.

```javascript
// tell JsHint is a valid global variable
/*global jQuery*/
(function ($) {
    'use strict';
    var module = {
        prop: false
    };

    function toggleProp() {
        /*jshint validthis: true*/

        // overlook possible 'this' strict mode violation
        this.prop = !!this.prop;
    }

    toggleProp.apply(module);
}(jQuery));
```

### Variables

Use a single variable statement, put all variables at the beginning of the scope, right after your `'use strict';` statement. Avoid meaningless variable names, function names should begin with a verb and variable names should begin with a noun.

Always use literals to create new Arrays or Objects. Prefer regular expression literal`/test/.test('testable')` to new Regexp();

```javascript
// bad
var foo = false,
    title = ['one', 'two'],
    test = new RegExp('test');

// good
`'use strict';`
var isVisible = false,
    stepNames = ['one', 'two'],
    reTest = /test/;
```

### Modules

#### Standalone module

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

#### Augment existing name space or module

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

#### Making a module testable

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
        // expose normally private functions for testing if needed
        my.helper = helper;
        my.initialize = initialize;
    }

    return my;
}(document, theModule || {}, QUnit));
```
