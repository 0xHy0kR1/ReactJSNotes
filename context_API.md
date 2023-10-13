### Why use Context API?
   - At a very high level, A react app consists of ‘state’ and ‘components’.
   - As we already know that every component in React has its own state. Due to this reason, building and managing a complex application that has a large number of states and components isn’t an easy task. We can resolve this issue with the help of state lifting technique as mentioned below:

### Understanding State Lifting
   - When different parts of a program or a webpage need to know the same piece of information, like a number or a message, instead of telling each part separately, you can put that information in a higher-level part that they all connect to.
   - The information is lifted up to this parent part, and then it's shared with all the child parts that need it.
   - In a layman language, this simply means sharing a state from one common source.
   - State lifting is accompanied by lifting the state to the parent component as a source to pass the state to the children components.
     ![[state_lifting.webp]]

**Explanation**: In the case of the above app, we can create all the states in app.js(Parent component) as a javascript object, and now we can pass the state to child components.

#### Example - 
Imagine you have a big family, and everyone needs to know some important information, like what's for dinner. Instead of telling each person individually, you can put a note on the fridge where everyone can see it. This way, you're lifting or moving the important information (the state) to a common place (the fridge) for everyone to access.

#### Technical Example - 
   Imagine you're building a digital store, and you want to display the current total price of items in two different places: on the product page and in the shopping cart.
   
   **Without State Lifting**
      - You could create a separate calculator for each place. So, the product page has its own calculator for the total price, and the shopping cart has another one.
      - Whenever you add or remove items, you need to update both calculators separately to keep them in sync. It's like having two cash registers that don't talk to each other.
    
   **With State Lifting**:
      - Instead, you decide to put a single calculator at the entrance of your store. When customers add items to their cart (on the product page or in the shopping cart), they all come to this central calculator to update the total price.
      - It's like having a big price display at the store entrance. Everyone can see it and update it together, ensuring that the total price is always correct, no matter where they are in the store.

**In this analogy:**

  - The separate calculators without state lifting represent different parts of your website (components).
  - The central calculator with state lifting represents a higher-level component (usually the parent component) that holds and manages the shared state (the total price).
  - The customers interacting with the central calculator are your website's components that need to access and update the shared state.
### Understanding Prop Drilling Issue
   - Prop drilling is a situation when the same data is being sent at almost every level due to requirements in the final level.
     ![[prop_drilling.webp]]

   - Let’s assume that in the above application we have to check if the user is logged in while accessing the ‘clothing’ and ‘o2’.
   - In this scenario, if we use the state lifting method then we have to pass the logged-in state from app.js to every component. Hence, it requires a lot of prop drilling as shown below:

**Explanation:**
   - Here, we have to send the ‘login’ state to the ‘offers’ component and then to the ‘O2’ component. In this case, we have to perform a ton of prop drilling to use the logged-in state in the ‘offers’ and ‘O2’ Components.
   - Hence, to resolve such issues in a complex react app, the developers use an amazing feature available in React, named Context API.

### Understanding Context API
   - The Context API can be used to share data with multiple components, without having to pass data through props manually.
     ![[context_api.webp]]

**Explanation:**
   In the above case, we have created a color state in App.js and now we want to use it in C7 and C8. To do so formally, we have to first pass the color to C7, in order to reach C8. A similar situation goes with C7 as well. However, A react developer can create a context, with the help of creating a context feature of the API. After doing that, any of the components in the react application can use a state directly without prop drilling.