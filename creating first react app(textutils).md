# Prequisite - [[npx]] and [[npm]]
## Write the following command in your VS code terminal
```python
npx create-react-app textutils
```
Note - "textutils" is the name of our app.

## Adding CSS:
- To add CSS to your application go to app.css available under Src Folder.
- Target your element, and write your desired CSS code. 

## Adding JavaScript:
- To add JavaScript in JSX we have to write the JS code in curly brackets. 
![[Adding_js_in_JSX.webp]]
## Features of our app:
-   Word Counting.
-   Removing Extra spaces.
-   Capitalizing the text of the document.
-   Adding Lowercase and uppercase to the text.

### Navbar of our app:
First copy the navbar component from bootstrap and paste it on your app.js of inside of your return().
-   Close those tags which don't have a closing tag. 
-   Replace the ‘class’ keyword with ‘ClassName’.
-   Replace href= “#” with href= “/”
-   The code must be in one tag or use a JSX fragment.

[[exports in react]]
## Creating the Navbar Component: 
- Creating `Navbar.js` inside "Component" folder which is inside of "src" folder.
```javascript
import react from 'react'
export default function Navbar() {
    return (
        <div>
            //Code of your Navbar
        </div>)
}
```
Note - After writing the code for navbar just import it to `app.js` 
![[import_navbar.webp]]
Pre-requisite - [[props]]
## Changing Values Using Props:
- Now let's Suppose you want to use the above navbar in your different applications but with different titles and About.
- You can do so by using Props in React. 
![[props_use_example.webp]]

## Passing values to the props(In app.js):
```javascript
function app() {
    return (
        <>
            <navbar title="Textutils" aboutText="About Textutils" />
        </>
    );
}
```
- Here, we have passed the `Textutils` in props.title and `About Textutils` in props.aboutText.
Note - Remember, we can even pass objects or links, etc. 

## Setting some of the constrants(conditions) for props:

### Firstly we need to import prop types:
```javascript
import PropTypes from 'prop-types'
```

### setting the constrants(conditions):
In `Navbar.js`
```javascript
navbar.propTypes = {title: propTypes.string.isrequired, aboutText: PropTypes.string}; 
```
- It means that my prop-type of title is a string which means on passing any other value, like Number, it will show an error in the console.
- We can use `isrequired` keyword, which makes sure that we won't leave that prop blank.

## Creating a Textbox:
- For creating a Textbox in our web page we are going to create a `TextForm.js` file inside our component folder.
- inside the `TextForm.js` file we create `function-based` component by using `rfc` snippet.
![[TextForm.js_file.webp]]
**Above our Textbox in textform.js

## In app.js
- We will be importing textform.js in app.js and return it inside our app by using a function-based component.
![[app.js_importing_textform.js.webp]]
## Output of the above code
![[output_of_app_after_textform.js.webp]]

### Before doing below stuffs visit --> [[State]] and [[hook]]
- Let's pass the value of text in our textbox and make sure to use the 'Onchange' event to enable text entry in your textbox. To do so change the code of your text area to: 
```javascript
<textarea className='form-Control' value={text} Onchange={handleOnchange} id='mybox' rows= '8'></textarea>
```
##### Output after above operation
![[textbox_after_using_state.webp]]
- Now, To change the value in the textbox, we can use the set text function:
```javascript
setText("Your Text here");
```
Note - You cannot change value of the variable in React like text = "Next Text";

## Making our button function:
- We are creating a function named handleUpClick, which on being clicked will change the text of the textbox to "You have clicked on handleUpClick".
### Our function:
```javascript
const handleUpClick = () => {
    console.log("Uppercase was clicked");
    SetText("You have clicked on handleUpClick")
}
```

## Result after clicking on button:
![[result_of_button_click.webp]]

## Creating new function handleOnChange
```javascript
const handleOnChange = (event) => {
    console.log("On change");
    setText(event.target.value);
}
```
- After adding the above function you are able to add more text to your textbox.

