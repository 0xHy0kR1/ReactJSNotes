## Create React App - iNotebook
To create a react app, firstly open Windows PowerShell and execute the create react app command:
```jsx
npx create-react-app iNotebook
```

#### iNotebook information:
  - This is the name of our new React application. It is the notebook on the cloud, that is it can be used to store any notes or important points on the cloud.
  -  This time we will be storing the data on the server. We will be creating a login Page to grant access to the notes for its right user only. Hence, we have **successfully** created the iNotebook React app.

#### Creating backend for iNotebook
   - We would be putting all the files related to the backend, in a separate backend folder to have a better understanding.
   - Open the backend folder with the source code editor. After that, open the terminal and execute the 'npm init' command and then fill up some basic details like name, description, entry point, etc to create a package.

Now, we can install the required framework inside the package.

## Installing Express and Mongoose

#### Express:
   - Express.js is a back-end web application framework for "Node.js".
   - To install express, simply execute the below command in the terminal:
```js
npm i express 
```

#### Mongoose:
   - Mongoose is an extraction layer on top of MongoDB, which would help us to connect with the Node Js.
   - It requires a connection to a MongoDB database. It provides a straightforward, schema-based solution to model the application data.
   - To install Mongoose, execute the below command in the terminal:
```js
npm i mongoose
```

**Note:** --> Make sure to create an "Index.js" file, which would be the entry point of our application.

