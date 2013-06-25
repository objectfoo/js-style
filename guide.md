# Guide

* [Style](#style)
    * [Whitespace](#whitespace)
    * [Naming](#naming)
    * [Syntax](#syntax)
* [Best Practices](#best-practices)
    * [Code quality](#code-quality)
    * [Variables](#variables)
    * [Modules](#modules)

---

## Style

### Whitespace

* indent with 4 spaces, no tabs
* never mix spaces and tabs

Blank lines

* between functions & methods
* between local variables in a method and it's first statement
* before controls statements (if, for, while)
* before a comment

```javascript

function foo () {
    var i,
        len = 10,
        localA = true;

    for (; i < len; i++) {
        alert(len);

        if (localA) {
            alert(len + ':' + localA);

            if (!localA) {
                alert('m(...)m');
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

### Naming

Constructor functions should be pascal case, regular function and variable names should be camel case. Variable names should begin with a noun, function names should begin with a verb.

```javascript
// ...
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

Functions (Expression, Named, Constructor)

```javascript
var foo = function (arg) {
    // ...
};
foo('arg');

function bar(arg) {
    // ...
}
bar('arg');

var foobar;

function FooBar(options) {
    this.options = options || {};
}
foobar = new FooBar({a: 'alpha'});

foobar.options;
// {a: 'alpha'}
```
---

## Best practices

### Code quality

Use strict mode for new code and make sure your code passes [JsHint](http://www.jshint.com/), if it doesn't pass, and you must go against a hint, add the appropriate [JsHint option](http://jshint.com/docs/#enforcing_options) to make it pass.

```javascript
// tell JsHint jQuery is a valid global variable
/*global jQuery*/
(function ($) {
    'use strict';
    var module = {
        prop: false
    };

    function toggleProp() {
        /*jshint validthis: true*/

        // tell jshint to ignore 'possible this strict mode violation'
        this.prop = !!this.prop;
    }

    toggleProp.apply(module);
}(jQuery));
```

### Variables

Use a single `var` statement at the beginning of the scope.

```javascript
(function () {
    var count,
        foo = null,
        hasQSA = (function() {
            return 'querySelectorAll' in document;
        }());


    function bar () {
        if (foo === null) {
            explode();
        }
    }
}());
```

### Modules

#### Standalone module

```javascript
(function (document, undefined) {
    'use strict';
    var private = true,
        danceparty = document.getElementById('danceparty');

    danceparty.className = 'dance-time';
}(document));
```

#### Augment existing name space or module

```javascript
window.NameSpace = (function (document, NameSpace) {
    'use strict';

    // setup
    var privateCount = 0;

    // public api
    NameSpace.counter = {
        count: function () {
            return privateCount;
        },

        increment: function () {
            return ++privateCount;
        },

        decrement: function () {
            return --privateCount;
        }
    };
    return NameSpace;
}(document, window.NameSpace || {}));
```

#### Making a module testable

We use QUnit, so if QUnit is defined expose normally private methods for testing and optionally don't run our normal initialization method.

```javascript
window.theModule = (function (document, theModule, QUnit, undefined) {
    'use strict';
    var initialize = function () {
        // initialize
    };

    theModule.publicMethod = function () {
        //...
    };

    if (!QUnit) {
        // initialize as normal if no QUnit
        initialize();
    } else {
        // expose normally private functions for testing if needed
        theModule.helper = helper;
        theModule.initialize = initialize;
    }

    return theModule;
}(document, window.theModule || {}, QUnit));
```
