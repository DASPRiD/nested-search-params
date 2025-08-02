# Nested Search Params

[![Release](https://github.com/dasprid/nested-search-params/actions/workflows/release.yml/badge.svg)](https://github.com/dasprid/nested-search-params/actions/workflows/release.yml)
[![codecov](https://codecov.io/gh/DASPRiD/nested-search-params/graph/badge.svg?token=tGUFh50sIX)](https://codecov.io/gh/DASPRiD/nested-search-params)

Parse URL query strings or URLSearchParams into deeply nested JavaScript objects with support for arrays and bracket 
notation.

## Features

- Converts URL query strings or URLSearchParams into nested objects and arrays
- Supports bracket notation like `user[address][city]=NY` and array indices `foo[0]=bar`
- Lightweight and zero dependencies

## Installation

```bash
npm install nested-search-params
# or
pnpm add nested-search-params
# or
yarn add nested-search-params
```

## Usage

```ts
import { parseSearchParams } from "nested-search-params";

const nested = parseSearchParams("user[name]=Alice&user[address][city]=NY&foo[]=bar&foo[]=baz");

console.log(nested);

/*
Output:

{
  user: {
    name: "Alice",
    address: {
      city: "NY"
    }
  },
  foo: ["bar", "baz"]
}
*/
```

You can also pass a URLSearchParams instance:

```ts
const params = new URLSearchParams("a[b]=c&a[d]=e");
const result = parseSearchParams(params);

console.log(result);

/*
Output:
 
{
  a: {
    b: "c",
    d: "e"
  }
}
*/
```

## Security

This parser protects against prototype pollution by ignoring keys named `__proto__`, `constructor`, and `prototype`.