## Changing the text Uppercase:
- We make this function to change the text to uppercase when user clicks on button.
```javascript
const handleUpClick = () => {
    console.log("Uppercase was clicked");
    let newText = text.toUpperCase();
    setText("new text")
}
```
- After adding the above function you are able to change the text to Uppercase which you enter to textbox.

## Editing textform.js
### 1.)Counting Words and Characters
![[counting_words_and_characters.webp]]
- Javascript split() is used to split the given string in an array.

### Result of above modification
![[counting_words_and_characters_result.webp]]

### 2.)Calculating Reading Time
- On average to read a single word takes 0.008 minutes.
![[calculating_reading_time.webp]]
### Result of above modification plus some extra
![[calculating_reading_time_plus_preview.webp]]

## Convert text to lowercase

### Adding Button:
```html
<button className= "btn btn-primary" onClick={handleloClick}> Convert to Lowercase</button>
```

### Adding a function:
```javascript
const handleLoClick = () => {
    console.log("lowercase was clicked");
    let newText = text.toLowerCase();
    setText("new text")
}
```

- **Result:** On clicking the button our text will change to Lowercase.

# Enable Dark Mode

## Create about.js
In the about.js we copy paste the bootstrap Accordian component.

## In app.js
comment out the textform.js and add the about.js file.
![[adding_about.js.webp]]

## Adding button
```html
<button type=“button” className=“btn btn-primary”>Enable Dark Mode</button>
```

## What our function must do?
- On invoking the function, by clicking the button, we want that dark mode to get enabled and the text in our button to change from ‘Enable dark mode’ to ‘Enable Light Mode’ and vice versa.
- To do so follow the steps: Firstly, we will add the style of dark mode to our application and then interchange it with light mode on invoking the function.

## Adding Styles of Dark mode 
```javascript
style = {myStyle}
```
- Where 'myStyle' is an object which we are using as a style variable. 

```javascript
let myStyle = {
	color : 'white', 
	backgroundColor : 'black'
}
```
**Remember** - In JS everything is in camel case

## Using this Style
After applying styles our app is appearing something like this:
![[after_applying_styles.webp]]

## Style as a State variable
We would be using two-state variables:
1. myStyle as a State variable
```javascript
const[mystyle, setMystyle] = useState({
    color: 'black',
    backgroundColor: 'white'
})
```

2. Button Text as a State variable
```javascript
const[btnText, SetBtnText] = useState("Enable Dark mode")
```

Initially, these are the State of our application and we would replace them with setMyStyle and setBtnText.

## Function
- We would like to change the style of our application on invoking a function, Suppose toggleStyle.
- For that Create a function toggleStyle and use the if-else statement to define conditions for change.
```javascript
const toogleStyle = () => {
    if (myStyle.color === "black") {
        setMyStyle({
            color: "white",
            backgroundColor: "black",
            border: "1px solid white",
        })
        setBtnText("Enable Light Mode")
    }
}
```
- The above code means if the color of text of myStyle object is black(light mode) then on clicking the button change myStyle with SetMyStyle, which is replace the color of text with white and background color with black and enable border (that is Dark Mode)
- We have also replaced the text of the button with setBtnText, which is ‘enable light mode’.

```javascript
else {
    setMyStyle({
        color: 'black',
        backgroundColor: 'white'
    })
    setBtnText("Enable Dark Mode")
}
```
- If the above-mentioned conditions are false then replace myStyle with setMyStyle, this time, which is text color being black and background color being white, and replace the text in button with “Enable Dark mode”.
- Actually, this is the same as the initial condition of our text, which is light mode is being enabled.

## Code of button
```html
<button onClick={toggleStyle} type="button" className="btn btn-primary"> {btntext}</button>
```

## Summary of About.js
![[about.js_summary.webp]]

# Making the whole web page as dark

## In app.js
- In our app.js we will create a new state
```javascript
const[Mode, setMode] = useState('light');
```
- Here, by default *light* mode state is used and we pass this to navbar component.
```javascript
<Navbar title="TextUtils" mode={Mode} />
```

