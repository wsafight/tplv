# TPLV

> Nano(~170 bytes), High performance string template library, based on ES6 String template syntax.

[![npm Version](https://img.shields.io/npm/v/tplv.svg)](https://www.npmjs.com/package/tplv)
[![Build Status](https://github.com/hustcc/tplv/workflows/build/badge.svg)](https://github.com/hustcc/tplv/actions)
[![Coverage Status](https://coveralls.io/repos/github/hustcc/tplv/badge.svg?branch=master)](https://coveralls.io/github/hustcc/tplv?branch=master)
[![npm License](https://img.shields.io/npm/l/tplv.svg)](https://www.npmjs.com/package/tplv)


## Install

```bash
$ npm i --save tplv
```


## Usage

 - `render` template string

```ts
import { render } from 'tplv';

const template = '${ name }, ${value}(${percent} | Top ${array[2]})';

const data = {
  name: 'Hangzhou',
  value: 1200,
  percent: '13%',
  array: [1, 2, 3, 4]
};

render(template, data); // `Hangzhou, 1200(13% | Top 3)` will be got
```

 - `compile` mode

> For `13x` faster performance then render mode.

```ts
import { compile } from 'tplv';

const template = '${ name }, ${value}(${percent} | Top ${array[2]})';

const data = {
  name: 'Hangzhou',
  value: 1200,
  percent: '13%',
  array: [1, 2, 3, 4]
};

const fn = compile(template, ['name', 'value', 'percent', 'array']);

fn(data); // `Hangzhou, 1200(13% | Top 3)` will be got
```


## Perf

Run performance test with [rendering-test](https://aui.github.io/art-template/rendering-test/).

![perf test](https://user-images.githubusercontent.com/7856674/74140231-abef9300-4c2f-11ea-875d-d57e845e9ef7.png)


## Principle

The core code and principles are as follows:

```ts
function render(template, data) {
  const ks = Object.keys(data);
  const vs = ks.map((k) => data[k]);

  const t = `return \`${template}\``;
  const f = new Function(...ks, t);

  return f(...vs);
}
```


## Dev

```bash
# install dependence
$ npm install

# run test cases
$ npm run test

# run performance for render / compile mode
$ npm run perf

# build package
$ npm run build
```


## License

MIT@[hustcc](https://github.com/hustcc).
