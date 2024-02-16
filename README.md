# react-101

General information about the React framework

## ****React components****

- React applications are entirely made ouf of components
- Piece of UI that has its own data, logic, and appearance (how it works and looks)
- Able to build multiple components and combining them
- Components can be reused, nested inside each other and pass data between them

## ****What Is JSX****

- Declarative syntax to describe what components look like and how they work
- Extension of JavaScript that allows ut to embed JavaScript, CSS and React components into HTML
- Each JSX element is converted to a React.createElement function call

_Imperative vs Declarative_

`Imperative`

- Manual DOM element selections and DOM traversing
- Step-by-step DOM mutations until we reach the desired UI

`Declartive`

- Describe what UI should look like using JSX, based on current data
- React is an abstraction away from DOM, we never touch the DOM!
- We think of the UI as a reflection of the current data

## ****What are Props****

- Props are used to pass data from parent components to child components
  (down the component tree)
- Essential tool to configure and customize components
  (like function parameters)
- With props, parent components control how child components look and work
- Anything can be passed as props: single values, arrays, objects, function, even other components

## ****Rules of JSX****

- We can enter JavaScript mode by using {} brackets.
- We can place JavaScript expressions inside {}, such as reference variables, create arrays or objects, [].map(),
  ternary operator
- Statements are not allowed (if/else,for,switch)
- A piece of JSX can only have one root element. If you need more use: <React.Fragment> or <> for short.

## ****What is State****

- Data that a component can hold over time, such as information that it needs to remember throughout the app's lifecycle
- Component state: Single local component variable ("Piece of state, state variable")
- Updating component state triggers React to re-render the component

## ****Usage of State****

const [name, setName] = useState('Taylor').

useState returns an array with exactly two items:

- the "name" is the current state variable, initially set to the initial state you provided ("Taylor");
- the set function "setName" that lets you change it to any other value in response to interaction(Ex. button click /
  any event)

## ****State Vs Props****

`State`

- Internal data, owned by component
- Component "memory"
- Can be updated by the component itself
- Updating state causes component to re-render
- Used to make components interactive

`Props`

- External data, owned by parent component
- Similar to function parameters
- Read-only
- Receiving new props causes component to re-render, happens when the parent's state has been updated

## ****Types of States: Local vs Global State****

`Local State`

- State needed only by one or few components
- State that is defined in a component and only that component and child components have access to it (by passing props)

`Global State`

- State that many components might need
- Shared state that is accessible to every component in the entire application

## ****Derived State****

- State that is computed from an existing piece of state or from props
- uses regular variables, no useState
- Works because re-rendering component will automatically re-calculate derived state

## ****Prop Drilling****

- passing props to multiple child compontents to get data to the deepst nested component

## ****Component Composition****

- It consists of combining different components using the children prop (or explicitly defined props)
- We use them to create highly reusable and flexible components
- Fix prop drilling (great for layouts)

---

## Component vs Instance Vs Element

`Component`

- Description of a piece of UI
- A component is a function that returns React elements(element tree), usually written as JSX
- "Blueprint" or "Template"

`Component Instance:`

- Instances are created when we "use" components
- Has its own state and props
- Has a lifecycle (live > die)

`React Element:`

- JSX is converted to `React.createElement()` function calls
- A react element is the result of these function calls
- Information necessary to create DOM elements
- React Element (inserted to DOM) > DOM Element (HTML)
- Finally gets actually visual representation of the component instance in the browser

---

## How renders are triggered in React

#### There are two situations that trigger renders:

1. Initial render of the application
2. State is updated in one or more component instances(re-render)

- The render process is **triggered** for the entire application
- Renders are **not** triggered immediately, but **scheduled** for when the JS engine has some "free time".
- There is also batching of multiple setState calls in event handlers

---

## The render phase of React

1. React Element Tree (Virtual DOM) - **tree** of all React elements created from **all** instances in the component
   tree

- Cheap and fast to create multiple trees
- **Rendering a component will cause all of its child components to be rendered as well (not matter if props changed or
  not)**