## What do we want?
- We want that when our darkMode is true then, the color of our Navbar container becomes dark that is the below code of dark code is implemented otherwise the default light mode will be enabled.
```html
// For Dark mode
<nav ClassName="navbar navbar-expand-lg navbar-dark bg-dark">
//For light Mode
<nav ClassName="navbar navbar-expand-lg navbar-light bg-light">
```

- But how we will change the color of our component between light and dark for that we use javascript
```javascript
<nav ClassName= {`navbar navbar-expand-lg navbar-${props.mode} bg-${props.mode}`}>
```
- we have used $ to use props.mode as a variable and the curly brackets to specify that this is a JavaScript Code.
- We are using backticks so we can use template literals [Syntax: ${}] inside a string

## What have we done?
- We have created a state ‘mode’.
- The default value of the state is light. This value is passed to our Navbar props.mode, Which is actually the color of our Navbar.
- Hence, On changing the color in the defined state in app.js the color of the Navbar changes.

## Assigning Switch:
```jsx
<div className={`form-check form-switch text-${props.mode==='light'? 'Dark' : 'light'}`}>
    <input className="form-check-input" onClick={props.toogleMode} type="checkbox" id="flexSwitchCheckDefault" />
    <label className="form-check-label" htmlFor="flexSwitchCheckDefault">Enable DarkMode </label>
</div>
```
- Above we used ternary operators.
- Ternary operators used in place of longer if else for decision making in short line of code.

## Creating Function
- It changes the view from light to dark if our mode is light or vice versa.
#### In app.js
- We write it inside app.js.
```jsx
const toggleMode = () => {
    if (mode === 'light') {
        setMode('dark');
    }
    else {
        setMode('light');
    }
};
```
**Result - 
- At the end after clicking the button we are able to change the color of our navbar.
![[navbar_color_change.webp]]

## Enabling Dark mode for body 
#### In app.js
- Adding two more lines to our toggleMode function.
```jsx
const toggleMode = () => {
    if (mode === 'light') {
        setMode('dark');
        document.body.style.backgroundColor = 'grey';
    }
    else {
        setMode('light');
        document.body.style.backgroundColor = 'white';
    }
};
```
**Result - 
- At the end after clicking the button we are able make whole page as grey and navbar as black.
![[navbar_and_body_color_change.webp]]

## Changing Color of Text and Textbox
- Changing the color of textbox color to grey and the color of the text to white for better visibility.
- To do so we will pass the mode state variable to textform.js
```jsx
<Textform heading="Enter the text to analyze below" mode={mode}/>
```

## In textform.js
- We would like to change the color of the text to white when dark mode is enabled and vice-versa.

#### Changing the text color
- Changing CSS of the parent container and other containers.
```jsx
style={{color: props.mode==='dark'?'white':'black'}}
```

#### Changing the Background Colour of the Textbox
- changing the textbox color from white to grey.
```jsx
style={{backgroundcolour: props.mode==='dark'? 'Grey': 'white', color:props.mode=== 'dark'?'white': 'black'}}
```
- If dark mode is enabled then the textbox will become grey otherwise white.
![[textbox_background_change.webp]]

## Editing Preview Section:
- If the preview is empty we would like to see some default text written there, For that we can use the below command:
```jsx
<h2>Preview<h2>
<p>{text.length>0?text:"Enter something in the above textbox to preview it here"}</p>
```
**Result - 
![[preview_section.webp]]

## Adding Dismissing Alert Message

#### Create Alert.js
- Creating alert.js and paste the code of dismissable alert in the return().

#### Passing values as a prop
- We will be passing values in alert.js as a prop.
![[passing_props_to_alert.js.webp]]

#### In app.js
- We have created our Alert component and to render it in our application we will use <alert/> in return().
- Make sure your "Alert" component has been imported into "app.js".

#### Passing Text in props.alert from app.js
- Passing the 'This is alert' text to props.alert of the alert component as:
```html
<Alert alert= 'This is alert'/>
```

#### Passing Values as a State
- But we would like to pass text as State, for that we will create a State variable named "alert".
```javascript
const [alert, setAlert] = useState(initialState)
```
- alert is an object whose initial value is null.
- We can define value in the alert state variable by using the "setAlert" method. 
- We will be using the "showAlert" method to display the alert. 

