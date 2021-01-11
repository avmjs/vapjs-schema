## vapjs-schema

<div>
  <!-- Dependency Status -->
  <a href="https://david-dm.org/vapjs/vapjs-schema">
    <img src="https://david-dm.org/vapjs/vapjs-schema.svg"
    alt="Dependency Status" />
  </a>

  <!-- devDependency Status -->
  <a href="https://david-dm.org/vapjs/vapjs-schema#info=devDependencies">
    <img src="https://david-dm.org/vapjs/vapjs-schema/dev-status.svg" alt="devDependency Status" />
  </a>

  <!-- NPM Version -->
  <a href="https://www.npmjs.org/package/vapjs-schema">
    <img src="http://img.shields.io/npm/v/vapjs-schema.svg"
    alt="NPM version" />
  </a>

  <!-- Javascript Style -->
  <a href="http://airbnb.io/javascript/">
    <img src="https://img.shields.io/badge/code%20style-airbnb-brightgreen.svg" alt="js-airbnb-style" />
  </a>
</div>

<br />

The complete Vapory RPC specification as a JSON object export.

## Install

```
npm install --save vapjs-schema
```

## Usage

```js
const schema = require('vapjs-schema');

console.log(schema.tags);

// result ['latest', 'earliest', ...]
```

## About

This is a pure JSON export of the Vapory RPC specification. This can be, and is being used to generate the `vapjs-query` object. This object specification is not standardized, it is the leanest data structure implementation I could come up with for the Vapory RPC spec.

The entire spec is contained in the [schema.json](src/schema.json) file.

## Specification Details

### Method Specification:

  ```
  methods: {
    <method name : [ input(s), output(s), minimum required outputs, 'latest' tag default position (if any) ] >,
  }
  ```

  example:

  ```
  {
    methods: {
      "vap_getBalance": [["D20", "Q|T"], "Q", 1, 2],
      ...
    },
    ...
  }
  ```

### Primitives:

  - "D" : bytes data
  - "D20" : bytes data, length 20
  - "D32" : bytes data, length 32
  - "B" : boolean true or false
  - "S" : string data
  - "Array|DATA" : either an array of DATA or a single bytes DATA
  - "Q" : a number quantity
  - "QP" : a number quantity (with frontal padding)
  - "Q|T" : a number quantity or a tag (e.g. 'latest', 'earliest' ...)

Note, post version 0.1.1 value primitives have been compressed.

### Tags:

  ```
  {
    "tags": ["latest", "earliest", "pending"],
  }
  ```

### Complex Data Structures (.objects):

The `__required` property is added to specify which properties of the object must be fulfilled in order to be a valid object structure (ready for payload transmission).

  - "VapSyncing"
  - "SendTransaction"
  - "EstimateTransaction"
  - "CallTransaction"
  - "Block"
  - "Transaction"
  - "Receipt"
  - "Filter"
  - "FilterChange"
  - "SHHPost"
  - 'SHHFilter'
  - "SHHFilterChange"
  - "SHHMessage"

  example:

  ```
  {
    "objects": {
      "SendTransaction": {
        "__required": ["from", "data"],
        "from": "D20",
        "to": "D20",
        "gas": "Q",
        "gasPrice": "Q",
        "value": "Q",
        "data": "D",
        "nonce": "Q"
      },
      ...
    }
    ...
  }
  ```

## Contributing

Please help better the ecosystem by submitting issues and pull requests to default. We need all the help we can get to build the absolute best linting standards and utilities. We follow the AirBNB linting standard and the unix philosophy.

## Guides

Please see the Vapory RPC specification hosted on their github:

https://github.com/vaporyco/wiki/wiki/JSON-RPC

## Help out

There is always a lot of work to do, and will have many rules to maintain. So please help out in any way that you can:

- Create, enhance, and debug vapjs rules (see our guide to ["Working on rules"](./github/CONTRIBUTING.md)).
- Improve documentation.
- Chime in on any open issue or pull request.
- Open new issues about your ideas for making `vapjs-schema` better, and pull requests to show us how your idea works.
- Add new tests to *absolutely anything*.
- Spread the word.

Please consult our [Code of Conduct](CODE_OF_CONDUCT.md) docs before helping out.

We communicate via [issues](https://github.com/vapjs/vapjs-schema/issues) and [pull requests](https://github.com/vapjs/vapjs-schema/pulls).

## Important documents

- [Changelog](CHANGELOG.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [License](https://raw.githubusercontent.com/vapjs/vapjs-schema/master/LICENSE)

## Licence

This project is licensed under the MIT license, Copyright (c) 2016 Nick Dodson. For more information see LICENSE.md.

```
The MIT License

Copyright (c) 2016 Nick Dodson. nickdodson.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
