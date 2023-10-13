## Why use React Router?
**It enables the creation of single-page web or mobile apps that allow navigating without refreshing the page**.

## Install React Router package
```js
npm install react-router-dom
```
Once you have installed it, just go to the package.json file, and you will see the react-router-dom package right there.

## Setting Up routing for our application
**Procedure:**
```js
import { BrowserRouter, Route, Routes } from "react-router-dom";
```

1. **Using BrowserRouter:**
	- Now, we want to surround our entire application with the BrowserRouter component and what that means is we can use the router in the entire application.
	- As a result, all components that are nested inside this app component(app.js) get access to the BrowserRouter.
**Use:**
```jsx
<BrowserRouter></BrowserRouter>
```

2. **Using Routes**:
	- The Routes component makes sure that only one route shows at any one time. All of our routes go inside this Routes component.
**Use**:
```jsx
<Routes></Routes>
```

3. **Using Route**:
	- Alright, we need to set up our individual routes for the About and Home page. So, we will create a route for each page, for which we will be using the route component(route).
**Use**:
```jsx
<route></route>
```

4. **Add property to Route**:
	- Now, we are going to add the "exact path" property to the route. The "exact path" is basically the route, so for the home page, it would just be forward slash [‘/’].

**For Home Page:**
```jsx
<Route exact path="/" element={ <TextForm showAlert={showAlert} heading="Try TextUtils - Word Counter, Character Counter, Remove extra spaces" mode={mode}/>} />
```
We would link to render our text form component whenever someone visits the forward-slash route.

**For About Page:**
Similarly, for the about page, it would be Forward slash about (/about). 
Something like this:
```jsx
<Route exact path="/About" element={ <div className="container">  <About mode={mode} />  </div>} />
```

**Problem**:
in that case, your application will be sending the fresh request to the server each time whenever you click on "About" and navigate to home page, which we don’t want to happen as it will reload the page each time, just as a normal application.

5. **Using 'Link to' tag:**
	- To overcome this issue, instead of an Anchor tag, we will be using a special type of tag known as link tag.
	- The first thing we are going to do is import the link tag in Navbar.js as:
```jsx
import { Link } from 'react-router-dom'
```

**Now we can replace the anchor tag with link to tag as follows:**
```jsx
<a href= "/">Home</a>
<a href= "/about">About</a>
```
**Change the code to:**
```jsx
 <Link to="/">Home</Link>
 <Link to="/About">About</Link>
```

**Result**: You can now navigate between your About and Home page very quickly
**Point to be Noted:** The Navbar component of our application will always show up because it’s not inside the Routes statement.

### In a Nutshell:
Here is the short summary of this concept:
![[router_setup1.png]]
Remember you must use an ‘exact’ parameter with the Route component as it disables the partial matching of the route and makes sure that it only returns the route if the path is exact.
