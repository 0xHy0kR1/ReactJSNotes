## Create a React App
Open Windows Powershell (shortcut: Shift + Right-click in folder ) and run below command as follows:
```powershell
PS S:\Reactjs\Reactjs_codes\newsapp> npx create-react-newsapp
```

## The component structure of our application
![[component_structure_second_app.webp]]

**Navbar Component:**
- It will have navigation of different pages of our application, like About, Home, etc pages.

**News Component:**
- The big red component is the News component. It will contain a lot of ‘NewsItem’ components.

**NewsItem Component:**
- Many of these items will be specific news. For example Weather news, Sports News, Politics news, etc.

**News Detail Component:**
- I would like to point out that later on, we would create a ‘NewsDetail’ Component.
- This component will show details of specific news when the reader clicks on a specific NewsItem. Our navbar will remain intact at the top of the application.
![[second_app_news_detail.webp]]

**Benefits**:
Structuring our app in this way lets us easily manage our application and also helps in reusing the components again and again.

# Getting Started With NewsMonkey
## Using Bootstrap
- Visit getBootstrap.com and copy-paste the starter Template of Bootstrap in your "Index.html" file.
- Make sure to remember the below points while copying the code from Bootstrap:
	1. Close those tags which don’t have a closing tag
	2. Replace the "Class" keyword with "ClassName"
	3. Replace href= “#” with href= “/”

## Changing Title and meta description
![[second_app_ti_desc.webp]]

## Navbar component
we would copy-paste the code of the Navbar component from Bootstrap.

### Using Navbar component
We know that "App.js" is the file that is being rendered in our application. So, We have to use this Component in our "App.js" to render it in our application.
![[second_app_navbar_component.webp]]

## News Component
‘news’ component, that would reside in the center of our application, and it will contain all the NewsItem components. So let’s create a new file:

### News.js:
- Create a "news.js" file and add a Class-based component to it.
- After doing so, we would add this component to our "App.js".
![[second_app_newsjs_add_app.webp]]

### "NewsItem.js"
- Create a "NewsItem.js" file and add a Class-based component to it.
- After doing so, we would add this component to our "News.js".
- Hence, Our News.js file is being rendered in app.js and the News.js file contains our NewsItem Component.
![[second_app_newsjs.webp]]

## Fetching API Key from News API

