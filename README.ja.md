# cssesc

CSSの文字列や識別子をエスケープしつつ、可能な限り短いASCIIのみの出力を生成するJavaScriptライブラリです。[ホームページ](https://mths.be/cssesc)

作成者: [Mathias Bynens](https://mathiasbynens.be/)

## 特徴

*   CSSで安全に使用できるように文字列と識別子をエスケープします。
*   可能な限り短く、有効なASCIIのみの出力を生成します。
*   追加面の文字（astral symbols）を含む、Unicodeの全範囲をサポートします。
*   堅牢なコマンドラインインターフェース（CLI）を提供します。
*   `CSS.escape()` のポリフィルとして使用できます。
*   クォートやラッピングなどのオプションで高度にカスタマイズ可能です。

## インストール

[npm](https://www.npmjs.com/) 経由:

```bash
npm install cssesc
```

## 使い方

### Node.jsでの使用

```js
const cssesc = require('cssesc');

// 文字列のエスケープ
console.log(cssesc('Ich ♥ Bücher'));
// → 'Ich \2665  B\FC cher'

// 識別子のエスケープ
console.log(cssesc('123', { 'isIdentifier': true }));
// → '\31 23'
```

### ブラウザおよびDeno（ESモジュール）での使用

```js
import { cssesc } from "https://code4fukui.github.io/cssesc/cssesc.js";

console.log(cssesc("Ich ♥ Bücher"));
// → 'Ich \2665  B\FC cher'
```

### ブラウザ（`<script>`タグ経由）での使用

```html
<script src="cssesc.js"></script>
<script>
  console.log(cssesc('Ich ♥ Bücher'));
  // → 'Ich \2665  B\FC cher'
</script>
```

## API

### `cssesc(value, [options])`

この関数は文字列 `value` を受け取り、エスケープされた文字列を返します。オプションの `options` オブジェクトを使用してカスタマイズが可能です。

#### `options.isIdentifier`

型: `Boolean`
デフォルト: `false`

`true` に設定すると、入力をCSS識別子としてエスケープします。識別子は文字列よりも厳格なルールがあります（例: 数字で始まることはできません）。

```js
cssesc('1a', { 'isIdentifier': true });
// → '\31 a'

cssesc('--foo', { 'isIdentifier': true });
// → '\--foo'
```

#### `options.quotes`

型: `String`
デフォルト: `'single'`
値: `'single'`, `'double'`

出力をラップするクォートの種類を指定します。このオプションは `options.wrap` が `true` の場合にのみ使用されます。

```js
cssesc('foo "bar"', { 'wrap': true, 'quotes': 'double' });
// → '"foo \\"bar\\""'

cssesc("foo 'bar'", { 'wrap': true, 'quotes': 'single' });
// → "'foo \\'bar\\''"
```

#### `options.wrap`

型: `Boolean`
デフォルト: `false`

`true` に設定すると、出力をクォートでラップし、有効なCSS文字列リテラルを作成します。

```js
cssesc('foo', { 'wrap': true });
// → "'foo'"
```

#### `options.escapeEverything`

型: `Boolean`
デフォルト: `false`

`true` に設定すると、出力内のすべての記号（印刷可能なASCII文字も含む）をエスケープします。

```js
cssesc('foo', { 'escapeEverything': true });
// → '\66\6F\6F'
```

## コマンドラインインターフェース（CLI）

CLIを使用するには、`cssesc` をグローバルにインストールします:

```bash
npm install -g cssesc
```

### 使い方

```bash
cssesc [options] <string>
```

文字列は `stdin` からパイプで渡すこともできます。

### オプション

*   `-i`, `--identifier`: CSS識別子としてエスケープします。
*   `-s`, `--single-quotes`: シングルクォートを使用します。
*   `-d`, `--double-quotes`: ダブルクォートを使用します。
*   `-w`, `--wrap`: 出力をクォートでラップします。
*   `-e`, `--escape-everything`: すべての記号をエスケープします。
*   `-v`, `--version`: バージョン番号を表示します。
*   `-h`, `--help`: ヘルプ画面を表示します。

### 例

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

## インテグレーション

*   **Ruby:** [`ruby-cssesc`](https://github.com/mathiasbynens/ruby-cssesc) gem経由で使用します。
*   **Sass:** [`sassy-escape`](https://github.com/mathiasbynens/sassy-escape) ミックスイン経由で使用します。

## ライセンス

MIT © [Mathias Bynens](https://mathiasbynens.be/)
