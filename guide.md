# Javascript style guide

This guide borrows heavily from around the net and Nicholas Zakas' book [Maintainable Javascript](http://www.amazon.com/Maintainable-JavaScript-ebook/dp/B0082CXEB0).

* [Code Quality](#code-quality)
* [Indentation](#indentation)
* [Statement Termination](#statement-termination)
* [Line Length](#line-length)
* [Blank Lines](#blank-lines)
* [Naming](#naming)
* [Equality Operators](#equality-operators)
* [Ternary Operator](#ternary-operator)
* [Compound Statements](#compound-statements)
* [White Space](#white-space)
* [Best Practices](#best-practices)
    * [Standalone module](#standalone-module)
    * [Augment module](#augment-module)
    * [Making a module testable](#making-a-module-testable)

## Code Quality

Use strict mode for all new code and make sure it passes [JsHint](http://jshint.com/). If you must include code that doesn't pass the JsHint check add a [directive](http://jshint.com/docs/#directives) to make it pass.

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
        this.prop = !this.prop;
    }

    toggleProp.apply(module);
}(jQuery));
```
## Indentation

Indent with 4 spaces, do not mix spaces and tabs.

## Statement Termination

Always include semi-colons, don't rely on Javscript's [automatic semi-colon insertion](http://bclary.com/2004/11/07/#a-7.9.1) rules.

## Line Length

Limit line length to 80 characters, for lines greater than 80 characters break after an operator and double indent the next line unless doing an assignment.

```javascript
if (isLongPoorlyNamedFunctionReturningBoolean() && !isGiraffe() && !isFishy() ||
        isBriney() && isFishy()) {
    fooWithFeeling();
}

// exception when doing assignment
var UI_MESSAGE = stringBegin + option[1] + option[3] + stringMiddle +
                 stringEnder;
```

## Blank Lines

Use blank lines to separate related lines of code from unrelated lines of code. It's a good idea to add blank lines: 

* before control statements
* between methods
* between the local variables in a method and the first statement
* before a comment
* between logical sections inside a method to improve readability

```javascript
var len,
    p,
    i = 0;
    
if (1 && !0) {

    for (len = items.length; i < l; ++i) {
        p = items[i];

        if (p.nodeType === 1) {

            if (p.nodeName === 'A') {
                p.href = '#';
            } else {

                // kill the child
                p.parentNode.removeChild(p);
            }
        }
    }
}
```

## Naming

Use camel case for variables and regular functions, pascal case for constructors and all caps to indicate a constant. Variables and constructors should begin with a noun and regular functions should begin with a verb.

```javascript
function MoneyMaker(amount) {
    var UI_UNIT = 'dollars';

    this.money = amount || 1;
    this.addMoney = function (amount) {
        return this.money += amount;
    };
}

var piggyBank = new MoneyMaker(1000);
piggyBank.addMoney(1);
```

## Equality Operators

Use `===` and `!==` instead of `==` and `!=` to avoid type coercion.

```javascript
var same = (a === b);
```

## Ternary Operator

Use ternary operator to conditionally assign a value, not as a shortcut for an if statement.

```javascript
var val = (a > b) ? b : a;
```

## Compound Statements

Opening braces should be at the end of the line that begins the compound statement. Braces should be used around all statements even one-liners. Variables should not be declared in the initialization section of a for statement.

```javascript
if (true) {
    // ...
}

if (true) {
    // ...
} else {
    // ...
}

var i,
    len;

for (i = 0, len = 10; i < 10; i++) {
    // ...
}

var prop;

for (prop in someObject) {
    // ...
}

while (condition) {
    // ..
}

do {
    // ...
} while (value);

switch (true) {
    case 1:
        /* fall through */
    case 2:
        fn();
        break;
    default:
        return undefined;
}

try {
    // ...
} catch (e) {
    // ...
} finally {
    // ...
}
```

## White Space

```javascript
// ...
```

## Best Practices

## Standalone module

```javascript
(function (document, undefined) {
    'use strict';
    var private = true,
        danceparty = document.getElementById('danceparty');

    danceparty.className = 'dance-time';
}(document));
```

## Augment module

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

## Making a module testable

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