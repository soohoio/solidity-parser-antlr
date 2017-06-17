solidity-parser-antlr
=====================

[![npm](https://img.shields.io/npm/v/solidity-parser-antlr.svg)](https://www.npmjs.com/package/solidity-parser-antlr)
[![Build Status](https://travis-ci.org/federicobond/solidity-parser-antlr.svg?branch=master)](https://travis-ci.org/federicobond/solidity-parser-antlr)

A Solidity parser built on top of a robust [ANTLR4 grammar](https://github.com/solidityj/solidity-antlr4).

### Usage

```javascript
import parser from 'solidity-parser-antlr';

var input = `
    contract test {
        uint256 a;
        function f() {}
    }
`

parser.parse(input)
```

The `parse` method also accepts a second argument which lets you specify the
following options, in a style similar to the _esprima_ API:

| Key      | Type    | Default | Description                                                                                                                                                                                 |   |
|----------|---------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
| tolerant | Boolean | false   | When set to `true` it will collect syntax errors and place them in a list under the key `errors` inside the root node of the returned AST. Otherwise, it will raise a `parser.ParserError`. |   |
| loc      | Boolean | false   | When set to `true`, it will add location information to each node, with start and stop keys that contain the corresponding line and column numbers.                                         |   |
| range    | Boolean | false   | When set to `true`, it will add range information to each node, which consists of a two-element array with start and stop character indexes in the input.                                   |   |


#### Example with location information

```javascript
parser.parse('contract test { uint a; }', { loc: true })

// { type: 'SourceUnit',
//   children: 
//    [ { type: 'ContractDefinition',
//        name: 'test',
//        baseContracts: [],
//        subNodes: [Array],
//        kind: 'contract',
//        loc: [Object] } ],
//   loc: { start: { line: 1, column: 0 }, end: { line: 1, column: 24 } } }

```


### Author

Federico Bond ([@federicobond](https://github.com/federicobond))

### License

GPL 3.0
