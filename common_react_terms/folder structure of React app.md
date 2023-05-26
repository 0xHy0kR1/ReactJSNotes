	1. node_modules: It contains all the packages, which are used by React app.
1. .gitignore: It contains the files, which you do not want to push in Github.
2. package.json: Contains all the packages which are installed in Node modules.
3. readme.md: It provides the basic info about your app.

## The two folders in which we are interested are:
1. "public" folder: It contains an index.html file.
	 - index.html: It is the main HTML file of our react app. This is the page that is displayed on starting our application. it has an empty div tag like this:
	 ```html
<div id="root"></div>
```
2. "src" folder:

Two most important files in the src folder are: 
1. index.js: 
	- It is the main entry point for the application, and it is responsible for rendering the root component into the DOM, typically by using the `ReactDOM.render()` method.
2. app.js: 
	- It is the root component of the application, and it contains the main logic and layout for the application. It typically imports other components and renders them as needed. 
![[app.js_and_index.js_ex.webp]]

## How to run your React app?
- write **npm start** in terminal and your react app will be served at _localhost:3000_
-  You can use **npm run build** if you are creating an app for production.