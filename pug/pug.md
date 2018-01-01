#Pug

ps: Medium article follow it: Mark P.

```js
> npm i -D apply-loader pug pug-loader --save-dev
```

Create pug-rule-insert.js beyong protactor.js 

pug-rule-insert.js
```js
const fs = require('fs');

const commonCliConfig = 'node_modules/@angular/cli/models/webpack-configs/common.js';
const pug_rule = `\n{ test: /\.pug$/, loader: "apply-loader!pug-loader?self" },`;

fs.readFile(commonCliConfig, (err, data) => {
  if (err) { throw err; }

  const configText = data.toString();

  if (configText.indexOf(pug_rule) > -1) {
    return;
  }

  console.log('-- Inserting .pug webpack rule -- ');

  const position = configText.indexOf('rules: [') + 8;
  const output = [configText.slice(0, position), pug_rule, configText.slice(position)].join('');

  const file = fs.openSync(commonCliConfig, 'r+');
  fs.writeFile(file, output);
  fs.close(file);
});

```
node_modules/@angular/cli/models/webpack-configs/common.js

add in the rules: 
```js

  rules: [
                { test: /.pug$/, loader: "apply-loader!pug-loader?self" },
```

### package.json
```js
"postinstall": "node pug-rule-insert.js"
```

## app.ts and change .html to .pug
```html
extends header.pug or header with no .
```

### Ref to html
http://html2jade.org/
