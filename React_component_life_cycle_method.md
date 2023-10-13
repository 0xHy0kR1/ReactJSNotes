## React Component Lifecycle Method
The three phases are: **Mounting**, **Updating**, and **Unmounting**.

**Component LifeCycle:** The series of events that happens from the mounting of a React Component to its unmounting.

Each component in React has a lifecycle which you can monitor and manipulate during its three main phases.

1. **Mounting:** Birth of your component
2. **Update:** Growth of your component
3. **Unmount:** Death of your component

### Methods in React Component Lifecycle

1. **render() Method:** 
	- It is used to render the HTML of the component in React.
	- It is used to render the DOM while using the class-based component.
	- Remember, Inside the Render method we cannot modify the state in React.

2. **componentDidMount():**
	- This method executes after the component output has been rendered to the DOM.
	- We have already used this method in the NewsMonkey Application for fetching the Data from the API.
	- You can also use setState, async, and await methods in ComponentDidMount().

3. **componentDidUpdate():**
	- This method is used to update the DOM in response to the prop or state changes.
	- Remember that props are read-only. That’s why here, `changes in the prop` means that it can be received again in the component.

4. **componentWillUnmount():**
	- It is invoked just before the component is unmounted and destroyed.
	- It is usually used to perform cleanups.

These are the four most commonly used React Component Lifecycle methods.

### React Lifecycle methods diagram by wojtekmaj.pl
![[react_component_life_cycle_methods_dia.webp]]

**Here’s the sequence of the methods that will run while Mounting, Unmounting, Updating the React component.**
#### While Mounting - 
In this case, the ‘Constructor’ runs first after that the ‘render’ lifecycle method is invoked. After that, React will update the DOM and finally, the ComponentDidMount will be executed.

#### While updating - 
The three possible ways in which one can update the React component are:
1. New props
2. Using setState
3. Using forceupdate()

**After updating the component, the render method will be executed at the start. After that react updates the "DOM and references" and in the end, the componentDidUpdate method will be run.**

#### While Unmounting - 
At the time of unmounting, only the componentWillUnmount method will be executed and the component will be unmounted.