2. **Reconciliation** (**Fiber**) + **Diffing**

- **RECONCILIATION**: Deciding which DOM elements actually need to be inserted, deleted, or updated, in order to reflect
  the latest changes
- **THE RECONCILE (FIBER)**: During the initial render of the application Fiber takes the entire element tree (VIRTUAL
  DOM), and based on it builds another tree, the Fiber Tree
- Fibers are **NOT** re-created on every render
- The tree is never destroyed, therefore **immutable data structure**
- Fibers makes the perfect place for keeping track of component state, props, side effects, list of used hooks and more

3. How Diffing works

#### Diffing uses 2 fundamental assumptions(rules):

1) Two elements of different types will produce different trees
   (Same position, **DIFFERENT** element)

- React assumes entire sub-tree is no longer valid
- Old components are destroyed and removed from DOM, including state
- Tree might be rebuilt if children stayed the same (state is reset)

2. Elements with a stable key prop stay the same across renders
   (Same position, **SAME** element)

- Element will be kept (as well as child elements), including state
- New props / attributes are passed if they changed between renders

##### Sidenote:

Work can be done asynchronously ==> rendering process can be split into chunks, tasks can be prioritized, and work can
be paused, reused, or thrown away

- Enables concurrent features like Suspense or transitions
- Long renders won't block JS Engine

`Fiber tree` - Internal tree that has a "fiber" for each component instance and DOM element

---

## The commit phase and browser paint

- React writes to the DOM: insertions, deletions, and updates (list of DOM updates are "flushed" to the DOM)
- Committing is synchronous: DOM is updated in one go, it can't be interrupted
- After the commit phase is finished, the workInProgress fiber tree becomes the current tree for the next render cycle

##### Sidenote:

- React does **NOT** touch the DOM. It **only** renders. It doesn't know where the render result will go
- It can be used on different platforms ("hosts")
- So we have to use renders(committers): like ReactDOM / React Native, which basically commit the result of the render
  phase to certain platforms ("hosts")

---

## What is the KEY prop?

- Special prop that we use to tell the diffing algorithm that an element is unique
- Allows React do distinguish between multiple instances of the same component type
- When a key stays the same across renders, the element will be kept in the DOM (even if the position in the tree
  changes)
- When a key changes between renders, the element will be destroyed and a new one will be created (even if the position
  in the tree is the same as before)

1. Using keys in lists

- Always use the key prop when have multiple child elements of the same type
- Even if the position is different in the tree, the key stays the same, so the elements will be kept in the DOM! (super
  good for performance!)

2. Using keys to reset state

- Always put different key value of the initial component to enable the reset state of the new one

---

## REFRESHER: FUNCTIONAL PROGRAMMING PRINCIPLES:

##### Side effect:

- Dependency on or modification of any data outside the function scope.
  (Interaction with the outside world). Ex: HTTP requests, writing to DOM etc.

##### Pure function:

- Does not change any variables outside its scope
  (Interaction with the outside world). Ex: HTTP requests, writing to DOM etc.
- Given the same input, a pure function always returns the same output

---

## Rules for render logic

- Components must be pure when it comes to render logic:
  given the same props (input), a component instance should always return the same JSX(output)

##### Render logic must produce no side effects: no interaction with the "outside world" is allowed, so in render logic:

- Do **NOT** perform network requests (API calls)
- Do **NOT** start timers
- Do **NOT** directly use DOM API
- Do **NOT** mutate objects or variables outside of the function scope
- This is why we can't mutate props therefore Do NOT update state (or refs): this will create an infinite loop!

---

## How state updates are batched

- Renders are not triggered immediately, but scheduled for when the JS engine has some "free time". There is also
  batching of multiple setState calls in event handlers

1. Updating state is asynchronous:

- First when initially render the event handler function, the state is stored in the Fiber tree during render phase
- At this point, re-render has not happened yet
- Therefore, the variable still contains current state, not the updated state
- UPDATING STATE IN REACT IS ASYNCHRONOUS

