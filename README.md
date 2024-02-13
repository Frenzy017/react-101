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