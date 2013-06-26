# Javascript style guide

This guide borrows heavily from around the net and Nicholas Zakas' book [Maintainable Javascript](http://www.amazon.com/Maintainable-JavaScript-ebook/dp/B0082CXEB0).

## Indentation

Indent with 4 spaces, do not mix spaces and tabs.

## Statement Termination

Always include semi-colons, don't rely on Javscript's [automatic semi-colon insertion](http://bclary.com/2004/11/07/#a-7.9.1).

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

