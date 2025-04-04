
To publish a new version of this fork, follow https://docs.npmjs.com/creating-and-publishing-an-organization-scoped-package:
1. Authenticate with npm with `npm adduser`
2. Merge any desired changes
3. Update the `version` field in `package.json`
4. Push desired changes and version update.
5. Run `npm run build`
6. Run `npm publish --access public`

# JSON→URL

[![License: MIT](https://img.shields.io/github/license/jsonurl/jsonurl-js.svg?label=License)][license]
[![NPM version](https://img.shields.io/npm/v/@jsonurl/jsonurl.svg)](https://www.npmjs.com/package/@jsonurl/jsonurl)
[![CI](https://github.com/jsonurl/jsonurl-js/workflows/ci/badge.svg?branch=main)](https://github.com/jsonurl/jsonurl-js/actions/workflows/ci.yml)
[![Quality Gate](https://sonarcloud.io/api/project_badges/measure?project=jsonurl-js\&metric=alert_status)](https://sonarcloud.io/dashboard?id=jsonurl-js)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=jsonurl-js\&metric=coverage)](https://sonarcloud.io/dashboard?id=jsonurl-js)
[![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=jsonurl-js\&metric=ncloc)](https://sonarcloud.io/dashboard?id=jsonurl-js)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=jsonurl-js\&metric=security_rating)](https://sonarcloud.io/dashboard?id=jsonurl-js)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=jsonurl-js\&metric=vulnerabilities)](https://sonarcloud.io/dashboard?id=jsonurl-js)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=jsonurl-js\&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=jsonurl-js)
[![Known Vulnerabilities](https://snyk.io/test/github/jsonurl/jsonurl-js/badge.svg?targetFile=package.json)](https://snyk.io/test/github/jsonurl/jsonurl-js?targetFile=package.json)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fjsonurl%2Fjsonurl-js.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fjsonurl%2Fjsonurl-js?ref=badge_shield)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.0%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-green)](CONTRIBUTING.md)
[![project chat](https://img.shields.io/badge/zulip-join_chat-brightgreen.svg)](https://jsonurl.zulipchat.com/)

## About

[RFC8259][RFC8259] describes the JSON data model and interchange format, which is widely
used in application-level protocols including RESTful APIs. It is common for
applications to request resources via the HTTP POST method, with JSON entities.
However, POST is suboptimal for requests which do not modify a resource's
state. JSON→URL defines a text format for the JSON data model suitable
for use within a [URL][RFC1738]/[URI][RFC3986].

## Usage

JSON→URL is available as a commonjs module (suitable for use in Node), ES6
module, or a script that may be used directly in a browser.

### NPM install

```sh
npm install @jsonurl/jsonurl --save
```

### CJS

```js
const JsonURL = require("@jsonurl/jsonurl");
```

### ES6 (Node + Babel)

```js
import JsonURL from "@jsonurl/jsonurl";
```

### Browser script tag

```html
<script
    src="https://cdn.jsdelivr.net/npm/@jsonurl/jsonurl@1.1.8"
    integrity="sha512-LIJoXzT8Z9ZYDVCop/RciWbhJCDBzOevskMv9YPLHI8kGUtJ32DHHDWdIBLBmMoKkMr7vsZEysOrOBbVg7yioA=="
    crossorigin="anonymous"></script>
```

### The JavaScript API

Once included, the API is the same for all three.

[![RunKit: Hello, World!](https://img.shields.io/badge/RunKit-Hello%2C%20World!-ff69b4)][runkit1]

```js
let value = JsonURL.parse( "(Hello:World!)" );
let string = JsonURL.stringify( value );
```

If you intend to use JSON→URL inside a browser's address bar then you'll want to
enable the AQF (address bar query string friendly) syntax.

[![RunKit: Hello, Browser Address Bar!](https://img.shields.io/badge/RunKit-Hello%2C%20Address%20Bar!-ff69b4)][runkit2]

```js
let value = JsonURL.parse( "(Hello:Address Bar!!)",  { AQF: true });
let string = JsonURL.stringify( value,  { AQF: true } );
```

### Options - noEmptyComposite

The JSON→URL specification defines the empty composite value, `()`, because an
empty array is indistinguishable from an empty object. This works well in
practice, generally, but it can lead to counterintuitive results when parsing
JSON→URL text into a language-native object and then stringifying it back
into JSON→URL text; the input text doesn't "round-trip" back to
itself as expected.

The `noEmptyComposite` parse option causes the character sequence `()` to be
parsed as an empty array, and the character sequence `(:)` to be parsed as an
empty object. And the `noEmptyComposite` stringify option instructs
`stringify` to generate those strings appropriately.

[![RunKit: noEmptyComposite](https://img.shields.io/badge/RunKit-noEmptyComposite-ff69b4)][runkit3]

```js
let value = JsonURL.parse( "(Array:(true,false,(nested),()),Object:(nested:(:)))",  { AQF: true, noEmptyComposite: true });
let string = JsonURL.stringify( value,  { AQF: true, noEmptyComposite: true });
```

### Options - More

There are additional options available. The [typescript definition][dts] file
is a good place to learn more.

JSON→URL has no runtime dependencies.

## Security

The parser is designed to parse untrusted input. It supports limits on
the number of parsed values and depth of nested arrays or objects.
When the limit is exceeded an Error is thrown, and reasonable limit values are
set by default.

[RFC8259]: https://tools.ietf.org/html/rfc8259

[RFC3986]: https://tools.ietf.org/html/rfc3986

[RFC1738]: https://tools.ietf.org/html/rfc1738

[license]: https://opensource.org/licenses/MIT

[runkit1]: https://runkit.com/jsonurl/hello-world

[runkit2]: https://runkit.com/jsonurl/hello-aqf

[runkit3]: https://runkit.com/jsonurl/noemptycomposite

[dts]: https://github.com/jsonurl/jsonurl-js/blob/main/jsonurl.d.ts

## License

[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fjsonurl%2Fjsonurl-js.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fjsonurl%2Fjsonurl-js?ref=badge_large)