## ThunderClient
   - It helps in testing the APIs. For example, Below we have sent a request in the [https://www.thunderclient.io/welcome](https://www.thunderclient.io/welcome) API and have got a response from the API. Now, we can use this response in the application.
   - To use it, We can simply install the thunderclient extension in vscode.
![[reactjs_thunderclient_ex.webp]]

## Working with Backend

### Installing Nodemon
- Nodemon allows us to develop node.js-based apps, by automatically restarting the node application when file changes are detected in the directory.
- You can install the nodemon package in the application as a dev dependency by using the below command:
```jsx
npm i -D nodemon 
```

### MongoDB compass
MongoDB compass provides a Graphical user interface(GUI) to a client, which helps in interacting with the MongoDB database management system.

### Features of MongoDB compass
  - It visualizes and inspects the data, which is stored in your database
  - It creates databases and allows you to insert, update, and delete data in your database
  - It provides real-time server statistics.
  - It provides a great way of Managing your indexes

### Connecting to a Database
Mongoose requires a connection to the MongoDB database.

![[database_connect1.png]]

![[database_connect2.png]]
- You can copy the connection string and paste it in Mongoose to build the connection between Node.js and MongoDB.

- The next step will teach you about how you can connect MongoDB and Node.js with the help of the above database URL.

### Connect MongoDB with Node.js using Mongoose
![[nodejs_connect_to_mongodb_using_mongoose.webp]]

**To connect MongoDB with Node.js, you have to configure the code as shown below-**
```js
const mongoose = require('mongoose'); //Importing mongoose

const mongoURI = "mongodb+srv://R3g0s666:thm.local666.me@cluster0.ebgrjft.mongodb.net/"


const connectToMongo = async ()=>{

    try {

        await mongoose.connect(mongoURI, { useNewUrlParser: true, useUnifiedTopology: true });

        console.log('Connected Successfully');

    } catch (error) {

        console.error(error);

    }

}


module.exports = connectToMongo; //Here, we export this function
```

**Explanation:** 
- Here, we have firstly created a db.js file in the root folder of the application. After that, we have required mongoose in the application.
- In the second line of code, we have set the mongoURI equal to the Connection String, which we have copied earlier.
- In the end, we have created a ‘connectToMongo’ function and have used the mongoose.connect function inside it and have exported the connection successfully.
- Remember, we have used the common js modules instead of ES6 modules.

### Use Node.js MongoDB Connection Script - Index.js
We would like to use the db.js file in routes/index.js, therefore we would include it  by adding the below code in Index.js:
```js
const connectToMongo = require('./db');
connectToMongo();
```

**Express Server Setup**
Moreover, we would like to make the index.js an express server of the application. To do so simply copy the below code in the application:

**In Index.js**
```js
const connectToMongo = require('./db');
const express = require('express')
connectToMongo();
const app = express()
const port = 3000
app.get('/', (req, res) => {
    res.send('Hello harry')
})
app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`)
})
```
**Result:** After doing this, we are successfully connected to MongoDB.

### Testing the API
we would be using Thunder Client in this course for testing the APIs.

**So, let’s enter the URL in Thunder Client and check for the response of the endpoint. Thunderclient will respond to the request as shown below.**
![[api_testing_backend_done.png]]
Here, we are getting ‘hello World!’ as a response, which proves that our endpoint is working perfectly.

Hence, we have **successfully** created a .get endpoint that is returning Hello World!.

## Creating Routes
We can create all our routes in "Index.js". we can add three routes such as Login, Sign up, Home route as shown below:
![[inotebook_routes.webp]]
But, this method will lead to the distortion of the file structure of our React Application. As a result, maintaining a large React app will be a nightmare for you. Therefore, we won’t recommend you to use this method for large applications.

## Creating Mongoose Models
   - We are creating a Models folder to store the Mongoose Models.
   - A Mongoose model is a wrapper on the Mongoose schema.
   - A Mongoose schema defines the structure of the document, default values, validators, etc., whereas a Mongoose model provides an interface to the database for creating, querying, updating, deleting records, etc.

## Getting Started
We have already connected the Mongoose with the database. Thus, we would simply create a model. For example - "Notes.js" and "User.js".

##### In User.js:
The "user.js" model will contain info about the user. Now, we would be creating a schema for the user in the following manner.
```jsx
const mongoose = require('mongoose');
const UserSchema = new Schema({
    name: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true,
        unique: true
    },
    password: {
        type: String,
        required: true
    },
    date: {
        type: Date,
        default: Date.now
    },
});
module.exports = mongoose.model('user', UserSchema);
```

**Explanation:**
   - Above, we have added some of the common fields, such as Name, Email, Password, Date, etc in the schema.
   - We have also added the data types for the given fields and have made some of the fields compulsory to be entered by the user.
   - In the end, we have exported the schema. Hence, we can use the above schema in the routes.

##### In Notes.js
Notes.js model will be containing all the Notes of the iNotebook application. Therefore, let’s build a NotesSchema for it in the following manner.
```jsx
const mongoose = require('mongoose');
const NotesSchema = new Schema({
    title: {
        type: String,
        required: true
    },
    description: {
        type: String,
        required: true,
    },
    tag: {
        type: String,
        default: "General"
    },
    date: {
        type: Date,
        default: Date.now
    },
});
module.exports = mongoose.model('notes', NotesSchema);
```

**Explaination** - 
   - Above, we have added some of the common fields, such as Title, Description, Tag, etc in the schema.
   - We have also added the data types for the given fields and have made some of the fields compulsory to be entered by the user and have provided some of the fields with a default value.
   - In the end, we have exported the schema. Hence, we can use the above schema in the routes as well.

## Creating Routes
We are creating a Routes folder to store all the routes of the iNotebook application. After that, We would be linking the routes with the help of app.use as shown below
![[inotebook_routes_declaration.webp]]
We have added the "auth" and "Notes" routes. Thus, we are going to create two files named "auth.js" and "notes.js".

##### In auth.js
We would be using the router inside the "auth.js" file. Here’s how we are going to do that:
![[inotebook_auth.webp]]
**Explanation:**
   - Above, we have imported the express router in auth file.
   - After that we have used the router.get to specify the endpoint for a particular route.
   - Here, we have passed the JSON to the router to display for a specific endpoint of the appplication.In the end, we have exported the router.

**Result:** Hence, the JSON is rendered in the application for a specific routes as shown below:
![[inotebook_routes_result.webp]]

## Middleware
   - They are the functions that have access to the request and response object in the request-response cycle.
   - They are used to alter res and req objects for some specific tasks.
   - We have to use the middleware before using the req.body command.

let’s add the middleware in "Index.js" by writing the below code:
```js
app.use(express.json())
```

##### res.send():
   - It is used to Send a string response in a different format like XML, plaintext, etc.
   - For example, we can send Hello, plain text, using res.send to /api/auth endpoint.
   ![[res_send_ex.webp]]


##### req.body:
   - It holds parameters that are sent up by the client as a part of the Post request.
   - By default, its value is set to be undefined and hence it is populated with the help of middleware.
   - For now, we are extracting the req.body values in the terminal by using the console.log() command. At this moment it is undefined as shown below:
   ![[req_body_ex.webp]]


##### In auth.js:
Now, we would be learning how to send data to the request body. In our case, we would be sending data of a specific user in the request body.

## Creating User
   We are entering some random data of users in the request body as shown below:
   ![[random_data_user_create.webp]]
   
   **Result:** - Hence, we have gotten the following details printed on the console. This means that we are able to read the req.body properly as well as we are able to send 'hello' as a response by using res.send.
   ![[random_data_user_create_result.webp]]

**Now, if we send the req.body as a response by using the res.send then we would be able to get the data as a response as shown below:**
![[random_data_as_response.webp]]
## Saving the Data in Database
   - Firstly, Import the user from the model folder in your auth.js. After that, create a user and use the save function as shown below.
   - The save() function is used to save the document data into the database.
   - Remember, To import schema in your User.js model before performing the above step.
![[authjs_data_save_to_database.webp]]

**Result:** Now, our user would be saved in our MongoDB Database with a different ID as shown below:
![[preview_of_data_save.webp]]

## Adding Data Validation Using express-validator

### Installing express-validator
```python
npm install --save express-validator
```

### Using express-validator
Firstly, we have to import express validator in our auth.js file by writing the below piece of code:
```js
const { body, validationResult } = require('express-validator');
```

### Adding Validation Checks
![[validating_creds.png]]

### Error page
Now, If an error occurs in the value then we would like to inform the user about his/her mistake by showing an error page. 
```js
router.post('/', [
    body('name').isLength({ min: 3 }),
    body('email').isEmail(),
    body('password').isLength({ min: 5 }),
], (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }
    res.send(req.body);
})
module.exports = router
```
**Explanation:** In the above code, we have set that if error.empty didn’t return a true value, then show a 400 bad request error and send the specific errors details.

### Checking if Validation is Working
For demo purposes, we are sending some invalid values like the ‘Empty name’ field value. Here’s the result after entering the invalid data:
![[creds_validate_check.png]]

### Adding a Custom Message
At this moment, an 'Invalid' message is shown to the user if the entered data didn’t meet the predefined conditions. However, we can add a custom message so that the user can know his/her mistake and can fix it.

**You can add the custom message as shown below:**
![[inotebook_custom_message.png]]
**Explanation:**
   - Above, we have added a custom message for Name, Email, Password as 'Enter a valid Name', 'Enter a valid Email' and  'Password must be at least 5 characters respectively.
   - Now, if any invalid data is entered in these fields then the custom message error will be shown to the user.

**Result:** Hence, we have successfully added the validation layer for the desired fields of the Application.

### Creating User
Now, we would be creating the user of the Mongoose model by writing the below piece of code instead of the save function, which we have used earlier to store data into the Database.
```js
User.create({
    name: req.body.name,
    email: req.body.email,
    password: req.body.password,
}).then(user => res.json(user));
```

### Saving the Data into the Database
Now, let’s try to add the data of a legit user in our Database by adding genuine values in the Name, Email, Password fields as shown below.
![[inotebook_test_user.png]]

**Result:** Thus, the data is being saved in the MongoDB database as shown below:
![[inotebook_mongoDB_datasave.png]]

### Two Entries with One email - issue Fixation
There’s one more issue with our validation, that is if the user submits the request two times with the same ‘Name’ and ‘Email’ then the two different entries of Data are stored in the database. This means that we are not getting the unique email for each submitted data.

**Solution:**
   - To resolve this issue, we would firstly open the db.js and would specify a database, suppose iNotebook.
   - In our user.js we would create a user variable and user indexes as shown below:
```js
const User = mongoose.model('user', UserSchema);
User.createIndexes();
module.exports = User
```

**Result:**
Now, the data of a specific user is stored in an iNotebook folder. After submitting the data once, we are unable to add the data of the user with the same email id as shown below:
![[inotebook_same_creds_issue_fix.png]]

### Response - While entering a registered ID
Here, we are noticing that whenever someone tries to register with the same email id then no response is shown to the user. Now, to make it more appealing we can show a custom message to the user by sending a response JSON as shown below:
![[inotebook_entering_register_email.png]]

**Result:** Here’s the result of applying the above set of code. Now, In our database, every user has a unique email id.
![[inotebook_entering_register_email_issue_fix.png]]

## Creating ThunderClient Collections to Manage Requests

### Refactoring the Code
   - Earlier, we were providing the same response to the client for any kind of error. But, now we would like to show the particular error to the user to provide him/her a better understanding of the issue.

**To do this, we can simply use the catch error method, as show below** - 
```js
catch (error) {
    console.error(error.message);
    res.status(500).send("Some Error occurred");
}
```

### Adding Comments  and Validation
   - Now, we would add some comments in our 'auth.js' to make the code more understandable.

**Here, we are using the async and await function with some more lines of codes for validation of the unique email id as shown below:**

![[inotebook_authjs_add_comments_custom_error.webp]]

**Explanation**:
   - Above, We have used the 'findone' method on the model, to search and list the user with the email as 'req.body.email', that is the user with this ID already exists in the database.
   - "findone()" method is used to return a single document that satisfies the specified query criteria. Moreover, we have set that if the user with the email ID already exists then return a '400 bad request' with a custom message.

### Thunderclient Collections
   - It is a collection of endpoints that are connected with the application. We can easily manage all the endpoints with the help of thunderclient collections.

### Getting Started
   - We would create an iNotebook collection in the Thunderclient.
   - You can do so by opening the collection option in thunderclient and then selecting the drop-down menu and adding a 'NewCollection'.

##### In iNotebook collection:
   - We would create a new folder named 'authentication' inside the iNotebook collection.
   - Inside the authentication folder, we would be creating a new request named 'create a new user'.
   - Moreover, We would post a request at the '/api/auth/createUser' endpoint and would again simply add a request body for validation.

![[thunderclient_collection_intro.webp]]

**Result**: Since the user with this email existed we are thrown with the error. However, if the user enters with the unique email id then the data is added to our iNotebook database, as we have already seen.

**refer** --> [[Understanding_Password_Hashing,Salt_&_Pepper]] to learn about hashing

## Hashing Passwords using bcryptjs in NodeJs

#### Installing bcryptjs package
   Bcryptjs is a nodejs package that will help us in implementing password Hashing, salt and pepper in Nodejs easily.

   **To install bcryptjs you can use the below command -**
   ```jsx
 npm i bcryptjs  
   ```

### Using bcryptjs
   Bcrypt works in two regular steps. In the first step, we will generate the salt and secondly, we will hash the password with the generated salt.

1. **Generating Salt**
   To generate the salt you can simply use the below command:
```jsx
   const salt = await bcrypt.genSalt(10);
