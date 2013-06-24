# Best Practices

* Variables
* Modules


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

    initalize = function () {
        // initalize
    };

    if (!QUnit) {
        // init as normal if no QUnit
        initialize();
    } else {
        // expose normally private functions for testing
        my.helper = helper;
        my.initialize = initialize;
    }

    return my;
}(document, theModule || {}, QUnit));
```