```javascript
const showAlert = (message, type) => {
    setAlert({
        msg: message,
        Type: type
    })
}
```
- We have passed two arguments in the object which are 'message' and 'type'.
- The 'type' is actually the status of our action, like success, warning, etc.
- The 'message' is the text which will be displayed like copied to the clipboard, etc.

#### Showing alert while performing the action
- Passing alert to our Alert component instead of the text like this.
```html
<Alert alert={alert}/> 
```
- Here, alert is a object.

#### In Alert.js
- Now to render the 'type' value of object use {props.alert.type}. 
- To display the value of 'msg' use {props.alert.msg}.
![[passing_value_to_alert.js.webp]]
- If props.alert is null then the code written after "&&" won’t be shown otherwise the code inside <div></div> tag will be displayed.

#### To show alert while changing modes
- We would like to show the alert while switching between the dark and the light mode.
```javascript
const toggleMode = () => {
    if (mode === 'light') {
        setMode('dark');
        document.body.style.backgroundColor = 'grey';
        showAlert("Dark mode has been enable", "success")
    }
    else {
        setMode('light');
        document.body.style.backgroundColor = 'white';
        showAlert("Light mode has been enable", "success")
    }
```
**Result** - 
![[alert_showing_on_toggle_blackwhite.webp]]

#### Change the color of the Alert box 
![[change_alert_color_app.webp]]
- Here, By using Javascript we have changed the keyword ‘warning’ with the word which we have passed in the ‘type’, that is Success.
**Result** - 
![[change_color_alert_2_app.webp]]

#### Capitalizing the first character
- We would like to capitalize ‘s’ letter of success. To do so there is below function:
```js
const capitalize = (word) => {
    const lower = word.toLowerCase();
    return lower.charAt(0).toUpperCase() = lower.slice(1);
}
```
- To use the Capitalize function, we would use below code:
```js
{capitalize(props.alert.type)}
```
- summary of above is below:
![[alert_first_letter_capitalize_app.webp]]
**Result** - The ‘S’ character of the success word will be capitalized.

#### Show Alert message while using the features
- To do so we have to pass showAlert to our Texform component like this:
```jsx
<TextForm showAlert={showAlert} heading="Enter the text to Analyze below" mode={mode}/>
```

#### In textform.js
- In every handler of our application, we can use this showAlert method as:
```jsx
props.showAlert("Converted to uppercase!", "success");
```

#### Set Timeout for the Alert
- You might have noticed after dismissing the alert through the close button you aren’t able to see the alert again with reloading the page.

##### In app.js
- We would use ‘set timeout’ to the showAlert function as:
![[setTimeout_to_alert_app.webp]]
- Alert message will be shown to him/her which will automatically disappear after 1.5 seconds.

## Changing Meta Description
Open "index.html" available in the public folder. In "index.html" we can easily change the meta description.
![[meta_desc_change.png]]

## Changing Favicon
- In our case, We will be generating the favicon online by converting an image to ".ico" file format.
- ico is the file format used for computer icons, and paste it inside the public folder of our React application.
- In index.html replace the old name of the image with your desired one.

## Here are some of the issues in our TextUtils application:

1. Word Counting Error
2. No Mobile friendly buttons
3. No Relevant About Text 
4. The layout is shifting when an alert appears (while clicking a button)
5. The cursor is invisible in Dark mode
6. Expected Reading Time Error
7. No SEO optimization
8. Buttons are still working when the textbox is blank.
9. Deselecting the Copied Text

#### 1. Word Counting Error
- We have created the function of Counting words in our Textform.js.
- The split() method is used to convert the string into an array.
- In our case, We are splitting the string by a space and then counting the length of that array, which comes out to be one. Therefore, a blank space is being counted as a word.

**Solution** - 
- The quick way of fixing this error is by removing the empty strings from the split array.
- We can easily do so by using the filter method in our Text.split function as described below:
```js
{text.split(" ").filter((element)=>{return element.length!==0}).length}
```
- The arrow function `(element) => {return element.length !== 0}` checks whether the length of each `element` in the array is not equal to zero. If the length is not zero (i.e., the element is not an empty string), it is included in the new filtered array.
- For example, using the previous array `["Hello", "World"]`, the filter will remove any empty strings (if any), and the result will still be `["Hello", "World"]`.