## News API
- We would be using a News API to render news in our news monkey Application.
- To check out the news API, click [here](https://newsapi.org/)
- After you are logged in, you will see your live API key in every example.
- We would be using the Top headlines Endpoint for our application.
![[second_app_newsApi.webp]]

**In order to use newsApi, copy the Definition Url and search for it on the internet to get the example response News as shown below:**
![[second_app_newsApi_sample_response.webp]]

**Note:**
We are getting the output as a parsed JSON because we have installed ‘[JSON view](https://chrome.google.com/webstore/detail/jsonview/gmegofmjomhknnokphhckolhcffdaihd?hl=en)’ extension. We will disable the extension and will copy the raw JSON code.
![[second_app_raw_api_data.webp]]

### Using NewsAPI in News Monkey
- Create a new file named sampleOutput.json and paste the sample response code into it.
- Remember, It is just a piece of sample news and not real-time news. These sample articles will act as our News Item. As for now, we have four articles.
![[second_app_sample_news.webp]]

### Enhancing News Item Component
We would like to use Cards to display our NewsItems. So, Copy the code of your desired card and paste it inside NewsItem.js as shown below:
![[second_app_newsitem_card.webp]]

Now, we will change the Title and Description of every card. To do that, we will be taking the title and description as a prop in the NewsItem.

### Using props in class-based component
We would be passing the title and description of the News as a prop.
![[class_based_component_props.webp]]
**Explanation:** - 
- Above, We have used a destructuring method of Javascript. It allows us to extract values from arrays and objects and lets us assign them to other variables.
- In our case, this.props is an object, and we are extracting the title and description from that object.

### Adding Title and Description
For the demo, We are passing the title as ‘myTitle’ and the description as ‘mydesc’ in the NewsItem from News.js.
![[second_app_newsItem_title_desc.webp]]

**Result** - 
![[second_app_title_desc_newsItem.webp]]

### Enhancing NewsMonkey
Here, We are providing a grid layout to our cards.
![[second_app_news_enhance.webp]]

**Result** -
![[second_app_enhance_news.webp]]

### Adding Sample Images to card
In the sample response code of news API, we are provided with a Sample Image URL. We can use this URL in the ‘img src’ tag of the NewsItems Card.
![[second_app_sample_newsapi_output.webp]]

**Result**:
![[second_app_news_url_img.webp]]

## Passing ImageURL as a Prop
First of all, you have to use the Image Url with the props object. After that, We would pass the image URL in the ‘img src’ tag.
![[second_app_img_url_props_pass.webp]]

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

### Create a variable
Here, we will be creating an article variable. We would be using all the articles of ‘sampleoutput.json’ in this article variable as an array.

#### Accessing this array
- We can easily access this array from the constructor by using ‘this.articles’ in the state.
- We can even add some more properties in this.state
**Example** - 
we are adding a loading property to our application.
![[second_app_article_state_use.webp]]

## Rendering Articles in NewsItems
Now, We want to iterate the articles array present inside the state, and then we would render these articles in our NewsItem Component.

### Iterating the Array
Initial state of our news.js(default title, description and many more...)
![[newsjs_initial.webp]]

**The title, description, and URL to an image of an article are already provided in the sample response as shown below:**
![[second_app_sample_response.webp]]
We want to change the values of Title, Description, and Image URL from the previously passed values to the values provided in the sample response of the article.

## Getting Started
- To do that, first of all, we have to iterate the articles array and then render its data in the NewsItem. We can do so by using the map() method.
- **map() method:**
	- The map() method is the most commonly used function to iterate over an array of data in JSX.
	- You can attach the map() method to the array and use a callback function that gets called for each iteration.
![[second_app_map_method.webp]]
**Explanation:**
- In our case, The map would go through each of the objects in the array, and it will make each individual array item available to us as an element.
- Notice, Inside the arrow function, we have returned the NewsItem Component.

**Result:**
![[second_app_after_map_func_add.webp]]

## Passing Title, Description, and URL to Image
Now, let’s begin passing the provided values of articles in our NewsItem Components.
![[second_app_pass_values.webp]]

**Result:**
![[second_app_after_value_pass.webp]]

## Making the 'ReadMore' button Functional
We would like to display the complete News in a New Tab whenever the user clicks on the ‘ReadMore’ button.
To do so, we would add a newsUrl. We would be passing the value of the URL of the respective article to newsUrl.
![[second_app_read_more_button.webp]]

**We would be passing the URL of the respective article in it from News.js as shown below:**
![[second_app_pass_url.webp]]

## Enhancing the Structure
- The length of all the NewsItems Cards isn’t equal due to this, our NewsMonkey application is looking destructured. Therefore, To fix this issue, we would limit the length of visible characters in the title and description of the NewsItems Cards.
- This can be accomplished by using the slice method of Javascript as shown below:
![[second_app_text_slice_title_desc.webp]]

**Result** - 
![[second_app_slice_text_result.webp]]

## News API
First of all, you have to visit the News API website. You will get a lot of the latest news categories, which you can use in your application.

## Removing the article variable and State
As of now, we will render the data in our application from the endpoints. For that purpose, we will change the articles with the help of the componentDidMound method.

## componentDidMount() method
- This method gets invoked once the component has been rendered.
- As a result, the constructor of our application gets executed first, followed by the ‘render method,’ and at last, the ComponentDidMount() method is invoked.

**Note** - ComponentDidMount() is a lifecycle method.

## Fetch data in React using the async/await syntax

**First of all, we would use our copied News URL in the component Did Mount method as a variable. This URL will help in fetching the News in our application.**
```jsx
componentDidMount(){
    console.log("cdm");
    let url = "https://newsapi.org/v2/top-headlines?country=in&apikey=dbe57b028aeb41e285a226a94865f7a7";
}
```


**After that, we would be using the Fetch API. Remember, the fetch API takes a URL and returns a promise. Here, how you can use the fetch API:-**
```jsx
componentDidMount(){
    console.log("cdm");
    let url = "https://newsapi.org/v2/top-headlines?country=in&apikey=dbe57b028aeb41e285a226a94865f7a7";
    let data = fetch(url);
}
```

## Using Async and Await
- Async keyword is used to make a function asynchronous.
- Async can wait inside its body to resolve for some of the promises.
- The await keyword will stop the execution until a defined task is completed.
- In our case, it will wait for the promise to be resolved.
```jsx
async componentDidMount(){
    console.log("cdm");
    let url = "https://newsapi.org/v2/top-headlines?country=in&apikey=dbe57b028aeb41e285a226a94865f7a7";
    let data = await fetch(url);
    console.log(parsedData);
}
```
Once, The promise is resolved, it would provide us the data. We can parse the data as text or JSON.

**After that, we would use the setState method to set the state of the articles as parsed Data articles.**
```jsx
async componentDidMount(){
    console.log("cdm");
    let url = "https://newsapi.org/v2/top-headlines?country=in&apikey=dbe57b028aeb41e285a226a94865f7a7";
    let data = await fetch(url);
    let parsedData = await data.json()
    console.log(parsedData);
    this.setState({ articles: parsedData.articles })
}
```

## Resolving “Cannot Read property ‘slice’ of null” Error
- This Error occurs as some of the values, such as title, description, are null for some of the articles. Due to this, we can’t use the slice() method to set the limit of the characters.
- To resolve this issue, we would be using the ternary operators as follow:
```jsx
<div className="row">
    {this.state.articles.map((element)=>{
    return <div className="col-md-4" key={element.url}>
        <NewsItem title={element.title?element.title.slice(0, 45):""}
            description={element.description?element.description.slice(0, 88):""} imageUrl={element.urlToImage}
            newsUrl={element.url} />
    </div>
    })}
</div>
```

**Explanation:** - 
Now, If in case the element title or description is Null, then a blank space will be rendered, that is the else statement. Otherwise, the sliced content will be rendered in our NewsItems.

**Our Application**:
![[second_app_after_slice_error.webp]]

## Resolving the ‘Image Not Rendering’ Issue
Our application is quite astounding, but for some of the NewsItem Components, the image isn’t rendering in the NewsItem.
![[second_app_image_error.webp]]

**Here, the image is null for one of the Articles. Due to this reason, the image isn’t rendering in Our NewsItem. To resolve this issue, we would use a default Image URL when the ‘Url to the image of article’ is Null.**
```jsx
<img src={!imageUrl?"https://fdn.gsmarena.com/imgroot/news/21/08/xiaomi-smart-home-india-announcements/-476x249w4/gsmarena_00.jpg":imageUrl} className="card-img-top" alt="..."/>
```

## Creating Page Parameter State
- We have found that only some of the articles are being rendered in the News Monkey application. The other articles are rendered on the Next Page.
- We would be fetching the remaining articles on the Next Page of the NewsMonkey application. For that, we would firstly add a page parameter to the state as follow:
```js
constructor(){
    super();
    this.state = {
        articles: [],
        loading: false,
        page: 1
    }
}
```

## Creating Previous and Next Buttons
Here, we have added an arrow to the buttons and have even aligned the buttons perfectly.
![[button_align.webp]]

## Adding the Onclick Function to the Buttons
Now, we want to render the next set of News by clicking the Next Button and the previous news by navigating through the previous button. For that reason, we would assign an OnClick function to the buttons.
```jsx
<div className="container d-flex justify-content-between">
    <button type="button" class="btn btn-dark" onClick={handlePrevClick}> &larr; Previous</button>
    <button type="button" class="btn btn-dark" onClick={handleNextClick}>Next &rarr;</button>
</div>
```

## Disabling Next And Previous button at a certain instance
```js
<div className="container d-flex justify-content-between">
    <button disabled={this.state.page<=1} type="button" class="btn btn-dark" onClick={handlePrevClick}> &larr;
        Previous</button>
    <button type="button" class="btn btn-dark" onClick={handleNextClick}>Next &rarr;</button>
</div>
```
This parameter only renders the specific articles on a single page. For example, if the page size parameter is equal to ‘two’ then only ‘2’, of all the articles, will be rendered in the application.

## Math.ceil() method
We have a total of 38 results so if we render 20 News on one page then it will take 1.9 pages to render all the NewsItems. But, we want to display two pages.
Thus, To overcome this issue we would use math.ceil() method. This method rounds a number up to the next largest integer.

## Using if-else Statement
Now, we would like to perform the below functions only when the next page exists. Otherwise, we would disable the button, that is no function will be invoked. To do so we would use the if and else statement in our handleNextClick function.

## Creating 'handleNextClick' and 'handlePrevClick' Function
- We would update the page state and content of ComponentDidMount by using these functions.
- That is, We would like to increase the page number by ‘1’ on clicking the Next button and on clicking the previous button we would decrease it by 1. To do so use the following code:

### For the next button:
```javascript
handleNextClick = async () => {
    console.log("Next");
    if (this.state.page + 1 > Math.ceil(this.state.totalResults / 20)) {
    }
    else {
        let url = `https://newsapi.org/v2/top-headlines?country=in&apikey=dbe57b028aeb41e285a226a94865f7a7&page=${this.state.page + 1}&pageSize=20`;
        let data = await fetch(url);
        let parsedData = await data.json()
        console.log(parsedData);
        this.setState({
            page: this.state.page + 1,
            articles: parsedData.articles
        })
    })
}
```
**Explanation**: In the above code we have used the if-else statement to use the function only if the next page exists otherwise it won’t be executed. Now if the function is executed then the state of the page will be updated by 1.

### For the previous button:
```javascript
handlePrevClick = async () => {
    console.log("Previous");
    let url = `https://newsapi.org/v2/top-headlines?country=in&apikey=dbe57b028aeb41e285a226a94865f7a7”&page=${this.state.page - 1}&pageSize=20`;
    let data = await fetch(url);
    let parsedData = await data.json()
    console.log(parsedData);
    this.setState({
        page: this.state.page - 1,
        articles: parsedData.articles
    })
})
```
**Result:** Now, on clicking the Next Button we can move to page ‘2’ where the remaining articles are being rendered.

## Using Props
Now, we would be sending all the required data in the form of props.

## Page Size as variable
- At this moment, the page size is set as 20, which means 20 articles are being rendered on each page of the application.
- Suppose, we would like to render only 5 articles in the NewsMonkey application. But this time we would be setting the page size as a variable.
**To do so follow the below steps:**
1. In app.js:
```jsx
<News pageSize={5}/>
```

2. In News.js:
Accessing the props by using "this.props.pageSize" as shown below:
![[access_props_newsjs.webp]]
Remember to replace "20"  with "this.props.pageSize"

**Result:** Hence, only five news items are being displayed in the NewsMonkey application.
![[newsjs_access_result.webp]]

## Adding Loading Spinner
Copy the downloaded spinner and paste it inside the src of the NewsApp.

### Create Spinner component
We have created a separate file for the spinner named "spinner.js".
![[spinner_intro.webp]]

### Using Spinner component
- Since we would like to show the spinner while loading. Thus, we will change the loading from false to true.
- Now, we want to show the spinner when the loading is true otherwise not. To do so we would add a simple javascript logic in our application as follows:
```jsx
{this.state.loading && <spinner/>}
```
**Explanation:** The above logic means if the state of loading is true then only display the spinner in the application otherwise not.

### Using Spinner while clicking Next and Previous buttons
![[next_prev_spinner_accor.webp]]
**Note:** You can also add the Loading at any instance, like while switching the pages or rendering the application.

**Result** - 
![[spinner_error.webp]]

## Fixing Issue
Thus, To fix this issue we would like to do one more thing to the application, which is erasing the NewsItems when the loading is going on. To do so, we would go to news.js and would edit the code in the following way:
![[spinner_issue_fix.webp]]
**Explanation:** If this.state.loading is true then don’t show any NewsItem otherwise render the news items.

## The NewsMonkey Application
![[newsmonkey_29vi_final.webp]]

## Passing "country" as a Prop

**1. Firstly, You need to pass the country as a prop from App.js as shown below. For the demo, we are passing the country like India:**
```jsx
<News pageSize={5} country= "in" />
```

**2. Secondly, we would be using the created country prop in URL to filter the News as shown below:**
```jsx
let url = `https://newsapi.org/v2/top-headlines?country=${this.props.country}&apiKey=dbe57b028aeb41e285a226a94865f7a7&page=${this.state.page + 1}&pagesize=${this.props.pageSize}`;
```

## Prop types in Class-Based Component
- React has a mechanism for props authentication called prop types.
- As some functions need compulsory arguments, similarly in react components might require a prop to be defined. Otherwise, it won’t render properly.

## Using PropTypes with static variable
Import them into the "News.js" as follows:
```jsx
import PropTypes from 'prop-types'
```

## Static variable
- The static variable can be used to refer to the common property of all objects.
- Static is the property that belongs to the class only.
- Earlier in React, we used to define props outside of the class. But now we will be defining them inside the class by using the static variable.

## Creating Static Variable
![[props_newsjs.webp]]

## Creating Categories
![[newsjs_categories.webp]]
**Result:** We have successfully added all the categories in the Navbar. At this moment all the href links are /about so clicking on any of the categories will still render the same news.

## Passing Categories as Props
passing the category from App.js.

**For the demo, we are passing the category as science in the following manner:**
```jsx
<News pageSize={5} country= "in" category="science" />
```

**Secondly, we have to embed this category in the URL. To do so we have to first add the category in the static default prop and static prop type variable.**
![[newsjs_cate_pass_from_app_to_news.webp]]

**Now, We can easily pass the Category to the URL of ComponentDidMount, handlePrevClick, and handleNextClick function as follows:**
```jsx
let url = `https://newsapi.org/v2/top-headlines?country=${this.props.country}&category=${this.props.category}&apiKey=dbe57b028aeb41e285a226a94865f7a7&page=${this.state.page + 1}&pagesize=${this.props.pageSize}`;
```

**Result:** Here, we have passed the category as ‘science’ and as a result, we are getting all the NewsItems related to Science.
![[newsjs_cate_result.webp]]

## Fetching News category wise in NewsMonkey React App

### Install React Router package
```jsx
npm install react-router-dom
```

### Set Up routing for our application
**Procedure:** After installing the package, The first thing you have to do is go to the root component, that is, your "app.js" file, and import a few things from the react-router package.
```jsx
import {
      BrowserRouter,
      Route,
	  Routes
} from "react-router-dom";
```

### In App.js
1. **Using BrowserRouter:**
	- We have to surround our entire application with the BrowserRouter component and it means that we can use the router in the entire application.
	- Hence, To surround your app with the router component, use 
```jsx
<BrowserRouter></BrowserRouter>
```

2. **Using Routes:**
	- The next step is to decide where we want our page content to go when we go to different pages.
	- Since we want to access the different News items with Update Props. So, we are going to use the Routes component.
	- The Routes component makes sure that only one route shows at any one time. All of our routes go inside this Routes component.
```jsx
<Routes></Routes>
```

3. **Using Route:**
	- Alright, we need to set up our individual routes for the pages of different Categories. So, we will create a route for each page, for which we will be using the route component.
	- At this moment, we have General, Business, Entertainment, Health, Science, Sports, Technology pages of our application, and hence we are going to place the same number of routes inside this switch component.
```jsx
<Route></Route>
```
![[Routes_ex_second_app.png]]
**Result**: We would be displaying the News of a specific Category while the selected path is used as an endpoint in the URL.

**Point to be noted:**
- React won’t render the NewsComponent again while navigating through different categories as it will render the NewsComponent for the first request. But we want to rebound the News component with the Updated Props.
- To fix this issue we would add a unique key prop to every route as shown below:
![[react_routes_news.png]]
**Result**: We would be displaying the News of a specific Category while the selected path is used as an endpoint in the URL.

### In Navbar.js:
- We would like to show the specific news when the user selects the desired category.
- For example, when the user visits the sports category then we want to display the news articles related to sports, to do this we have to refactor the navbar component.
- We would replace the "/about" endpoint with different endpoints related to those specific news categories, as shown below:
![[category_issue_fix.webp]]

## Fixing the Reloading issue
Replace the "a href" keyword with ‘link to’ in "Navbar.js". To do so firstly, Make sure to import the link from react-router-dom.
![[reload_cate_news.webp]]

**Result:** Now, we can switch between the News of different categories without reloading the page. Here’s a look at the NewsMonkey application.
![[reload_fix_result.webp]]

## Adding Published Date and Time of the News
We are adding the Date and Time field in the News Item Card as:
```jsx
<p className="card-text"><small class="text-muted">By {author} on {date}</small></p>
```

**We would be passing values in the author and date variable. With the help of the destructuring method of javascript, we would be getting the author and date from "this.props" as shown below:**
```js
let {title, description, imageUrl, newsUrl, author, date} = this.props;
```

#### In News.js:
- Now, we had to pass the "Author" and "Date" from the "News.js" to the NewsItem component.
- Then only, with the help of destructuring, we would be getting the date and Author information from the props.
![[news_to_newItem_date_author.webp]]

**Result:**  Hence, the published date and author of the article are shown in the NewsItem component.
![[news_to_newItem_date_author_result.webp]]

## Author Field Null Issue
- We have noticed that for some of the NewsItems the author field isn’t being displayed in the NewsItem component.
- To fix this issue we would add a Javascript logic, such that whenever the author field is null then ‘Unknown’ is displayed in the author field of NewsItems.
```jsx
<p className="card-text"><small class="text-muted">By {!author?"Unknown": author} on {date}</small></p>
```

## Formatting Date and Time
Now, we would like to change the format of date and time from the ISO time format to the GMT Date time format.

**ISO time format:** yyyy-MM-dd'T'HH:mm:ss
**GMT time format:** Fri, 27 Aug 2021 07:00:00 GMT

We can simply do so by creating a new Date object and then simply convert it into the GMT string as shown below:
```jsx
<p className="card-text"><small class="text-muted">By {!author?"Unknown": author} on {new Date (date).toGMTString}</small></p>
```

**Result:** Thus, We have successfully formatted the Date and Time and have also fixed the ‘null field of Author’ issue in the application.
![[null_author_fix.webp]]

## Adding Source Badge to NewsItems
We are using the badges from the bootstrap to embed in the News Monkey Application.
```jsx
<h5 className="card-title">{title} <span className="position-absolute top-0 translate-middle badge rounded-pill bg-danger" style={{left: '90%', zIndex: '1'}}> 99+ </span>
```
As a result, the above badge will be embedded in the top right corner of every NewsItem. Now, remember to get the "source" from "this.props" with the destructuring method of Javascript.

**Moreover, we would be passing the Source information of the respective News in the badge as shown below:**
```jsx
<h5 className="card-title">{title} <span className="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger"> {source} </span>
```

**Now, we can simply pass the source in the badge from the News.js as:**
```jsx
source={element.source.name}/>
```

**Result:** Hence, we have **successfully** added a source badge to the NewsItems.
![[source_badge_newsjs_added.png]]

## Creating update Function
- At this time, we are using the same function(updateNews) in componentDidMount, handlePrevClick, and handleNextClick function, just with a slight update in the page number.
- This time, we would create a function that would be used in place of writing this same code again and again. So, let’s create a ‘updateNews’ Function as shown below:
```jsx
async updateNews(pageNo){
    const url = `https://newsapi.org/v2/top-headlines?country=${this.props.country}&category=${this.props.category}&apikey=dbe57b028aeb41e285a226a94865f7a7&page=${this.state.page}&pageSize=${this.props.pageSize}`;
    this.setState({ loading: true });
    let data = await fetch(url);
    let parsedData = await data.json()
    this.setState({
        articles: parsedData.articles,
        totalResults: parsedData.totalResults,
        loading: false
    })
}
```
Here, we are passing the page number in the function as it is different at different places of the function.

## Using the Update News Function

### For componentDidMount
```jsx
async componentDidMount(){
    this.updateNews();
}
```

### For HandlePrevClick
In the handlePrevClick function, we would like to run the update news function by decreasing the state of page number by 1 as shown below:
```jsx
handlePrevClick = async () => {
    this.setState({ page: this.state.page - 1 });
    this.updateNews();
}
```

### For HandleNextClick Function
Similarly, In the handlePrevClick function, we would like to run the update news function by increasing the state of page number by 1 as shown below:
```jsx
handleNextClick = async () => {
    this.setState({ page: this.state.page + 1 });
    this.updateNews();
}
```

**NewsMonkey Application:**
There is no big change in the application but the same task is being performed by a more precise and optimized code.
![[newsMonkey_after_updateNews_func_added.png]]

## Changing the Title Dynamically
![[newsMonkey_title_dynamic_change.png]]
- Here, we have used the category props, which is passed from app.js, and also a function to capitalize the first letter of the Title.
- Now, on selecting a specific category the title also changes accordingly.

## Changing the Heading of Application dynamically
```jsx
<h1 className="text-center" style={{ margin: '35px 0px' }}>NewsMonkey - top {this.capitalizeFirstletter(this.props.category)} Headlines</h1>
```

**Result**: Thus, when the user navigates between the different categories then the ‘heading’ as well as the ‘title’ of the Application changes accordingly as shown below:
![[newsMonkey_title_heading_dynamic_change.png]]

## Removing Previous and Next Button
Firstly, we will remove the Next/Previous button and the function assigned to them, as instead of those buttons we would be using the Infinite scroll to render all the available NewsItems on one page.

### Installing react-infinite-scroll-component
To start using the Infinite scroll, we have to install the react-infinite-scroll-package npm package by using the below command:
```javascript
npm i react-infinite-scroll-component
```

## In News.js:

### 1. Adding Infinite Scroll
Firstly, make sure to import Infinite scroll and then add the infinite scroll in News Component as shown below:
![[infinite_scroll_logic.webp]]
**Explanation:**
- Above, we have set the data length equal to the article length.
- We would be creating a "fetchMoreData" function later on.
- After that, to check if more articles are available for rendering in the NewsComponent we have used "hasMore".
- Inside the constructor, remember to set the total results equal to 0. Finally, we have added the spinner component in the Loader.

### 2. Creating fetchMoreData Function
We have to write a function to render more NewsItem. Here’s the code of the fetchMoreData function:
```js
fetchMoreData = async () => {
    this.setState({ page: this.state.page + 1 })
    const url = `https://newsapi.org/v2/top-headlines?country=${this.props.country}&category=${this.props.category}&apikey=dbe57b028aeb41e285a226a94865f7a7&page=${this.state.page}&pageSize=${this.props.pageSize}`;
    let data = await fetch(url);
    let parsedData = await data.json()
    this.setState({
        articles: this.state.articles.concat(parsedData.articles),
        totalResults: parsedData.totalResults,
        loading: false,
    })
};
```

**Explaination** - 
 In the fetchMoreData function, we have set the state of the page number and have fetched the previously used Data. After that, We have concatenated the "parsedData.articles" in articles.

**Result**: Hence, we have successfully added an Infinite Scroll bar to the application.
![[infine_scroll_result.webp]]

## Installing React loading bar package
```js
npm i react-top-loading-bar
```

**It is a very easy-to-use package. This package can be used in two ways:**
1. With the help of 'ref'
2. With the help of 'state'

Here, we would be using the second method to add a loading bar to our application.

## Using React Loading bar
Firstly, Make sure to import the Loading bar in "App.js". After that, add the loading bar in "App.js" as shown below:
![[loading_bar_newsjs.webp]]
**Explanation**:
- Above, we have added our desired color, which is red, to the loading bar.
- We would create a state object having progress. Remember, the initial progress in the state is 0. We are using the state progress in the progress variable of the loader.
- After that, we have created a 'set progress' method to change the 'progress' of the created state.
- In the end,  we passed the ‘set progress method to the NewsComponent. This will allow us to set progress from the NewsComponent.
- We have also set the height of the progress bar as 3 to have a clear visible look of the loader in the application.

#### In News.js:
- As a result of the above steps, we have a function in the NewsComponent that will allow us to change the state of the loading bar.
- So, now we would be using the loading bar at certain instances with different values. This will provide a smooth-moving effect to the loading bar.
![[setProgress_newsjs_changes.webp]]

## Fixing issue - Source Badge Not responsive
We have noticed that the 'source News Badge' isn’t displayed  properly in the Mobile Devices as shown below:
![[source_badge_newsjs_issue.webp]]

To fix this issue we would be adding the Source badge inside a div container and setting the display, justifyContent, position, and right CSS properties as flex, flex-end, absolute, and 0 respectively.
![[source_badge_newsjs_issue_fix.webp]]

**Result:** Here’s the look of our application on android and PC devices.
![[NewsMonkey_look_after_source_badge_fix.webp]]

## API Exhausted issue
we would be hiding the API key with the help of the environment variable.

### Hiding the API key
- Firstly, we will define the environment variable in the ".env" file.
- Remember that, by default, the ".env.local" file is included in the ".gitignore". After that, we would be fetching the API key from the ".env" file in an API key variable.
- In the end, we would be passing the apiKey variable as a prop in the news update and FetchMoreData function of NewsComponent.

#### 1. Defining Environment variable
- Firstly, create a ".env.local" file, and let’s define an environment variable inside it.
- Remember, whenever you start any environment variable, It must be prefixed with REACT_APP_ then only you get access to that variable in your React Application.
```jsx
REACT_APP_NEWS_API= "dslkhpdsoiher32sdgsoihg3oisdf"
```
**Note:** We would be adding our original API key in place of the fake code and obviously we would not like to make it public.

#### 2. Fetching the API key
- Now, we have to fetch this API key as an object in "app.js". To do so we would simply add the below code in our "app.js".
- Remember that, You can access your environment variable by using "process.env.prefix".
```jsx
apiKey = process.env.REACT_APP_NEWS_API
```

#### 3. Passing the API key as Prop in NewsComponent
Now, to use the API key we have to first pass the "apiKey" variable in the NewsComponent as shown below:
![[apikey_pass_to_news.webp]]

#### 4. Using the API key
Earlier, we used the API key in the 'updateNews' and 'FetchMoreData' function. But this time, we would be using the API key as a prop as shown below:
```jsx
const url  = `https://newsapi.org/v2/top-headlines?country= ${this.props.country}&category=${this.props.category}&apiKey=${this.props.apiKey}&page=${this.state.page}&pageSize=${this.props.pageSize}`;
```

**Result:** Hence, we have **successfully** hidden the API key of the News Monkey application. Here’s the look at our application:
![[newsMonkey_after_apikey_hide.webp]]

## Changing Class based NewsMonkey components to Functional based
We have a total of five components which are Navbar, Spinner, "App.js", "News.js", "NewsItem.js". So let’s begin changing these class-based components to the functional component:

### Changing Navbar.js:
Firstly, we will remove the render function and returning the component in an arrow function as shown below:

![[class_based_compo_to_func_compo_navbarjs.webp]]

### Changing Spinner.js:
firstly remove the render function and after that return the spinner in an arrow function as shown below:

![[newsMonkey_newsItem_fix.webp]]

### Changing News.js
- We will first begin changing the ‘proptypes’ and ‘default Props’ to the function-based component.
- If you remember, we can use the prop types in the functional component as shown below:
```js
News.defaultProps = {
    country: 'in',
    pageSize: 8,
    category: 'general',
}
News.propTypes = {
    country: PropTypes.string,
    pageSize: Proptypes.number,
    category: PropTypes.string,
}
```

- Moreover, we will change the Export class component in an arrow function.
- After that, we will be using the ‘usestate’ hook in News.js to update the state and to set an initial value of the state. To do so firstly, Import the ‘useState’ hook in News.js. As a result, we can now utilize the ‘use state’ hook inside the function as shown below:
```js
const News = (props) => {
    const [articles, setarticles] = useState([])
    const [loading, setloading] = useState(true)
    const [page, setPage] = useState(1)
    const [totalresults, setTotalResults] = useState(0)
```
**Explanation:**
- Since we have set the state with the help of the 'useState' hook, therefore we can remove the constructor from the News.js as it is not required anymore.
- Now, we can define a state by using the above state functions, and hence we will remove 'this' keyword, before declaring any state or variable.
-  Make sure to define updateNews, fetch more and other functions by converting them into an arrow function.

![[newsjs_state_hook_and_this_fix.webp]]

#### Changing componentDidMount
To perform the task of  componentDidMount, we will be using the useEffect function as shown below:
```js
useEffect(() => {
    updateNews();
}, [])
```

**Result:** Hence, we have successfully refactored the application from a class-based component to a function-based component. Here’s a look at the NewsMonkey application.
![[result_after_class_based_to_func_based.webp]]

## Sticky Navbar
To make the Navbar sticky, we can simply add the "fixed-top" class in "Navbar.js" as shown below:
![[sticky_navbar.webp]]

## Fixing Bugs

#### Issue:
 Whenever we are fetching the new News by running the fetch more Data function, then the "setPage" is taking some time to set the page value, which means taking extra time in rendering the page while scrolling. This issue occurs as the "setPage" is an asynchronous function.

#### Solution:
 To solve this issue we would add "page+", that is set page by incrementing the value, in the url. This is so because the url is being fetched before the set page.
![[setPage_issue_sol.webp]]

## Changing App.js to Functional Component
![[appjs_functional_to_class_comp.webp]]
**Explanation:**
   - Firstly, we will render the app in an arrow function instead of the class. After that, we would use the 'useState' hook to set the progress and the initial state of progress.
   - Finally, remove the render function from the "App.js" and also remove the 'this' keyword from the application.

**Result**: Hence, we have **successfully** created the NewsMonkey application here is a look at the NewsMonkey application:
![[newsMonkey_after_bug_fix.webp]]
