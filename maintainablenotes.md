# maintainable

## Notes

* Indentation
	* 4 spaces not tab
* Statement termination
	* always use semi-colon
* Line length
	* 80 chars max
* Line breaks
	* break after an operator
	* double indent next line
* Blank lines
	* between methods
	* between local variables in a method and it's first statement
	* before controls statements (if, for)
	* before a comment
* Naming
	* function names use camel case and begin with a verb
	* variable names use camel case and begin with a noun
	* avoid meaningless names like foo
* Constants
	* all caps
* Constructors
	* Pascal case
* Literals
	* Strings
		* single quote strings
	* Numbers
		* avoid leading decimal point
		* avoid hanging decimal point
		* avoid octal
	* Objects
		* prefer object literal to Object constructor
	* Array
			* prefer array literal to array constructor
*  Comments
	* comment on line above
	* don't comment if it doesn't add value
	* comment browse specific hacks with specifics
* Blocks and Expressions
	* Braces
		* always include braces
		* prefer opening brace on the same line as the block beginning
	* Parenthesis
		* include a space before and after parenthesis
* Functions
	* put a single space before and after parenthesis in function declaration
	* put a single space after between parameters in function declaration
	* no spaces between name and parenthesis when calling a function
	* prefer full parenthesis wrap on IEFE `(function () {}());`

* Strict Mode
	* 'use strict'; please
	* use JsHint and make it pass, add overrides if you need to

## Appendix

* Indentation
	* 4 spaces, no tabs
* Line length
	* no longer than 80 chars, if a line goes longer wrap after an operator and double indent the following line
* Primitives
	* Strings should use single quote and should be on a single line. Don't use `\` to wrap a string
	* Numbers should have at least one digit before a decimal point, never use octals
* Operator spacing
* Parentheses spacing
* Object literals
* Comments
* Variable declarations
* Function declarations
* Naming
* Strict mode
* Assignments
* Equality operators
* Ternary operator
* Statements
* White space
* Avoid
