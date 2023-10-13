## Introduction
- Class components are basically ES7 Classes.
- A class Component can also receive props as Input and return HTML.
- A class component can also maintain some information that is private to that component and can use that information to describe the user interface.

## Creating class component:
- Now, whenever you create a class component, we need to include two imports that are the React and the Component class from React like this:
```jsx
import React, { Component } from 'react'
```
After this, you have to just define a class.

**Remember that for a class to become a react component. There are two simple steps.**
	- The first step is that it should extend the component class from React. Secondly, The class has to implement a render method that will return null or some HTML. Code:
```jsx
export default class App extends Component {
    render() {
        return (
            <div></div>
        )
    }
}
```

**Note** - Now to generate the class-based component skeleton, you can simply use the ‘rcc’ snippet because of our installed "react/redux extension".

### Using props in class-based component
We would be passing the title and description of the News as a prop.
![[class_based_component_props.webp]]
**Explanation:** - 
- Above, We have used a destructuring method of Javascript. It allows us to extract values from arrays and objects and lets us assign them to other variables.
- In our case, this.props is an object, and we are extracting the title and description from that object.

## Using States in Class Components
The first step is to create a state object and initialize it, and this step is usually done inside the class constructor:

### Constructor
- the constructor is a method used to initialize an object’s state in a class.
- Remember, within the constructor, we will call the super method. This is required because we extend react component class, and a call has to be made to the base class constructor.
#### Syntax:
```jsx
constructor(){
    super()
}
```

#### Creating the State object
After doing this, we create our state object. For now, let ‘this.state’ equals an empty object.
By the way, State is the reserved keyword in react. So, when you declare this.state, react understands your intention.
```jsx
constructor(){
    super()
    this.state = {
    }
}
```
**Note** - 
- **Remember,** we are using the class-based components, so don’t forget to use the ‘this’ keyword.

## Difference between Function and Class-based Component:
![[class_based_components.webp]]
