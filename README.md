# cssesc

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A JavaScript library for escaping CSS strings and identifiers while generating the shortest possible ASCII-only output. [Homepage](https://mths.be/cssesc)

Authored by [Mathias Bynens](https://mathiasbynens.be/).

## Features

*   Escapes strings and identifiers for safe use in CSS.
*   Generates the shortest possible, valid ASCII-only output.
*   Supports the full Unicode range, including astral symbols.
*   Provides a robust command-line interface (CLI).
*   Can be used as a polyfill for `CSS.escape()`.
*   Highly configurable with options for quotes, wrapping, and more.

## Installation

Via [npm](https://www.npmjs.com/):

```bash
npm install cssesc
```

## Usage

### In Node.js

```js
const cssesc = require('cssesc');

// Escaping a string
console.log(cssesc('Ich ♥ Bücher'));
// → 'Ich \2665  B\FC cher'

// Escaping an identifier
console.log(cssesc('123', { 'isIdentifier': true }));
// → '\31 23'
```

### In Browsers and Deno (ES Module)

```js
import { cssesc } from "https://code4fukui.github.io/cssesc/cssesc.js";

console.log(cssesc("Ich ♥ Bücher"));
// → 'Ich \2665  B\FC cher'
```

### In a Browser (via `<script>` tag)

```html
<script src="cssesc.js"></script>
<script>
  console.log(cssesc('Ich ♥ Bücher'));
  // → 'Ich \2665  B\FC cher'
</script>
```

## API

### `cssesc(value, [options])`

This function takes a string `value` and returns an escaped version. The optional `options` object allows for customization.

#### `options.isIdentifier`

Type: `Boolean`
Default: `false`

Set this to `true` to escape the input for use as a CSS identifier. Identifiers have stricter rules than strings (e.g., they cannot start with a digit).

```js
cssesc('1a', { 'isIdentifier': true });
// → '\31 a'

cssesc('--foo', { 'isIdentifier': true });
// → '\--foo'
```

#### `options.quotes`

Type: `String`
Default: `'single'`
Values: `'single'`, `'double'`

Specifies the type of quotes to use when wrapping the output. This option is only used when `options.wrap` is `true`.

```js
cssesc('foo "bar"', { 'wrap': true, 'quotes': 'double' });
// → '"foo \\"bar\\""'

cssesc("foo 'bar'", { 'wrap': true, 'quotes': 'single' });
// → "'foo \\'bar\\''"
```

#### `options.wrap`

Type: `Boolean`
Default: `false`

Set this to `true` to wrap the output in quotes, creating a valid CSS string literal.

```js
cssesc('foo', { 'wrap': true });
// → "'foo'"
```

#### `options.escapeEverything`

Type: `Boolean`
Default: `false`

Set this to `true` to escape all symbols in the output, including printable ASCII characters.

```js
cssesc('foo', { 'escapeEverything': true });
// → '\66\6F\6F'
```

## Command-Line Interface (CLI)

Install `cssesc` globally to use the CLI:

```bash
npm install -g cssesc
```

### Usage

```bash
cssesc [options] <string>
```

The string can also be piped from `stdin`.

### Options

*   `-i`, `--identifier`: Escape as a CSS identifier.
*   `-s`, `--single-quotes`: Use single quotes.
*   `-d`, `--double-quotes`: Use double quotes.
*   `-w`, `--wrap`: Wrap the output in quotes.
*   `-e`, `--escape-everything`: Escape all symbols.
*   `-v`, `--version`: Print the version number.
*   `-h`, `--help`: Show the help screen.

### Examples

```bash
$ cssesc 'fóo bår'
f\F3 o b\E5 r

$ cssesc --identifier '1a'
\31 a

$ cssesc --wrap --double-quotes 'fóo "bår"'
"f\F3 o \"b\E5 r\""

$ echo 'fóo bår' | cssesc
f\F3 o b\E5 r
```

## Integrations

*   **Ruby:** Use via the [`ruby-cssesc`](https://github.com/mathiasbynens/ruby-cssesc) gem.
*   **Sass:** Use via the [`sassy-escape`](https://github.com/mathiasbynens/sassy-escape) mixin.

## License

MIT © [Mathias Bynens](https://mathiasbynens.be/)