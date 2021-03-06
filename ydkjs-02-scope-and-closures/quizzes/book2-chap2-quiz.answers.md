# Quiz - YDKJS: Scope & Closures 2/5

## Chapter 2. Lexical Scope

### Answer Sheet

#### Section: Lex-time

---

##### 1. What are the two predominant models for how Scope works used by the majority of programming languages?

> _lexical scope_
>
> _dynamic scope_

##### 2. Which is the `Scope` model that JavaScript employs?

> _lexical scope_

##### 3. How many `Scopes` can you identify in the following snippet, and what would be the output?

###### Snippet #1

```js
var result = (function (a) {
  function foo(b) {
    return bar(5);

    function bar(c) {
      return a + b + c;
    }
  }

  return foo(2);
})(3);

console.log(result);
```

> _There are 4 `Scopes`:_
>
> _global scope_
>
> _- anonymous function (iife) scope_
>
> _-- foo scope_
>
> _--- bar scope_
>
> _Output: `10`_

##### 4. What is `shadowing`?

> _when an identifier of an inner scope `shadows` an identifier of an outer scope._

##### 5. Look Up in nested scopes. What would be the output for the following snippets?

_**NOTE:** replace `window` with `global` if you are using node.js_

###### Snippet #2

```js
var name = "John";

function foo(name) {
  function bar() {
    var name = "Doe";

    return (function baz() {
      return name;
    })();
  }
  return bar();
}

console.log(foo(name));
```

> _"Doe"_

###### Snippet #3

```js
var a = 2;

console.log(window.a);
```

> _`2`_

###### Snippet #4

```js
function foo() {
  var a = 3;
}

console.log(foo.a);
```

> _`undefined`_

###### Snippet #5

```js
function foo() {
  // noop
}

foo.a = 4;

console.log(foo.a);
```

> _`4`_

###### Snippet #6

```js
var a = 5;

function foo() {
  a = 10;

  console.log(a);
  console.log(window.a);
}

foo();
```

> _`10`_
>
> _`10`_

#### Section: Cheating Lexical

---

##### 6. `eval`. Write the output for the following snippets:

###### Snippet #7

```js
"use strict";

function foo(str) {
   eval(str);
   console.log(z);
}

foo("var z = 4;");
```

> _ReferenceError: z is not defined_

###### Snippet #8

```js
function foo(str) {
   eval(str);
   console.log(x);
}

foo("var x = 5;");
```

> _`5`_

###### Snippet #9

```js
function foo(str) {
   eval(str);
}

foo("y = 7;");

console.log(y);
```

> _`7`_

###### Snippet #10

```js
function foo(str) {
   eval(str);
}

foo("var y = 7;");

console.log(y);
```

> _ReferenceError: y is not defined_

##### 7. `with`. Write the output for the following snippets:

###### Snippet #11

```js
function foo(o) {
   with (o) {
     a = 5;
   }
}

var obj = { a: 2 };

foo(obj);

console.log(obj.a);
```

> _`5`_

###### Snippet #12

```js
function foo(o) {
   with (o) {
     b = 10;
   }
}

var obj = { a: 2 };

foo(obj);

console.log(obj.b);
```

> _`undefined`_

###### Snippet #13

```js
function foo(o) {
   with (o) {
     b = 5;
   }
}

var obj = { a: 2 };

foo(obj);

console.log(b);
```

> _`5`_

###### Snippet #14

```js
function foo(o) {
   with (o) {
     b = 5;
   }
}

var obj = { a: 2 };

foo(obj);

console.log(a);
```

> _`ReferenceError: a is not defined`_

###### Snippet #15

```js
function foo(o) {
   with (o) {
     var b = 3;
   }
   console.log(b);
}

var obj = { b: 2 };

foo(obj);
```

> _`undefined`_

###### Snippet #16

```js
function foo(o) {
   with (o) {
     var b;
   }
   b = 3;
   console.log(b);
}

var obj = { b: 2 };

foo(obj);
```

> _`3`_

###### Snippet #17

```js
function foo(o) {
   with (o) {
     var b = 3;
   }
}

var obj = { b: 2 };

foo(obj);

console.log(b);
```

> _`ReferenceError: b is not defined`_

###### Snippet #18

```js
function foo(o) {
   with (o) {
     b = 3;
   }
}

var obj = { b: 2 };

foo(obj);

console.log(b);
```

> _`ReferenceError: b is not defined`_

###### Snippet #19

```js
"use strict";

function foo(o) {
   with (o) {
     b = 3;
   }
}

var obj = { a: 2 };

foo(obj);

console.log(b);
```

> _`SyntaxError: Strict mode code may not include a with statement`_

##### 8. Why should you avoid using both `eval` and `with` in your code?

> _**code will run slower** no matter how smart the Engine is, because these mechanisms defeat the Engine's ability to perform compile-time optimizations._

##### 9. What's the difference between `Lexical Scope` and `Scope`?

> _none. both are the same, actually is more proper to call it `Lexical Scope`_