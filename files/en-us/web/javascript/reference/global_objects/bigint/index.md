---
title: BigInt
slug: Web/JavaScript/Reference/Global_Objects/BigInt
page-type: javascript-class
browser-compat: javascript.builtins.BigInt
sidebar: jsref
---

**`BigInt`** values represent integer values which are [too high](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER) or [too low](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_SAFE_INTEGER) to be represented by the `number` {{Glossary("Primitive", "primitive")}}.

## Description

A **BigInt value**, also sometimes just called a **BigInt**, is a `bigint` {{Glossary("Primitive", "primitive")}}, created by appending `n` to the end of an integer literal, or by calling the {{jsxref("BigInt/BigInt", "BigInt()")}} function (without the `new` operator) and giving it an integer value or string value.

```js
const previouslyMaxSafeInteger = 9007199254740991n;

const alsoHuge = BigInt(9007199254740991);
// 9007199254740991n

const hugeString = BigInt("9007199254740991");
// 9007199254740991n

const hugeHex = BigInt("0x1fffffffffffff");
// 9007199254740991n

const hugeOctal = BigInt("0o377777777777777777");
// 9007199254740991n

const hugeBin = BigInt(
  "0b11111111111111111111111111111111111111111111111111111",
);
// 9007199254740991n
```

BigInt values are similar to Number values in some ways, but also differ in a few key matters: A BigInt value cannot be used with methods in the built-in [`Math`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) object and cannot be mixed with a Number value in operations; they must be coerced to the same type. Be careful coercing values back and forth, however, as the precision of a BigInt value may be lost when it is coerced to a Number value.

### Type information

When tested against `typeof`, a BigInt value (`bigint` primitive) will give `"bigint"`:

```js
typeof 1n === "bigint"; // true
typeof BigInt("1") === "bigint"; // true
```

A BigInt value can also be wrapped in an `Object`:

```js
typeof Object(1n) === "object"; // true
```

### Operators

Most operators support BigInts, however most do not permit operands to be of mixed types — both operands must be BigInt or neither:

