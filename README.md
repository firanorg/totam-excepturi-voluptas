# @firanorg/totam-excepturi-voluptas <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

ES2020 spec-compliant shim for String.prototype.matchAll. Invoke its "shim" method to shim `String.prototype.matchAll` if it is unavailable or noncompliant.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment, and complies with the [spec](https://tc39.es/ecma262/#sec-@firanorg/totam-excepturi-voluptas).

Most common usage:
```js
const assert = require('assert');
const matchAll = require('@firanorg/totam-excepturi-voluptas');

const str = 'aabc';
const nonRegexStr = 'ab';
const globalRegex = /[ac]/g;
const nonGlobalRegex = /[bc]/i;

// non-regex arguments are coerced into a global regex
assert.deepEqual(
	[...matchAll(str, nonRegexStr)],
	[...matchAll(str, new RegExp(nonRegexStr, 'g'))]
);

assert.deepEqual([...matchAll(str, globalRegex)], [
	Object.assign(['a'], { index: 0, input: str, groups: undefined }),
	Object.assign(['a'], { index: 1, input: str, groups: undefined }),
	Object.assign(['c'], { index: 3, input: str, groups: undefined }),
]);

assert.throws(() => matchAll(str, nonGlobalRegex)); // non-global regexes throw

matchAll.shim(); // will be a no-op if not needed

// non-regex arguments are coerced into a global regex
assert.deepEqual(
	[...str.matchAll(nonRegexStr)],
	[...str.matchAll(new RegExp(nonRegexStr, 'g'))]
);

assert.deepEqual([...str.matchAll(globalRegex)], [
	Object.assign(['a'], { index: 0, input: str, groups: undefined }),
	Object.assign(['a'], { index: 1, input: str, groups: undefined }),
	Object.assign(['c'], { index: 3, input: str, groups: undefined }),
]);

assert.throws(() => matchAll(str, nonGlobalRegex)); // non-global regexes throw

```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.com/package/@firanorg/totam-excepturi-voluptas
[npm-version-svg]: https://versionbadg.es/firanorg/totam-excepturi-voluptas.svg
[deps-svg]: https://david-dm.org/firanorg/totam-excepturi-voluptas.svg
[deps-url]: https://david-dm.org/firanorg/totam-excepturi-voluptas
[dev-deps-svg]: https://david-dm.org/firanorg/totam-excepturi-voluptas/dev-status.svg
[dev-deps-url]: https://david-dm.org/firanorg/totam-excepturi-voluptas#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@firanorg/totam-excepturi-voluptas.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@firanorg/totam-excepturi-voluptas.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@firanorg/totam-excepturi-voluptas.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@firanorg/totam-excepturi-voluptas
[codecov-image]: https://codecov.io/gh/firanorg/totam-excepturi-voluptas/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/firanorg/totam-excepturi-voluptas/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/firanorg/totam-excepturi-voluptas
[actions-url]: https://github.com/firanorg/totam-excepturi-voluptas/actions
