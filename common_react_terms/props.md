- props stand for properties.
- It is used to Pass information into the React Components.
- For example, if we create a custom Component, then by using Props, we can pass data into it in the form of Objects, strings, numbers, etc.
- `ES7React/redux/GraphQL/React-native snippets` is a very useful extension while working in React, as it provides a shortcut way to write code. 
- For example: if you type 'imp' then it will print:
  ```js
  import moduleName from 'module'
```
- importing protypes-
```javascript
import PropTypes from 'prop-types'
```
1. String/object/Number Prop-Type
```javascript
navbar.propTypes = {title: propTypes.string.isrequired, aboutText: PropTypes.string}; 
```
- It means that my prop-type of title is a string which means on passing any other value, like Number, it will show an error in the console.
- We can use `isrequired` keyword, which makes sure that we won't leave that prop blank.
2. Default Prop-Type 
```javascript
navbar.defaultProps = {
    title: 'Set title here',
    aboutText: 'About text here'
};
```