#### 2. Adding Mobile-Friendly Buttons
![[not_mobile_friendly_buttons.webp]]
- The above error is occurring as there is no margin for the buttons in the Y direction.
- To solve this issue add some margin to the buttons, available in "textform.js", in the Y direction

#### 3. Enhancing "about.js"
![[aboutjs_problem.webp]]
We would remove the Dark mode button of the Accordion and also the ToggleStyle function assigned to it from about.js. We are adding our desired text in Accordion and editing it in our own way.

**Adding a proper Dark Mode** **to about.js**
To add dark mode to our about.js, follow the below steps.

**Step 1:** Firstly, Pass Mode in About component of App.js as
```js
<About mode={mode}/>
```

**Step 2:** We would create a new ‘myStyle’ variable which would provide our desired design to the About page, on enabling the dark mode.
```js
let myStyle = {
    color: props.mode === 'dark'?'white':'#042743',
    backgroundColor: props.mode ==='dark'?'rgb(36 74 104)':'white'
}
```

#### 4. Layout Shifting Issue
- The layout of our application is shifting when an alert is shown. Remember that the layout shift must be minimum for your application, as this is one of the ranking factors from the SEO point of view.
- **Solution** - To resolve the issue, go to your "alert.js", and inside the alert component, we would wrap the alert inside a div container having a specific height.
![[alert_issue.webp]]
As a result, the Alert component will have a specific height for its display.

#### 5. Expected Reading Time Error
- Our application will be showing the expected time to read the provided text, but if the Textbox is blank then also our Time counter is showing an expected time to read the text.
- To fix this bug in our application, we would use the filter method as we have used to solve the counting word error.
```js
<p>{0.008 * text.split(" ").filter((element)=>{return element.length!==0}).length} Minute read </p>
```

#### 6. Fixing for SEO
- SEO is one of the factors which helps our website to rank on Google.
- To make our application SEO optimized we would make the following changes to our Index.html and Textform.js:
**In index.html:**
**Meta Description:**
-  It provides a brief sketch of the content of the website to the Google crawler.
- Therefore, it becomes utterly important to add specific keywords related to our content in the meta description.
**Title**:
- It specifies the Content of our specific web pages. Hence, we have changed the title of our application by adding some relevant Keywords to it.
![[seo_optimized.webp]]

**In textform.js:**
**Editing Headings**:
- It plays a major role in the SEO optimization of our website as it makes it easier for a User and Crawler to navigate through the page.
- We will be passing a new heading, having relevant keywords related to our application, in props.heading from app.js.
![[seo_optimized2.webp]]
**We have optimized our app for search engines.**

#### 7. Disable button
When our Textbox is empty, but our buttons are working and performing their functions, which seems like a bug to our application.
**Solution:** To overcome this issue, we would add the below code to every button.
```js
disabled={text.length===0} 
```
This code means to disable the buttons when the length of the text is 0. That is, the textbox is empty.

Error has been **successfully** resolved.

#### 8. Word Counting Error
![[word_counter_prob.webp]]
- This issue occurs as we have forgotten to split the string with a new line.
- We would like to split it by space and a new line. To do so, Go to textform.js where we have written the code for counting words, and edit it as follows:
```js
<p>{text.split(/\s+/).filter((element)=>{return element.length!==0}).length} words and {text.length} characters</p>
```
Here, We are using the regular expression(regex) instead of space. The \s is the common shorthand in regex for any whitespace character, including newlines and ‘+’ denotes more than one.
![[word_counter_sol.webp]]

#### 9. About page arrow Invisibility
- In the dark mode, the side arrows in the accordion component of our About Page disappear due to their matching color with the background.
- We can easily fix this issue by adding the below CSS code to accordion-button::after in index.css.
```css
.accordion-button::after {
    filter: invert(1);
}
```
![[back_arrow_color.webp]]

