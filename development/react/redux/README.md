# Redux

Redux is a state management for React. The concepts are quite similar to Vuex that I'm more familiar with. So in this note, I'm going to use Vuex to compare and contrast the similarities and differences to get more understanding.

## Concepts

There are three crucial components that make up Redux, namely **store**, **action**, **reducer**.

### Components

#### Store

Like Vuex, **store** is the single soruce of truth for Redux. It's simply a JavaScript object that contains all the states. Treat the store like a snapshot of the application like a commit in *git*. The only way to change the data inside the store is to create another snapshot using **actions**.

#### Actions

**Actions** should be the only way to mutate the states. Imagine the store is a hotel. You should not patch anything yourself. Instead, you should call the service to do it for you and you don't have to know *how* (what steps) the service worker have to take to achieve what you want. You just tell them what you want and they'll do it for you.

#### Reducers

Having to be pure functions, **reducers** are the functions that take the whole state and return the new state accordingly to the given action. Going back to the previous hotel analogy, once you have asked the service to do something (that's an *action*), the service goes through steps to get what you want done. The process of patching is described in the reducer.
