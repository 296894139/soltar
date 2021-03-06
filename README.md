# soltar
Generate Solidity Code from its Abstract Syntax Tree. (The AST must follow the Spider Monkey API for defining AST nodes).

#Application
Don't like your peers' Solidity coding style? Always getting into the tabs vs. spaces debates? But still gotta comply with a standard style that everybody follows? No problem!

Write your Solidity code with style that aesthetically pleases you, generate its AST and give it to Soltar to generate code in a standard style your company follows.

Now **you get to work with your own style** on your local machine and **push the code with style that pleases your boss**!

#AST!

A couple of modules exist for you to generate AST of your Solidity Code:

[solidity-parser](https://github.com/ConsenSys/solidity-parser) (by **tcoulter** from Consensys)

```bash
npm install --save solidity-parser
```

[solparse](https://github.com/duaraghav8/solparse) (I'm the author)

```
npm install solparse
```

#Installation
```bash
npm install --save soltar
```

#Documentation

To use Soltar in Browser, include:

```html
<script src="soltar-bundle.js"></script>
```

You can then access the Soltar object by using ```window.Soltar``` or simply ```Soltar```.

In order to access Soltar's functionality in Node.js, ```require()``` it like:
```js
let Soltar = require ('soltar');
```

#API

1. **generate** - The main function that takes 2 arguments:
ast (the Solidity Code's abstract syntax tree (following the Spider monkey API) &
options (optional) to confgure the output

2. **version** - Get version information

#Example
A typical AST would look like:

```json
{
  "type": "Program",
  "body": [
    {
      "type": "ExpressionStatement",
      "expression": {
        "type": "AssignmentExpression",
        "operator": "=",
        "left": {
          "type": "DeclarativeExpression",
          "name": "myVar",
          "literal": {
            "type": "Type",
            "literal": "uint",
            "members": [],
            "array_parts": [
              3
            ]
          },
          "is_constant": false,
          "is_public": false,
          "is_memory": false
        },
        "right": {
          "type": "ArrayExpression",
          "elements": [
            {
              "type": "Literal",
              "value": 1
            },
            {
              "type": "Literal",
              "value": 2
            },
            {
              "type": "Literal",
              "value": 3
            }
          ]
        }
      }
    }
  ]
}
```

The default options configuration is:
```js
let options = {
	format: {
		indent: {
			style: '\t',
			base: 0
		},
		newline: '\n',
		space: ' ',
		quotes: 'single',
		minify: false
	}
}
```

##Usage

```js
/*
	AST is the solidity-parser generated Abstract Syntax Tree
	soltar is the require()d object
*/

let options = {
	format: {
		indent: {
			style: '\t',
			base: 0
		},
		newline: '\n\n',
		space: ' ',
		quotes: 'double'
	}
};
	
let sourceCode = soltar.generate (AST, options);

console.log (sourceCode);
```

##Output

```
contract Vote {

	address public creator;
	
	function Vote () {
	
		creator = msg.sender;
		
	}
	
}
```

The above solidity code corresponds to [this](https://github.com/duaraghav8/soltar/blob/master/examples/customized-options/AST.json) Abstract Syntax Tree

See **examples** for a [full contract](https://github.com/duaraghav8/soltar/tree/master/examples/full-contract) example.

#Future enhancements:

	1. Commandline utility
