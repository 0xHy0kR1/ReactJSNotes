### 1. Default Export:
- In this case, if import occurs by any name, Suppose XYZ, then the default value will be exported.
- It is generally used to export a single object, function, or variable.
- Example - We are creating module.mjs and module2.mjs. We will be performing a default export from module.mjs to module2.mjs
##### In module.mjs: 
```javascript
const a = 'Harry';
const b = 'Rohan';
const c = 'Aakash';
const d = 'Lovish';
const e = 'Priyanka';
export default b;
```
##### In module2.mjs
```javascript
import XYZ from './module.js'
console.log(XYZ);
```
The default exported value, which is 'Rohan'.

### 2. Named Export:
- You can't use a different name in the import and export function.
- We use Curly brackets for Named export.
- For example: Performing the same export using named export.
##### In module.mjs:
```javascript
const a = 'Harry';
const b = 'Rohan';
const c = 'Aakash';
const d = 'Lovish';
const e = 'Priyanka';
export {b};
```
##### In module2.mjs
```javascript
import {b} from './module.js'
console.log(b);
```
The value of 'b' will be imported, which is 'Rohan'. Name Exports are used to export multiple values.
