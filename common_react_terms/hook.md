- Hook allows you to use state and other react features with a function-based component, that is without writing a class.

## useState
- It is the type of hook in react which allows us to use state variables in the function-based components.

## Steps to use state:
- Firstly, import the state to your react app by using the below command in app.js
```javascript
import React, { useState } from 'react';
```

- To use state, firstly enter the following code inside your function-based component.
```javascript
const [text, setText] = useState('Enter Text here2');
```
- Here, the value of our text is 'Enter Text here2'.

- Let's pass the value of text in our textbox and make sure to use the 'Onchange' event to enable text entry in your textbox. To do so change the code of your textarea to: 
```javascript
<textarea className='form-Control' value={text} Onchange={handleOnchange} id='mybox' rows= '8'></textarea>
```
##### Output after above operation
![[textbox_after_using_state.webp]]