```

**Explanation:** 
- Here, we have used the ‘await’ keyword before a function to make the function wait for this promise to be resolved.
- Here, we have used the default value of the salt round, which is 10. In our case, we have generated the salt and will perform the hash in the separate function call. However, You can salt and hash the password in one function.

2. **Hash a Password**
   First of all import bcryptjs in authjs by entering the below command:
```jsx
const bcrypt = require('bcryptjs');   
```

we are declaring a new variable name secure password which we will be using in the password field of the create user function. Here we have passed two parameters, Password and Salt, to the bcrypt.hash as shown below:

![[inotebook_hashed_pass.webp]]

**Result:**
Now, let’s open the thunder client collection and post a request to check out the result as shown below. As you can see, this time the password returned as a response is a Hash.

![[inotebook_pass_hashed_ex.webp]]

## Adding Login Authentication
   - Till now, whenever someone was logged in to the database, we were showing him/her their details as a response. It is obvious that we will be returning something else to the client. In our case, we will be returning a token, way of authentication, to the client as a response.
   - There are many types of authentication techniques available on the web, but in this course, we will use JWT authentication.

### JWT (JSON web token)
   - JWT is a JSON web token npm package, which helps in verifying a user.
   - JWT helps in facilitating secure communication between the server and the client.
   - JSON web token consists of three parts- Header, Payload, and Signature.

**Header:**
   - The information contained in the header describes the algorithm and the token type used to generate the signature.

**Payload:**
   - It contains the data you want to send, this data is used to provide authentication to the party receiving the token.

**Signature:**
   - Whenever we dispatch a JSON web token from the server, we will sign the token with secrets.

**Here’s how we can create a JWT secret:**
```js
const JWT_SECRET = 'Harryisagoodboy';
```

### Using JSON Web Token(JWT)
   First of all, we will import the JSON web token by entering the below command in the Auth.js file:
```js
var jwt = require('jsonwebtoken');
```

Now, we will send a token having a user-id instead of a User as a response. After that we will use the sign method as shown below:

![[inotebook_jwt_token_ex.webp]]

**Explanation:**
   - Above, we have created a data object containing a user-id. After that, we have created the ‘authtoken’ function in which we have used the jwt.sign method.
   - Jwt.sign method takes two parameters and returns the promise.
   - Remember, the jwt.sign is a sync function thus, there is no need of using async-await.
   - Finally, we have returned the ‘authtoken’ as a response by using the res.json command.

**Result:**
Now let’s check the response by sending a request as shown below.

![[inotebook_authtoken_test.webp]]

   - Here, we are getting the token in response to the request.
   - Now, whenever someone returns the auth token then we can easily convert it into data, and with the help of JWT secret we can easily find out if someone has tampered with the data or not.

## Creating Login Endpoint & sending auth token

### Authenticate a User
   Till now, we have created a signup user endpoint in "auth.js". In a similar fashion, we are going to create a login endpoint to authenticate the user as shown below:
   
   ![[inotebook_login_endpoint.webp]]

**Explaination** - 
Above, We have added a validation check for the Email and the password. If the client enters an invalid email or left the password field blank then the app will throw the occurring error with a bad request.  This simply means we won’t bother the server to fetch data from the database if an error occurs.

### Comparing Email
   We would use the destructuring method of javascript to get email and password from the req.body and would use the try-catch syntax as shown below:

![[inotebook_email_compare.webp]]

**Explanation:**
   - In try, we would like to fetch ‘User’ having the entered email-id and password of the client.
   - If we don’t find any existing user in the database with the given email, then we would throw an error with a custom message to the client.

### Comparing Password
   After comparing the client email we would compare the entered password of the client with the user actual password as shown below:
   
   ![[inotebook_pass_compare.webp]]

**Explanation:** 
   - Remember to use the await in bcrypt.compare as it is an asynchronous function.
   - Similarly, As we have done for email, if the password doesn’t match up then we would show an error message to the client.
   - However, if both the fields(Email and Password) are correct then we would send the payload to the user.
   - In catch, we would simply send an error to the user with a custom message, as we have done earlier.

**Result:** We would post a request, with correct credentials, at the /api/auth/login endpoint as shown below:
![[inotebook_login_endpoint_test.webp]]
Here, we are getting the auth token while entering the correct credentials. However, if we have entered the wrong email id and password then the application will throw an error.

## Creating a middleware to decode user from a JWT

### Creating 'Get user' Route
   - We would be creating a new route to get the details of the logged-in User using Post requests.  Remember, that to use this route, a login is required.
   - This simply means that we need to send the JWT token to this route.
![[inotebook_get_user_route_overview.webp]]

**Explanation:**
   - Here, we have used the try-catch syntax to allow us to define a block of code to be tested for errors while it is being executed.
   - In try, we would wait for the user ID to be fetched, which will be coming from the token.
   - Here, just for demo purposes, we have assumed that we get the user id (todo).
   - After that, we are finding the user by its received user-id from the token.
   - Subsequently, we would be showing all the details of the user by using the select method, except the password.

### Decode User ID from JWT
   - Now, we will be decoding the authtoken to get the user id and then we will pass the user id to our third route.
   - Remember, that we have sent the user id in the authtoken, in the previous article.

### Getting Started
   - We will send a header having auth-token to all the request which requires the user to be authenticated.
   - After that, we would extract the data from the header and would fetch it in the third route.
   - However, if we write the extraction code of the User ID in our third route, then we have to copy-paste it to every endpoint which requires user authentication. To overcome this issue we are going to use middleware.

#### Middleware in Nodejs
   In our case, middleware is a function that will be called whenever a request will be made in the 'login required' routes.

#### Creating Middleware
   - We are creating a middleware folder, inside which we are creating a "fetchuser.js" middleware.
   - In "fetchuser.js" middleware, we would write a function as shown below:
   
![[inotebook_fetchuser_overview.webp]]
**Explaination:**
   **Step 1:** 
		   Above, we have first imported the Jsonwebtoken (JWT). After that, we have created a fetch user arrow function, which takes request, response, and next.
		   
   **Step 2:** 
			After that, we would like to get the token from the header named auth-token. Moreover, if the token is not present then we have denied access to the user with a bad request.

   **Step 3:** 
	   - Subsequently, we have extracted the data from the token and have verified the token and the JWT_secret. Hence, we would get the user and therefore we would execute the next function.
	   - The next() function is not a part of the Node.js or Express API but is the third argument that is passed to the middleware function. This means that the async (req, res) will be called after getting the user in the ‘getuser’ route.

#### Enhancing the third Route
   This time, we have the user id appended in the request therefore we have used req.user.id to get the user-Id. Finally, we have sent the user details as a response as shown below:
   
![[inotebook_third_route_setup_done.webp]]

#### In Thunderclient:
   In the get user endpoint, we would append the authtoken in the header and will make a post request at the ‘get user’ endpoint as shown below:
![[inotebook_third_route_endpoint_test.webp]]
Hence, we have successfully fetched all the details and now these details can easily be taken to the frontend.

## Fetching all notes & Adding a Note

### Creating a new Route - Fetch All Notes
   - Now, we will be creating a new 'fetchallNotes' route, which will provide the client with all the notes of him/her, by fetching them from the database. Remember, it will be providing the notes to only those clients who are logged in.
   - We would be using get requests as we have to simply take the token from the header.
![[inotebook_fetchallnotes_route.webp]]

**Explanation:**
   - Above, we have used the find() method to get all the notes of the specific user.
   - Notice that we have used the async and await function while creating the fetch all notes route.
   - After getting the notes, we will be sending them as a response.

### Testing the Endpoint - Thunder Client
![[inotebook_fetchallnotes_test.webp]]

**Result:** 
You must have noticed that here we are getting the empty array as a response. This happens as no notes are available at this instance. However, if notes were available then all the notes would have been shown as a response.

### Associating the Notes with User
   - We would like to show the notes, stored in the database of the iNotebook application, of the client to him/her only to maintain and protect the privacy of the user. To add this functionality in the application, we have to somehow associate the Notes with the user.
![[inotebook_notes_schema_setup.webp]]

**Explanation:**
   - Above, in the Notes model, we have first imported the schema in the Notes model.
   - After that, we have created a user field in the NotesSchema.
   - Inside the User field, we have used the schema type to specify what a given path should have and what values are valid for that path. If you have ever used SQL then you can compare it with the foreign key.
   - In the second line of code, we have added the user model as a reference model. As a result, now we can store users in the Notes.

### Creating a New Route - Add Note
   - Earlier, we have got an empty array as a response on the 'fetchallNotes' endpoint. This had happened as no notes were available for display. Therefore, we will create a new route to add new notes
   
![[inotebook_addnote_route.webp]]

**Explanation:**
   - Here, we are creating an Add Note Route. Moreover, we are also using the express validator to check the notes, as we have done previously.
   - Once the notes are successfully validated without showing any error then we would like to save the new note.

### Saving a New Note

![[inotebook_note_save_to_database.webp]]

**Explanation:** To save the new notes in the database follow the below-mentioned steps:

1. **Step 1:** Firstly, we would get the title, description and tag from the req.body with the help of the destructing method of javascript.
2. **Step 2:** After that, we have added the title, description, tag and the specific user in the New Note object. 
3. **Step 3:** Finally, we have used the save() function to save the notes in the database and have returned the notes as a response to the client. If you remember, we have already learnt how to save a note in the database.

### Checking Results - Saving notes
   Now, let’s check the add note endpoint in thunder client by making a Post request and adding a random note as shown below:
   
![[inotebook_addnote_test.webp]]

**Result:**
   - Here, we have passed some random values to the title, description, and tag field. As a result, we have got the user detail as a response and all the notes data is being added in the database corresponding to that specific user.
   - Remember, the user must be logged in to access this endpoint.

### In thunder client- Fetching Notes
   Now, let’s check the fetch all Notes endpoint in thunder client by making a get request to fetch all the notes of a specific user as shown below:

![[inotebook_fetchallnotes_test.webp]]

Here, as a result, all the notes of the specific user have been successfully fetched.

## Updating an existing Note

### Creating Route - Updating Note
   - We will be creating a new endpoint that will help us to update an existing note in the database.
   - Remember, that we will make sure that the user is logged in for accessing the update Note endpoint.
   - To create a new route follow the below steps:
     ![[inotebook_updatenote_route.webp]]
     
**Explanation:**
   - We have to provide the id of the note, which we would like to update.
   - Firstly, we have used the destructuring method of Javascript to get the title, description, and tag from the body
   - After that, we have created a new note object, in which we have added the functionality to set the updated title, description, and tag field in place of the existing fields of the note.
   - Here, we have used the put request to create a new resource or update an existing one.

### Error - Note doesn't exist
   Firstly, we will allow the server to find the notes which are requested by the client as shown below:
   ![[inotebook_updatenote_note_finding_with_function.webp]]
   
**Explanation:**
   - Here, we have used the findById() method to get the notes by their ID.
   - However, if the server fails to find the notes that means the notes did not exist in the database. In that condition, we will be showing a not found error to the user.

### Validating the User
   Now, we will be adding a validation check so that a logged-in user can only update his/her notes and don’t tamper with the notes of another user.
   ![[inotebook_updatenote_user_check_for_note_update.webp]]

**Explanation:**
   Here, we are validating if the note belongs to the logged-in client or not. To do so we have extracted the user-id and have evaluated it with comparison to the logged-in user-id, to check if it is the same user who has created the note or not. However, if the match of user-id fails then we will unauthorize the logged-in user from accessing the notes of others.

### Find and Update Note
   However, If both the above-mentioned conditions are satisfied, that is the note exists in the database and the user id correctly matches with the logged-in user id. In that circumstances, we will find and update the note by using the findByIdAndUpdate() method as shown below:
   
   ![[inotebook_final_function_for_note_update.webp]]

### Testing the Update Note Endpoint
   Now, let’s check the update Note endpoint in thunderclient by making a put request to update a note as shown below:
   
   ![[inotebook_updatenote_testing.webp]]
   
   **Result**:
   Here, as you can clearly see, our notes have been successfully updated. You can also make a get request to fetch all notes endpoint to make sure if the notes are updated in the database or not.

## Endpoint for deleting a Note

### Creating Route - Delete Note
   - We will create the delete Note endpoint in a similar way, as we have created the update Note endpoint.
   - Remember, here we will be using the ‘delete’ request method in place of ‘put’ request as shown below:
     ![[inotebook_deletenote_route_overview.webp]]
     
### Find the Note
   Firstly, we will allow the server to find the notes which are requested by the client as shown below:
   ![[inotebook_deletenote_route_getting_notes.webp]]
   **Explanation:**
   - Here, we have used the findById() method to get the notes to delete by their ID.
   - However, if the server fails to find the notes that means the notes did not exist in the database. In that case, we will be showing a not found error to the user.

### Validating the User
   Now, we will allow the user to delete the note only if the user owns the note otherwise not. Here’s how we can do that:
   ![[inotebook_validating_user_for_note.webp]]

**Explanation:**
   - Here, we are validating if the note belongs to the logged-in client or not.
   - To do so we have extracted the user id and have evaluated it with comparison to the logged-in user-id, to check if it is the same user who has created the note or not.
   - However, if the match of user-id fails, then we won’t authorize the logged-in user to access the notes of others.

### Find and Delete Note
   However, If both the above-mentioned conditions are satisfied, that is the note exists in the database and the user-id correctly matches with the logged-in user id. In that circumstances, we will find the note by its id and delete the note by using the findByIdAndDelete() method as shown below:
   ![[inotebook_delete_note_with_func_msg_sent.webp]]
   
### Testing the Delete Note Endpoint
   Now, let’s check the delete Note endpoint in thunderclient by making a delete request to delete a note as shown below:
   ![[inotebook_deletenote_endp_test.webp]]
   **Result:** Here, as you can clearly see, our notes have been successfully deleted. Now, if the client tries to delete the same note twice they will face an error, as the note has been already deleted.

## iNotebook React Project Setup
   we finally finished setting up the backend of the iNotebook application. From now on, let begin setting up the frontend and connect it with the created backend of the iNotebook application.

### Getting Started with Frontend
   Firstly, we will completely set up the front end of the iNotebook app and later we will connect frontend with backend

#### Installing npm packages

1. **React router**:
	- It provides a way to introduce different pages or routes in our React application without reloading the page.
	- To install react-router, use the below command:
```js
npm i react-router-dom
```

2. **Concurrently**:
	- Concurrently is an npm package that allows us to use more than one server concurrently.
	- To install concurrently, use the below command:
```js
npm i react-router-dom concurrently
```

#### In package.json - React App
   We want to start our backend and the react app simultaneously with the help of concurrently. Therefore, we will add the below piece of code in the script of package.json
```js
"both": "concurrently \"npm run start\"  \"nodemon  backend/index.js\""
```

**Result:** Now, you can run both servers, by executing the ‘both’ in the terminal as follow:
```js
npm run both 
```

**iNotebook application:** Now, we will simply remove all the unwanted files and code from the application and will add some text in app.js, as we want to display something in our iNotebook application
![[inotebook_after_concurrently.webp]]

## Creating Navbar and Routes
### Adding Bootstrap to our React App (iNotebook)
   In the Documentation of Bootstrap, we will find the starter template which has two main things to add bootstrap in our application.
   1. **Bootstrap bundle with popper:**
	   - It contains the Jquery files, Bootstrap.js, and popper.js files. Copy the code and paste it inside the body tag of index.html of the react application.
   
   2. **Bootstrap CSS:**
	  - It contains the CSS files to enhance your application. Simply, Copy the code of Bootstrap CSS and add it inside the head tag of Index.html (In the Public folder) of the iNotebook application.
	  - Now, we can easily use the components of Bootstrap in our Application.
	   
	   
**Remember the following points while copying the code from bootstrap in the react application:**
   - Close those tags which don't have a closing tag. 
   - Replace the ‘class’ keyword with ‘ClassName’.
   - Replace href= “#” with href= “/”
   - The code must be in one tag or use a JSX fragment.

### Creating components
   We are creating a components folder, in which we will create the following components :
   1. **Home:**
	- we will add some random text, like ‘This is Home’ in Home.js to identify the component while opening the iNotebook application.
	
   2. **About:**
	- we will add some random text, like ‘This is About’ in About.js to identify the component while opening the iNotebook application.

   3. **Navbar:**
	- in Navbar.js, we will copy-paste and edit the code of a Navbar, from Bootstrap to save some time.
	- After creating the components, we will simply import and use the components in App.js. But before that let’s quickly look up the setup of react-router.

### Setting up Router

#### Install React Router package
   First of all, we have to install the react-router package, because it is not a part of the core react library.
```js
   npm install react-router-dom
