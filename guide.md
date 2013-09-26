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
    * [Module Patterns](#module-patterns)
        * [Private module](#private-module)
        * [Module with Public API](#module-with-public-api)
        * [Making a module testable](#making-a-module-testable)
    * [Declaring Variables](#declaring-variables)

## Code Quality

* use [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode) for all new code.
* make sure you code passes [JsHint](http://jshint.com/). If you must include code that doesn't pass the JsHint check add a [directive](http://jshint.com/docs/#directives) to make it pass.

```javascript
/*global jQuery*/ // jshint option: to declare jQuery a valid global
(function ($) {
    'use strict'; // turn on strict mode
    var module = {
        prop: false
    };

    function toggleProp() {
        /*jshint validthis: true*/ // jshint option: ignore 'possible strict mode violation'
        this.prop = !this.prop;
    }

    toggleProp.apply(module);
})(jQuery);
```
## Indentation

Indent a tab, do not mix spaces and tabs.

## Statement Termination

Always include semi-colons, don't rely on Javscript's [automatic semi-colon insertion](http://bclary.com/2004/11/07/#a-7.9.1) rules.

## Line Length

Limit line length to 80 characters, for lines greater than 80 characters break after an operator and double indent the next line unless doing an assignment.

```javascript
// double indent wrapped lines
if (isLongPoorlyNamedFunctionReturningBoolean() && !isGiraffe() && !isFishy() ||
        isBriney() && isFishy()) {
    fooWithFeeling();
}

// exception: when doing assignment
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
// put opening brace on same line as statement
if (true) {
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


// define loop variables at the beginning of scope
var i,
    len;

for (i = 0, len = 10; i < 10; i++) {
    // ...
}

var prop;

for (prop in someObject) {
    // ...
}
```

## White Space

Blank lines improve readability by setting off sections of code that are logically related.

Always put a blank line

* between methods
* between local variables and the next statement
* before comments
* before control statements e.g. if, for, while etc.

```javascript
(function() {
    'use strict';
    var a,
        b = 10;

    function theFunction() {

        if (true) {

            if (!!0) {

                while (--b) {
                    a = b;

                    // HACK: nonsense
                    b = a;
                }
            }
        }
    }

    function aFunction() {
        // ...
    }
})();
```

## Best Practices

### Module Patterns

#### Private Module

If you don't need to export any functionality wrap it in an [Immediately-Invoked Function Expression](http://benalman.com/news/2010/11/immediately-invoked-function-expression/) to prevent variable name collisions and keep the global namespace clean. Always try to use [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode).

```javascript
(function () {
    'use strict';
    var privateVar = true,
        danceparty = document.getElementById('danceparty');

    if (privateVar) {
        danceparty.className = 'dance-time';
    }
})();
```

#### Module with Public API

If you need to add functionality to an existing global namespace/module.

```javascript
// explicitly assign your module to window property,jhjh
var NameSpace = (function (NameSpace) {
    'use strict';

    // setup
    var privateCount = 0;

    // Add a counter sub-module to object
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

    return NameSpace; // return augmented object
})(NameSpace || {}); // if namespace object isn't defined yet create it
```

#### Making a module testable

We use QUnit, so if QUnit is on the window, expose your normally private methods for testing. Optionally don't run our normal initialization method.

```javascript
var myModule = (function (myModule) {
    'use strict';
    var initialize = function () {
        // initialize
    };

    myModule.publicMethod = function () {
        //...
    };

    if (!window.QUnit) {
        // initialize as normal if no QUnit
        initialize();
    } else {
        // expose normally private functions for testing if needed
        myModule.initialize = initialize;
    }

    return myModule;
})(myModule || {});
```

### Declaring variables

Declare variables at the beginning of their scope in a single statement. Declaring variables in a single statement performs faster than spreading them around, makes them easier to find and reduces [hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting) errors.

```javascript
(function (){
    'use strict';
    // declare module wide variables at the beginning of module scope in a single statement
    var moduleA = 4,
        moduleB = 5;

    function aFunc (msg) {
        // declare local variables at the beginning of function scope
        var standardGreeting = 'Hello';

        if (!!msg) {
            return standardGreeting + ' A: ' + moduleA;
        } else {
            return msg + 'B: ' + moduleB;
        }
    }

    alert(aFunc()); // Hello A: 4
    alert(aFunc('ohai!')); // ohai! B: 5
})();
```