- [Arithmetic operators](/en-US/docs/Web/JavaScript/Reference/Operators#arithmetic_operators): `+`, `-`, `*`, `/`, `%`, `**`
- [Bitwise operators](/en-US/docs/Web/JavaScript/Reference/Operators#bitwise_shift_operators): `>>`, `<<`, `&`, `|`, `^`, `~`
- [Unary negation (`-`)](/en-US/docs/Web/JavaScript/Reference/Operators/Unary_negation)
- [Increment/decrement](/en-US/docs/Web/JavaScript/Reference/Operators#increment_and_decrement): `++`, `--`

The boolean-returning operators allow mixing numbers and BigInts as operands:

- [Relational operators](/en-US/docs/Web/JavaScript/Reference/Operators#relational_operators) and [equality operators](/en-US/docs/Web/JavaScript/Reference/Operators#equality_operators): `>`, `<`, `>=`, `<=`, `==`, `!=`, `===`, `!==`
- [Logical operators](/en-US/docs/Web/JavaScript/Reference/Operators#binary_logical_operators) only rely on the [truthiness](/en-US/docs/Glossary/Truthy) of operands

A couple of operators do not support BigInt at all:

- [Unary plus (`+`)](/en-US/docs/Web/JavaScript/Reference/Operators/Unary_plus) cannot be supported due to conflicting usage in asm.js, so it has been left out [in order to not break asm.js](https://github.com/tc39/proposal-bigint/blob/master/ADVANCED.md#dont-break-asmjs).
- [Unsigned right shift (`>>>`)](/en-US/docs/Web/JavaScript/Reference/Operators/Unsigned_right_shift) is the only bitwise operator that's unsupported, as every BigInt value is signed.

Special cases:

- Addition (`+`) involving a string and a BigInt returns a string.
- Division (`/`) truncates fractional components towards zero, since BigInt is unable to represent fractional quantities.

```js
const previousMaxSafe = BigInt(Number.MAX_SAFE_INTEGER); // 9007199254740991n
const maxPlusOne = previousMaxSafe + 1n; // 9007199254740992n
const theFuture = previousMaxSafe + 2n; // 9007199254740993n, this works now!
const prod = previousMaxSafe * 2n; // 18014398509481982n
const diff = prod - 10n; // 18014398509481972n
const mod = prod % 10n; // 2n
const bigN = 2n ** 54n; // 18014398509481984n
bigN * -1n; // -18014398509481984n
const expected = 4n / 2n; // 2n
const truncated = 5n / 2n; // 2n, not 2.5n
```

### Comparisons

A BigInt value is not strictly equal to a Number value, but it _is_ loosely so:

```js
0n === 0; // false
0n == 0; // true
```

A Number value and a BigInt value may be compared as usual:

```js
1n < 2; // true
2n > 1; // true
2 > 2; // false
2n > 2; // false
2n >= 2; // true
```

BigInt values and Number values may be mixed in arrays and sorted:

```js
const mixed = [4n, 6, -12n, 10, 4, 0, 0n];
// [4n, 6, -12n, 10, 4, 0, 0n]

mixed.sort(); // default sorting behavior
// [ -12n, 0, 0n, 10, 4n, 4, 6 ]

mixed.sort((a, b) => a - b);
// won't work since subtraction will not work with mixed types
// TypeError: can't convert BigInt value to Number value

// sort with an appropriate numeric comparator
mixed.sort((a, b) => (a < b ? -1 : a > b ? 1 : 0));
// [ -12n, 0, 0n, 4n, 4, 6, 10 ]
```

Note that comparisons with `Object`-wrapped BigInt values act as with other objects, only indicating equality when the same object instance is compared:

```js
Object(0n) === 0n; // false
Object(0n) === Object(0n); // false

const o = Object(0n);
o === o; // true
```

Because coercing between Number values and BigInt values can lead to loss of precision, the following are recommended:

- Only use a BigInt value when values greater than 2<sup>53</sup> are reasonably expected.
- Don't coerce between BigInt values and Number values.

### Conditionals

A BigInt value follows the same conversion rules as Numbers when:

- it is converted to a [`Boolean`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean): via the [`Boolean`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) function;
- when used with [logical operators](/en-US/docs/Web/JavaScript/Reference/Operators) `||`, `&&`, and `!`; or
- within a conditional test like an [`if`](/en-US/docs/Web/JavaScript/Reference/Statements/if...else) statement.

Namely, only `0n` is [falsy](/en-US/docs/Glossary/Falsy); everything else is [truthy](/en-US/docs/Glossary/Truthy).

```js
if (0n) {
  console.log("Hello from the if!");
} else {
  console.log("Hello from the else!");
}
// "Hello from the else!"

0n || 12n; // 12n
0n && 12n; // 0n
Boolean(0n); // false
Boolean(12n); // true
!12n; // false
!0n; // true
```

### Cryptography

The operations supported on BigInt values are not constant-time and are thus open to [timing attacks](https://en.wikipedia.org/wiki/Timing_attack). JavaScript BigInts therefore could be dangerous for use in cryptography without mitigating factors. As a very generic example, an attacker could measure the time difference between `101n ** 65537n` and `17n ** 9999n`, and deduce the magnitude of secrets, such as private keys, based on the time elapsed. If you still have to use BigInts, take a look at the [Timing attack FAQ](https://timing.attacks.cr.yp.to/programming.html) for general advice regarding the issue.

### Use within JSON

Using [`JSON.stringify()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) with any BigInt value will raise a `TypeError`, as BigInt values aren't serialized in JSON by default. However, `JSON.stringify()` specifically leaves a backdoor for BigInt values: it would try to call the BigInt's `toJSON()` method. (It doesn't do so for any other primitive values.) Therefore, you can implement your own `toJSON()` method (which is one of the few cases where patching built-in objects is not explicitly discouraged):

```js
BigInt.prototype.toJSON = function () {
  return { $bigint: this.toString() };
};
```

Instead of throwing, `JSON.stringify()` now produces a string like this:

```js
console.log(JSON.stringify({ a: 1n }));
// {"a":{"$bigint":"1"}}
```

If you do not wish to patch `BigInt.prototype`, you can use the [`replacer`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#the_replacer_parameter) parameter of `JSON.stringify` to serialize BigInt values:

```js
const replacer = (key, value) =>
  typeof value === "bigint" ? { $bigint: value.toString() } : value;

const data = {
  number: 1,
  big: 18014398509481982n,
};
const stringified = JSON.stringify(data, replacer);

console.log(stringified);
// {"number":1,"big":{"$bigint":"18014398509481982"}}
```

You can then use the [`reviver`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse#using_the_reviver_parameter) parameter of `JSON.parse` to handle them:

```js
const reviver = (key, value) =>
  value !== null &&
  typeof value === "object" &&
  "$bigint" in value &&
  typeof value.$bigint === "string"
    ? BigInt(value.$bigint)
    : value;

const payload = '{"number":1,"big":{"$bigint":"18014398509481982"}}';
const parsed = JSON.parse(payload, reviver);

console.log(parsed);
// { number: 1, big: 18014398509481982n }
```

> [!NOTE]
> While it's possible to make the replacer of `JSON.stringify()` generic and properly serialize BigInt values for all objects as shown above, the reviver of `JSON.parse()` has to be used with caution, because the serialization is _irreversible_: it's not possible to distinguish between an object that happens to have a property called `$bigint` and an actual BigInt.
>
> In addition, the example above creates an entire object during replacing and reviving, which may have performance or storage implications for larger objects containing many BigInts. If you know the shape of the payload, it may be better to just serialize them as strings and revive them based on the property key's name instead.

In fact, JSON allows number literals that are arbitrarily long; they just cannot be parsed to full precision in JavaScript. If you are communicating with another program in a language that supports longer integers (such as 64-bit integers), and you want to transmit the BigInt as a JSON number instead of a JSON string, see [Lossless number serialization](/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON#using_json_numbers).

### BigInt coercion

Many built-in operations that expect BigInts first coerce their arguments to BigInts. [The operation](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-tobigint) can be summarized as follows:

- BigInts are returned as-is.
- [`undefined`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined) and [`null`](/en-US/docs/Web/JavaScript/Reference/Operators/null) throw a {{jsxref("TypeError")}}.
- `true` turns into `1n`; `false` turns into `0n`.
- Strings are converted by parsing them as if they contain an integer literal. Any parsing failure results in a {{jsxref("SyntaxError")}}. The syntax is a subset of [string numeric literals](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion), where decimal points or exponent indicators are not allowed.
- [Numbers](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) throw a {{jsxref("TypeError")}} to prevent unintended implicit coercion causing loss of precision.
- [Symbols](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) throw a {{jsxref("TypeError")}}.
- Objects are first [converted to a primitive](/en-US/docs/Web/JavaScript/Guide/Data_structures#primitive_coercion) by calling their [`[Symbol.toPrimitive]()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive) (with `"number"` as hint), `valueOf()`, and `toString()` methods, in that order. The resulting primitive is then converted to a BigInt.

The best way to achieve nearly the same effect in JavaScript is through the [`BigInt()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt/BigInt) function: `BigInt(x)` uses the same algorithm to convert `x`, except that [Numbers](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) don't throw a {{jsxref("TypeError")}}, but are converted to BigInts if they are integers.

Note that built-in operations expecting BigInts often truncate the BigInt to a fixed width after coercion. This includes {{jsxref("BigInt.asIntN()")}}, {{jsxref("BigInt.asUintN()")}}, and methods of {{jsxref("BigInt64Array")}} and {{jsxref("BigUint64Array")}}.

## Constructor

- {{jsxref("BigInt/BigInt", "BigInt()")}}
  - : Returns primitive values of type BigInt. Throws an error when called with `new`.

## Static methods

- {{jsxref("BigInt.asIntN()")}}
  - : Clamps a BigInt value to a signed integer value, and returns that value.
- {{jsxref("BigInt.asUintN()")}}
  - : Clamps a BigInt value to an unsigned integer value, and returns that value.

## Instance properties

These properties are defined on `BigInt.prototype` and shared by all `BigInt` instances.

- {{jsxref("Object/constructor", "BigInt.prototype.constructor")}}
  - : The constructor function that created the instance object. For `BigInt` instances, the initial value is the {{jsxref("BigInt/BigInt", "BigInt")}} constructor.
- `BigInt.prototype[Symbol.toStringTag]`
  - : The initial value of the [`[Symbol.toStringTag]`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toStringTag) property is the string `"BigInt"`. This property is used in {{jsxref("Object.prototype.toString()")}}. However, because `BigInt` also has its own [`toString()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt/toString) method, this property is not used unless you call [`Object.prototype.toString.call()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) with a BigInt as `thisArg`.

## Instance methods

- {{jsxref("BigInt.prototype.toLocaleString()")}}
  - : Returns a string with a language-sensitive representation of this BigInt value. Overrides the [`Object.prototype.toLocaleString()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toLocaleString) method.
- {{jsxref("BigInt.prototype.toString()")}}
  - : Returns a string representing this BigInt value in the specified radix (base). Overrides the [`Object.prototype.toString()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) method.
- {{jsxref("BigInt.prototype.valueOf()")}}
  - : Returns this BigInt value. Overrides the [`Object.prototype.valueOf()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf) method.

## Examples

### Calculating Primes

```js
function isPrime(n) {
  if (n < 2n) {
    return false;
  }
  if (n % 2n === 0n) {
    return n === 2n;
  }
  for (let factor = 3n; factor * factor <= n; factor += 2n) {
    if (n % factor === 0n) {
      return false;
    }
  }
  return true;
}

// Takes a BigInt value as an argument, returns nth prime number as a BigInt value
function nthPrime(nth) {
  let maybePrime = 2n;
  let prime = 0n;

  while (nth >= 0n) {
    if (isPrime(maybePrime)) {
      nth--;
      prime = maybePrime;
    }
    maybePrime++;
  }

  return prime;
}

nthPrime(20n);
// 73n
```

> [!NOTE]
> The `isPrime()` implementation is for demonstration only. For a real-world application, you would want to use a heavily memoized algorithm such as the [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) to avoid repeated calculations.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [`Number`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [`Number.MAX_SAFE_INTEGER`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)