```

#### Set Up routing for our application
   The first thing you have to do is go to the root component, that is, your app.js file, and import Browser Router as Router, Routes, Route.
```js
   Import {BrowserRouter as Router, Switch, Route, Link} from "react-router-dom"
```

1. **Using Router:**
	- Now, we have to surround our entire application with the router component. Hence, To surround your app with the router component, use `<router></router>`.

2. **Using Routes:**
	- The Routes component makes sure that only one route shows at any one time. All of our routes go inside this Routes component.

3. **Using Route**:
	- Alright, we need to set up our individual routes for the About and Home components, and hence we are going to place two routes inside this Route component.
	- Remember to replace the anchor tag with the ‘link’ tag for the proper working of the react-router.
	  ![[inotebook_routes_setup.png]]
	  Here, We have nested our component inside the route which will be displayed when the user visits that specific route. More importantly, this all will occur without the reloading of the page.

## The Context API - Recall
   - The Context API can be used to share data with multiple components, without having to pass data through props manually.
   - Any state inside a context will become accessible to every component of the React Application.

## Getting Started - Context API
   - We will create a context folder in Src folder, to store all the context of the iNotebook application. After that, we will create a Notes sub folder, which will contain all the context related to Notes.
   - Finally, we will be creating some files named NoteState.js and noteContext.js.

## Creating Context - In noteContext.js
   - First of all, we have to import createContext in the file by using the import command.
   - After that, we will be creating a new context with the help of a predefined syntax and finally, we will export the note context as shown in the below figure:
     ![[noteContext_code.webp]]
**Result**: Hence, we have successfully created a context for the iNotebook application. Remember that this context will be holding all the states related to the notes.

## Creating State - In NoteState.js
   Now, we will be creating a state which will be accessible to all the components, which are related to notes.
   
   To create such a state, follow the steps mentioned below:
   ![[inotebook_noteState.webp]]
**Explanation:**
   - In NoteState.js, first of all, we will import noteContext in NoteState.js as shown above.
   - Subsequently, we have created a state object having ‘name’ and ‘class’ items inside the ‘NoteState’ arrow function and finally have returned the NotesContext.Provider, having the values which we want to provide to our components.
   - The Provider component accepts a value prop to be passed to consuming components that are descendants of this Provider.
   - Here, the NoteContext provider contains all the children components, which means that we have to just wrap the application(app.js) inside <NoteState></NoteState>, in order to use the above-created state in every Component and Subcomponents.

### Using the Created Context -In About.js
   Let’s check if the created context is working or not. In our case, we are using the ‘about’ component for testing purposes.
   ![[inotebook_contextState_use_in_aboutjs.webp]]
   
**Explanation:**
  - Above, we have first imported the note context.
  - After doing that, we have used the ‘useContext’ method to accept the values provided by note context.
  - Hence, we have successfully used the ‘name’ property from the state object (Created in NoteState.js).

**Result:** Hence, in the 'about' endpoint we will be getting the string that we have passed as a state.

### Updating the State
   - In NoteState.js, we will be creating an update function, which will help us in updating the ‘s1’ state.
   - In the update function, we have made an update in the ‘Name’ and ‘class’ fields of the state after 1 second.
   - Remember, to import ‘useState’ from React and to pass the ‘update’ in the value of the context Provider.
 ![[inotebook_NoteState_update_function.webp]]

### Using the Update Function -In about.js
   Now, we will be using the use effect hook in about.js to update the context.
   ![[inotebook_aboutjs_update.webp]]
   **Result:** Now, the values of the State will be getting changed after one second of the reloading of the page. This simply means that we can also pass the function as context.

## useLocation Hook
   First of all, let’s refactor the code of NoteState.js and noteContext.js files. IN the previous video, we have added a state and an Update function to these files for the demo purpose. Now, they are not required anymore so we can remove the previous unnecessary code. We will be coming on back to these files in the later articles.

### Enhancing Navbar
   We are changing the ‘‘title’’ and also the looks of the navbar menu by adding a dark color to the Navbar.

### The Use location Hook
   - The Use location hook is a function that returns the location object that contains information about the current URL.
   - Whenever the URL changes, a new location object will be returned. We would be using this hook in our Navbar as discussed below:

**In Navbar.js**
  - In the navbar, you might have spotted that the ‘Home’ section is always highlighted as compared to about. This is so because the class of ‘Home’ is ‘active’.
  - Now, we would like to highlight that link of the navbar which is currently surfed by the client. To do so, we would be using the React Location Hook as mentioned below:

### Applying the Use location Hook
   First of all, we will import the use location hook in Navbar.js and then will begin using this hook to highlight the active link as shown below:
   ![[useLocation_hook1.webp]]

### Highlight Active Link
   Now, you have understood that the React router has a hook which can be very useful to know the current route.
   
   Here is how the use location hook from react-router-dom comes to the rescue.
   ![[inotebook_useLocation_navbar_setup.webp]]
   
**Explanation:**
   - Above, we have used the location hook to specify that whenever the location changes, then highlight the active link according to ‘location.path’.
   - Here, we have made the class ‘Active’ only when the path is equal to ‘/’ and ‘/about’ for the Home and About section respectively.
   - Hence, we have successfully added the functionality of highlighting the active link of the navbar with the interaction of the user.

### Enhancing the Home
   Now, let’s begin enhancing the Home Page of our iNotebook application as shown below:
   ![[inotebook_home_upgrade.webp]]

**Explanation:**
   - Above, We are adding a fascinating Heading, such as “Add a Note”,  in the body of the ‘Home’ menu page of our iNotebook application.
   - Moreover, we have added a form from the bootstrap in Home.

**Our iNotebook**: Here’s the look of our iNotebook application, created till now:

![[inotebook_after_useLocation.webp]]

## Fetching Notes from Context

### Fetch All Notes Endpoint - Recall
   If you remember, we have created the ‘fetchallNotes’ endpoint in the iNotebook thunder client collection, while we were preparing the backend of the application.
   ![[inotebook_fetchallnotes_route_overview.webp]]
### Creating Context - In NoteState.js
   - At this moment, we will copy-paste the response notes in the NoteState.js file (Our Context).
   - Remember, here we are hardcoding the notes in the application. However, In the upcoming articles, we will be learning how to make an API request to fetch the notes in the application.

![[inotebook_notestatejs_overview.webp]]

**Explanation:**
   - In the above scenario, we have passed the Notes and set notes parameter to the use State hook and also we have set the initial value as Notes Initial, the variable containing the fetched notes.
   - After that, we have exported the notes and the set notes with the help of the Provider.
   - Hence, we can use the ‘notes’ and ‘setNotes’ in any component of the iNotebook application. In our case, we will be using it at Home.js as discussed below.

### Using Context - In Home.js
   - This time, we will be rendering the fetched notes from the context in the ‘Your Notes’ section of the iNotebook application in two steps as shown below:

 **Setting Up UseContext Hook**
 ![[inotebook_homejs_context_use.webp]]

**Explanation:**
First of all, we have imported the ‘usecontext’ hook and ‘noteContext’ file in the Home.js. As a result, we are all set to apply ‘use context’ in the Home component.

**Using the Use Context Hook**

![[inotebook_homejs_map_func_context.webp]]

**Explanation:**
   Here, we have used the destructuring method of Javascript to obtain ‘notes’ and ‘SetNotes’ from the Context. Finally, we will be using the map method in the ‘Your Notes’ section to return the notes Title as an array.

**Result:**
   Hence, we are getting the title of the note in the ‘your Notes’ section as shown below. This means that we have successfully fetched the notes in the iNotebook application.
   ![[inotebook_homejs_context_result.webp]]

## iNotebook: Adding NoteItem in a Separate Note component

### Creating Notes Component
   Firstly, we will create a new component named Notes.js. Inside this component, we will add the ‘Your Notes’ section from the Home.js file as shown below:
   ![[inotebook_Notesjs_component.webp]]
   
**Explanation:** 
   - If you remember, in the previous article, we have created the YourNotes section in Home.js.
   - Here, we have just copied the same section and have made a minor change. In the above case, we are returning the ‘NoteItem’ component in the application.
   - Remember, to pass the Note Component in the Home.js file by using <Notes></Notes>.

**Result:** Hence, we have successfully added the ‘Your Notes’ section in a separate Note Component and have passed the ‘note’ prop to the NoteItem component.

### Creating NoteItem Component
   After performing the above step, let’s create a new component named ‘NoteItem.js’ as shown below:
   ![[inotebook_Noteitemjs.webp]]

**Explanation:**
   - Inside the NoteItem component, we have used the destructuring method of Javascript to extract the required properties from the prop.
   - After doing that, we have returned the title and description of the Note to the application.

**Result:** As a result, all the notes will be successfully rendered in the iNotebook application.

Now, we would like to display the notes in a more structured way with the help of the card components of Bootstrap. Let’s see how it is done!

### Adding Card to NoteItems
   Inside NoteItem, first of all, we will add the card component by adding the copied code from the bootstrap as shown below:
   ![[inotebook_Noteitemjs_bootstrap.webp]]

**Explanation:** 
   Above, we have made some changes to the card components. Here, Instead of passing the random card title and description, we have passed the note ‘title’ and ‘description’.

**Result:**  Hence, we have successfully rendered all the notes in a structured way in the iNotebook application as shown below:
![[inotebook_notes_rendered.webp]]

## Adding font awesome icons to iNotebook
   - Font Awesome is a web font used by website designers & developers for icons instead of traditional old image icons.
   - It’s flexible in terms of coloring, sizing & stacking on top of other background styles using plain CSS.

### Adding Font Awesome icons to iNotebook
   - After performing the above step, we can use the icons from the font awesome by simply searching and selecting the icon.
   - In the end, we have to just copy the code provided for that icon by font awesome and paste it in the desired place.
   - In our case, we want the Delete and Edit icon to be displayed in NoteItem, therefore we will add the code of both icons as shown below:

![[inotebook_font_awesome_adding.webp]]

**Result:**  As a result, the delete and Edit icon are added beside the heading of the Note as shown below:
![[inotebook_icon_add_result.webp]]

### Showing an Alert Message
   Subsequently, we would like to add the functionality of deleting the note whenever the client clicks on the delete icon. But, before deleting the note we would like to show an alert message to the client for his/her action. For that purpose, we have to create an alert component in the iNotebook application as discussed below:

#### Creating Alert Component
   First of all, create a new component in the components folder named Alert.js. Inside this component, we will add the bootstrap code for the "Alert" component as shown below:
   ![[inotebook_alert_component.webp]]
   
**Explanation:**
   - Here, we have also passed props to the alert component.
   - Remember to use this alert component in app.js using <Alert/>.
   - In addition to this, we would pass the message from app.js as a prop.

**Result:** Here’s the look at the iNotebook application. As you can observe, we have successfully rendered the alert message in the application.

![[inotebook_after_alert_component.webp]]

## Adding AddNote component to iNotebook

### Creating New Functions
   In NoteState, we would be creating some new functions to add, edit and delete the note as shown below:

### Add a Note Function
   Let’s begin with creating a new function to add a note to the application. So, let’s open the NoteState.js context and begin creating it as shown below:
   ![[inotebook_addnote_func.webp]]
   
**Explanation:**
  - Here, we have used the arrow function with the title, description and tag as parameters.
  - For now, we have made the note hardcoded because we aren’t making the API calls at this very instance.
  - After that, we have concat the ‘note’ in the new Notes array, and have updated the Note State.

**Result:**
Finally, we have to get the Add note function from the NoteState context in Notes.js with the help of the destructuring method of javascript. As a result, we can call the Add note function in Notes.js.

### Creating an Add Note Component
   Now, we will be creating a new component in the components folder named AddNote.js, After that, we will cut-paste the ‘Add Note’ container of Home.js in AddNote.js.
   
   **Basic Steps:**
    - First of all, we will import the note Context in AddNote.js. Consequently, we would use the destructing method to get the ‘AddNote’ function in the ‘AddNote.js’ component from the Context.
    - Make sure to pass the ‘AddNote’ Component in  Note.js by adding <AddNote/>.

### Assigning Function
   Now, we would be assigning the ‘handleClick’ function to the onClick event of the button, which means that on clicking the button the handleClick function will be invoked.
   
### handleClick function
```js
const [note, setNote] = useState({ title: "", description: "", tag: "default" })
const handleClick = (e) => {
    e.preventDefault();
    addNote(note.title, note.description, note.tag);
}
```

**Explanation:**
   - here, we are giving the title, description and tag value to the add note function.
   - Also, we are using the preventdefault() method to prevent the browser from executing the default action of the selected element.
   - Here, we are using the useState hook in AddNote.js to change the state of the Notes. In our case, the initial state of the Title and the description is blank and the tag value is the default.

### Creating onChange Function
   - The onchange event occurs when the value of an element has been changed.
   - Now, we would be assigning the ‘onChange’ function to the onChange event of the Title and the description field, having type as text. However, to use the ‘onchange’ function we have to first create it.
```js
const onChange = (e) => {
    setNote({ ...note, [e.target.name]: e.target.value })
}
```

**Explanation:**
   - Above, All the values inside the note object will remain on executing the ‘onchange’ function. But, the properties written after the note will be added or overwritten.
   - Consequently, we are using the target property to change the name, that is ‘description’ text, to the value of ‘onchange’. Remember, we are taking ‘e’ of the event as a parameter.

**Result:** Now, we are adding and submitting some values in the title and description field as a demo. As a result, We are getting a new note, having those entries, being added in the application as shown below:
![[inotebook_note_adding_demo.webp]]

## Adding "delete note" functionality to iNotebook

### Assigning the deleteNote Function
   - At this moment, we will be adding the feature of deleting the existing Note from the iNotebook by clicking the delete icon, available beside the ‘Title’ text of the Note.
   - To do so, we will add an Onclick listener to the delete icon, available in NoteItems.js. Here’s how it is done:
   ![[inotebook_delete_func_in_Noteitemjs.webp]]
   
**Explanation:**
   - Above, first of all, we have imported the note context and useContext in NoteItem.js.
   - After that, we are taking deleteNote from the Context with the help of the destructing method of Javascript.
   - Consequently, we have added the onClick listener and have provided it with the delete Note function to delete the note by ID.

### Creating a deleteNote Function
   In noteState context, we will be creating the delete note function as shown below:
   ![[inotebook_delete_func_in_noteState_context.webp]]
   
**Explanation**:
   - Above, we have used the filter method to create a new array with all the elements that pass the test successfully. In our case, if note.id is not equal to Id then it will pass the test and would remain in the new notes.
   - Remember, we are just deleting the note on the client-side only. However, we will be adding API calls, later on, to delete the note in the backend of the iNotebook application.

**Result:** Now, we can successfully add and delete an existing note from the client-side of the iNotebook application.
![[inotebook_delete_note_func_result.webp]]

## Adding "fetch notes" functionality to iNotebook

### Creating an EditNote Function
   First of all, we will create an Edit Note function in the NoteState Context of the application. After that, we will be able to use the EditNote function in different components.
   ![[inotebook_editNote_func.webp]]

**Explanation:** 
   - Here, we passed the id, title, description and tag to the Edit Note arrow function as a parameter.
   - After that, we have used the ‘for loop’ to execute the block of code until and unless a specific condition is true. In our case, if element id is equal to an id then the ‘if’ Statement will be executed.

### Update Note API call
   Now, we would like to make an API call to update notes in the backend of the iNotebook application. To do so, we have to use the fetch API as shown below:
   ![[inotebook_editNote_apicall.webp]]

**Explanation:** Above, we are using the fetch API to make a request to the server and make asynchronous HTTP requests in the web browsers
   
   **First Parameter:**  As you can see, the first parameter of the fetch function is the Update Note URL. The URL consists of the host, endpoint and our NotesId.
   
   **Second Parameter:**  
   - After that, the fetch takes a second JSON object with options like method, headers, request body, and so on.
   - In our case, we have declared the method as a ‘Post’ request and have passed the content type and authoken in the header. Remember that the data will be an object consisting of title, description and Tag.

   **Returning Response:** Finally the response object from Fetch will contain the information about the response object itself. This includes headers, status codes, etc. We have used the response.json() method to get the required data from the response object.
   
   **Points to be Noted:** Remember that we have also defined a host variable, making the host as “[https://localhost:5000](https://localhost:5000/)”. As you might have noticed, we are sending a hardcoded authtoken at this very instance. However, in the upcoming articles, we will be sending the authtoken by fetching it from the backend.

### AddNote API call
   We will perform a similar procedure in the addNote API call. The only difference is that we will be using the addNote API instead of the updateNote as shown below:
   ![[inotebook_addNote_apiCall.webp]]
   
### CORS Express Package
   - Now, we are getting an error as the access to fetch the API from the https://localhost:3000 has been blocked by the CORS policy.
   - To resolve this issue, we have to install the express cors package.
   - We will be using the below command to install the cors express package in the backend of the iNotebook application.
```js
npm install cors
```

**After doing this, we will be using the CORS in the Index.js file of the backend by using the below piece of code-**
```js
var cors = require('cors')
app.use(cors())
app.use(express.json())
```

## Creating the Get Note Function
   If you remember, we have hardcoded the notes in the iNotebook application in the NotesInital variable. Now, we will get all the Initial Notes with the help of Fetch API. To do so, we have to first create a Get all note function as shown below:
   ![[inotebook_getallnotes.webp]]

**Explanation:**
   - Above, we have created the GetNotes function, in a similar manner of creating the AddNote function. 
   - Remember, that it doesn’t require any parameter like title, description, or tag. In this scenario, we have made an API call to fetch all notes from the backend**.** In this case, we have declared the method as a GET request and have passed the content type and authoken in the header.
   - Finally, we have set notes equal to the response JSON, that is the notes that will be added to the iNotebook application.

## Using Get Notes Function
   - In Notes.js, we will be getting the getNotes function as a part of the Context. After that, we will be calling this function in the use effect to fetch all notes as shown below.
   - Make sure to import the getNotes function from the NoteState Context as a part of the value.

**Result:**
   Hence, we are getting the available two notes in the iNotebook application. In addition to this, the notes are also added in the iNotebook database of MongoDB as shown below. This proves that the connectivity with the database is working efficiently.
   ![[inotebook_front-end_connected_to_back.webp]]

## Adding a Modal for Editing Notes

   - We will add a modal for editing the existing notes of the iNotebook application.

## Delete note API Call

   ![[inotebook_deletenote_api_call_func.webp]]

**Result**: Hence, we have successfully added the functionality of deleting the note from the database of the iNotebook application.

## Adding a Modal For Editing Notes

   To do so, we will add a modal, which will be opened by clicking the edit icon. The modal will contain a form, having all the details of the specific Note, and we will be able to update the Note easily by changing the values and clicking the Update button.

## Creating an Update Note function

   - In notes.js, First of all, we will create an Update Note function, which will take ‘Note’ as a parameter.
   - We would like to invoke this function, whenever the client clicks on the update icon. Thus,  this update Note function is responsible for rendering the modal of Bootstrap.
   - Before that, let’s add the code of the modal in the Notes.js by copy-pasting it from the Bootstrap as shown below:
   
![[inotebook_updatenote_func.webp]]

**Explanation**:
   - Here, we have made some desired changes in the ‘Text’ and ‘Looks’ of the Modal component of the Bootstrap. Remember, we are launching this modal with the help of Javascript. Here, we are using the ‘useref’ hook of React. As we have discussed earlier that it is a hook that allows us to directly create a reference to the DOM element in the functional component. In our case, we have provided the reference to the  Button of the Modal.
   - Make sure to pass the update note function as a prop to the NoteItem and receive this function from the props, with the help of the destructuring method of javascript, in the NoteItems.js.
   - Finally, we will assign this function to the ‘onClick’ event of the Edit icon, available in NoteItem.js.

**Result:** Hence, the modal will be launched whenever the client clicks on the Edit Icon as shown below-
![[inotebook_editNote_modal.webp]]

## Adding the AddNote Form in the Modal

   Subsequently, we would like to render the AddNote form, to edit the values of the Note, in the Edit Modal. To do so, we will copy-paste the AddNote form from the AddNote.js file. However, we have made some changes in the ‘ID’ and ‘Name’ of the fields to avoid misconceptions.
   ![[inotebook_editNote_modal_form.webp]]
   
**Explanation:**
   - Above, we are adding the ‘handle click’ and ‘Onchange’ function in the Notes.js for editing the values in the fields of the form of Edit Note Modal.
   - Here, we are also using the UseState hook to set the initial value of Title, Description, and Tag. The useState hook is a special function that takes the initial state as an argument and returns an array of two entries.

**Result:** Hence, the AddNote form is being successfully added to the Edit Note Modal as shown below -
![[inotebook_modal_form.webp]]

## Enhancing the Edit Note Modal Form

   Now, we would like to populate the Title, Description, and Tag fields of the form with the values available in the Note. To do so,  we have to populate all the values whenever the update Note Function is executed. Here’s the look of the Update Note function-
   ![[inotebook_update_func_enhancing.webp]]
**Explanation:**
   - Above, we have enhanced the Update Note function. Here, we have passed the current Note as a parameter in the Update Note function and have used the setNote() method. Thus, we have set the values of the ‘current note’ in the Fields of the Edit Modal Form.
   - Make sure to assign the values to all the fields of the Form, available in Notes.js. Also, Assign the Handle Click function to the Onclick event of the Update Note button of the Edit Note Form.

**Result**:
   - Now, the edit note modal contains the forms, which have the existing values of the title, description and Tag fields of the Note.
   - Moreover, the ‘onchange’ is also working efficiently, as we are able to change the values of the title, description and tag fields of the Form.
   - Most importantly, on clicking the update note button, the handle Click function is being successfully executed. Therefore, the updated Notes are rendered as an object in the Console. However, the Notes aren’t updated in the UI of the iNotebook application.
![[inotebook_updatenote_modal_res.webp]]

## Updating Notes on edit in the UI using React

### Closing the Modal

   - First of all, we will add an ID of the Note in the useState hook, created in Notes.js.
   - In addition to this, we would like to set the ID as the current note ID while invoking the "updateNote" function.
   - Consequently, we would like to close the modal after updating the note, that is after the execution of the handle click function. To do that, we have to add logic to click on the ‘close’ button. We can do so with the help of the ‘Useref’ hook of React.

![[inotebook_Notejs_close_modal.webp]]

**Example** - 
   - Here, we have created a new ‘Useref’ named ‘refClose’ and have also added the logic in the handle click function to click on the button having refClose as a reference.
   - Remember that we have provided the Close reference to the close button, as we have done previously with the launch Modal button. As a result, on clicking the update Note button of the Modal, the Modal suddenly disappears.

### Updating the Note

   Now, we would like to update the Note in the Frontend and Backend of the iNotebook application. To do that, follow the procedure mentioned below:
   ![[inotebook_Notejs_editNote_call.webp]]

**Explanation**:
   - Here, we will first get the edit Note function from the NoteState context with the help of the destructuring method.
   - Now, when the user clicks on the update Note button of the modal then we would like to execute the ‘edit note’ function before the closing of the modal. Remember that the edit Note takes ID, Title, description, and tag as a parameter.

### Fixing Errors

   - In NoteState.js, We have assigned the value to ‘response’ and ‘JSON’ but we have never used them. Moreover, we have to use the ‘PUT’ method instead of the ‘POST’ request in the Edit Note function.

**Result:** Hence, we can easily add and update the note in the backend of the application.

### Updating the Note in the Frontend

   Till now, we are able to update the existing note in the backend of the application. However, we would also like to update the note in the front end of the iNotebook application. To do that, we will replace the ‘element’ with ‘newNotes[index]’, in the logic of editing the note on the client-side as shown below:
   ![[inotebook_Notejs_font-end_note_edit.webp]]

**Explanation:**
   - After executing the loop, we have made an exit from the loop with the help of the ‘break’ method. In addition to this, we have created a ‘New Notes’ variable to stringify the notes array.
   - Remember that we have wrapped this logic in the JSON.parsed  to create its deep copy.
   - In the end, we have set the state of the notes as new notes.

**Result:** Hence, we are able to edit and update the note in the backend as well as frontend of the application.

**Here’s the example, we have updated the title and description of all notes as shown below:**
![[inotebook_front-end_and_back-end_res.webp]]

