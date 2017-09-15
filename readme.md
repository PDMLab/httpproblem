# Create problem+json documents  with Node.js

`problem-json` is a small library that allos you to create `problem+json` documents according to [RFC 7808](https://tools.ietf.org/html/rfc7807).

## Installation

```
npm install --save-dev problem-json
```

## Usage

`problem-json` current supports these options:

* `type` (string) - A URI reference [[RFC3986](https://tools.ietf.org/html/rfc3986)] that identifies the problem type.
* `title` (string) - A short, human-readable summary of the problem type.
* Extension Members - Provide additional information.

### Example

To generate this `problem+json` result

```json
{
    "type": "https://example.com/probs/out-of-credit",
    "title": "You do not have enough credit.",
}
```

this code is required:

```javascript
const httpProblem = require('problem-json');

const doc = new httpProblem.Document({
  type: 'https://example.com/probs/out-of-credit',
  title: 'You do not have enough credit.'
});
```

### Example with Extension Members

To generate this `problem+json` result

```json
{
    "type": "https://example.com/probs/out-of-credit",
    "title": "You do not have enough credit.",
    "balance": 30,
    "accounts": ["/account/12345", "/account/67890"]
}

```

this code is required:

```javascript
const httpProblem = require('problem-json');

const extension = new httpProblem.Extension({
  balance: 30,
  accounts: ["/account/12345", "/account/67890"]
});

const doc = new httpProblem.Document({
  type: 'https://example.com/probs/out-of-credit',
  title: 'You do not have enough credit.'
}, extension);
```

## What's missing?

`problem-json` currently lacks support for `detail`-, `status`- and `instance`-Members. Also conventions for `type` are not implemented yet.

## Running the tests

While `docker-compose` runs on Node.js 6+, running the tests requires you to use Node.js 8 as they make use of `async/await`.

```
npm test
```

## Want to help?

This project is just getting off the ground and could use some help with cleaning things up and refactoring.

If you want to contribute - we'd love it! Just open an issue to work against so you get full credit for your fork. You can open the issue first so we can discuss and you can work your fork as we go along.

If you see a bug, please be so kind as to show how it's failing, and we'll do our best to get it fixed quickly.

Before sending a PR, please [create an issue](https://github.com/PDMLab/docker-compose/issues/new) to introduce your idea and have a reference for your PR.

Also please add tests and make sure to run `npm run eslint`.

## License

MIT License

Copyright (c) 2017 PDMLab

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
