- The Use location hook is a function that returns the location object that contains information about the current URL.
- Whenever the URL changes, a new location object will be returned. We would be using this hook in our Navbar as discussed below:

**In Navbar.js**
   - In the navbar, you might have spotted that the ‘Home’ section is always highlighted as compared to about. This is so because the class of ‘Home’ is ‘active’.
   - Now, we would like to highlight that link of the navbar which is currently surfed by the client. To do so, we would be using the React Location Hook as mentioned below:

### Applying the Use location Hook
   First of all, we will import the use location hook in Navbar.js and then will begin using this hook to highlight the active link as shown below:
   ![[useLocation_hook1.webp]]
   For further information you can look into [[Creating_third_react_app(iNotebook)]]