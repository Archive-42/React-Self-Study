# Beginner’s Guide To React Part 2

> As I learn to build web applications in React I will blog about it in this series in an attempt to capture the questions that a complete…

Here I will walk through a demo…. skip down below for more fundamental examples and resources…

*   ex1 — A Basic React Component
*   ex2 — A Basic React Class Component
*   ex3 — A Class Component with State
*   ex4 — A Class Component that Updates State
*   ex5 — A Class Component that Iterates through State
*   ex6 — An Example of Parent and Child Components

With regards to converting an existing HTML, CSS, and JS site into React, first you’ll want to think about how to break up your site into components,

*   as well as think about what the general hierarchical component structure of your site will look like.
*   From there, it’s a simple matter of copying the relevant HTML for that component and throwing it into the **render method of your component file.**
*   _Any methods that are needed for that component to function properly can added onto your new component._

Once you’ve refactored your HTML components into React components, you’ll want to lay them out in the desired hierarchical structure

*   with children components being rendered by their parents, as well as ensuring that the parent components are passing down the necessary data as props to their children components.

ex.)
```html
<!-- Hello world -->  
<div class="awesome" style="border: 1px solid red">  
  <label for="name">Enter your name: </label>  
  <input type="text" id="name" />  
</div>  
<p>Enter your HTML here</p>
```
Is equivalent to:


A component is some thing that is being rendered in the browser. It could be a button, a form with a bunch of fields in it…etc.…

React doesn’t place any restrictions on how large or small a component can be.

You _could_ have an entire static site encapsulated in a single React component, but that would defeat the purpose of using React.

So the first thing to remember about a component is that a **component must _render_ something.**

_If nothing is being rendered from a component, then React will throw an error._

Inside of `BasicComponent.js` , first import React at the top of the file. Our most basic of components looks like this:

> _This is a component that simply returns a div tag with the words Hello World! inside._
> 
> _The last line simply exports our component so that it can be imported  
> by another file._

Notice that this component looks exactly like an anonymous arrow function that we’ve named `BasicComponent` .

In fact, that is literally what this is.

The arrow function then is simply returning the div tag. When a component is written as a function like this one is, it is called a _functional_ component.

The above component is an example of a functional component, which is appropriate since that component is literally nothing more than a function that returns some HTML.

_Functional components are great when all you want a component to do is to render some stuff._

_Components can also be written as classes (although this paradigm is becoming outdated and you should strive to write your components functionally!_

For this exercise, we’re going to write a class component that does exactly the same thing as the functional component we just wrote.

We’ll again need to import React at the top of the file, but we’ll also need to add a little something. Our import statement will look like this:

import React, { Component } from 'react';

**So, in addition to importing React, we’re also importing the base Component class that is included in the React library.**

React lets you define components as classes or functions.
---------------------------------------------------------

Components defined as classes currently provide more features . To define a React component class, you need to extend `React.Component`:
```jsx
class Welcome extends React.Component {  
  render() {  
    return <h1>Hello, {this.props.name}</h1>;  
  }  
}
```
**The only method you _must_ define in a** `**React.Component**` **subclass is called** `[**render()**](https://reactjs.org/docs/react-component.html#render)`**.**

The `render()` method is the only required method in a class component.

When called, it should examine `this.props` and `this.state` and return one of the following types:

*   **React elements.** Typically created via [JSX](https://reactjs.org/docs/introducing-jsx.html). For example, `<div />` and `<MyComponent />` are React elements that instruct React to render a DOM node, or another user-defined component, respectively.
*   **Arrays and fragments.** Let you return multiple elements from render. See the documentation on [fragments](https://reactjs.org/docs/fragments.html) for more details.
*   **Portals**. Let you render children into a different DOM subtree. See the documentation on [portals](https://reactjs.org/docs/portals.html) for more details.
*   **String and numbers.** These are rendered as text nodes in the DOM.
*   **Booleans or** `**null**`. Render nothing. (Mostly exists to support `return test && <Child />` pattern, where `test` is boolean.)

The `render()` function should be pure, meaning that it does not modify component state, it returns the same result each time it’s invoked, and it does not directly interact with the browser.

If you need to interact with the browser, perform your work in `componentDidMount()` or the other lifecycle methods instead. Keeping `render()` pure makes components easier to think about.

> _Note_
> 
> `_render()_` _will not be invoked if_ `[_shouldComponentUpdate()_](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)` _returns false._

The export statement at the bottom of the file also stays, completely unchanged. Our class component will thus look like this:

**Notice that our** `**BasicClassComponent**` **inherits from the base** `**Component**` **class that we imported from the React library, by virtue of the 'extends' keyword.**

_That being said, there's nothing in this minimal component that takes advantage of any of those inherited methods._

**All we have is a method on our component class called** `**render**` **that returns the same div tag.**

If we really were deciding between whether to use a functional component versus a class component to render a simple div tag, then the functional style is more appropriate to use.

This is because class components are much better suited for handling component state and triggering events based on the component’s [lifecycle.](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

The important takeaways at this point are that there are two types of components, functional and class components, and that functional components are well-suited if you’re just looking to render some HTML.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

_Class components, on the other hand, are much better suited for handling components that require more complex functionality, need to exhibit more varied behavior, and/or need to keep track of some state that may change throughout said component’s lifecycle._

**Component state is any dynamic data that we want the component to keep track of.**

> For example, let’s say we have a form component. This form has some input fields that we’d like users to fill out. When a user types characters into an input field, how is that input persisted from the point of view of our form component?

**The answer is by using component state!**

There are a few important concepts regarding component state, such as how to update it, pass it to another component, render it, etc.

**Only class components have the ability to persist state, so if at any time you realize that a component needs to keep track of some state, you know that you’ll automatically need a class component instead of a functional component.**

> It is possible to handle state with functional components but that requires the use of something called the [useState() hook](https://reactjs.org/docs/hooks-state.html). Hooks were added in React 16.8; prior to this release, there was no mechanism to add state to functional components.

Here’s what the above component looks like as a functional component:

Our class component with state will look a lot like the basic class component we just wrote, but with some exceptions:

**So far, the only new thing going on here is the constructor block. If you recall how classes in JavaScript work, classes need constructors.**

**Additionally, if a class is extending off of another class and wants access to its parent class’s methods and properties, then the** `**super**` **function needs to be called inside the class's constructor function.**

Point being, the constructor function and the call to the `super` function are _not_ associated with React, they are associated with all JavaScript classes.
------------------------------------------------------------------------------------------------------------------------------------------------------------

*   Then there is the `**this.state**` **property inside the constructor function that is set as an empty object**.
*   We're adding a property called `state` to our class and setting it to an empty object.

State objects in React are always just plain old objects.
---------------------------------------------------------

**So why is it that the basic class component we wrote in the previous exercise had no constructor function within its body?**
------------------------------------------------------------------------------------------------------------------------------

That is because we had no need for them since all our class component was doing was rendering some HTML.

**The constructor is needed here because that is where we need to initialize our state object.**

**The call to** `**super**` **is needed because we can't reference** `**this**` **inside of our constructor without a call to** `**super**` **first.**

Ok, now let’s actually use this state object.

_One very common application of state objects in React components is to render the data being stored inside them within our component’s render function._

Refactoring our component class to do that:
-------------------------------------------

We added a key-value pair to our state object inside our constructor.

*   Then we changed the contents of the render function.
*   Now, it’s actually rendering the data that we have inside the state object.
*   Notice that inside the div tags we’re using a template string literal so that we can access the value of `this.state.someData` straight inside of our rendered content.

**With Reacts newest version, we can actually now add state to a component without explicitly defining a constructor on the class. We can refactor our class component to look like this:**

This new syntax is what is often referred to as ‘syntactic sugar’: under the hood, the React library translates this back into the old constructor code that we first started with, so that the JavaScript remains valid to the JavaScript interpreter.

The clue to this is the fact that when we want to access some data from the state object, we still need to call it with `this.state.someData` ; changing it to just `state.someData` does not work.

Great, so we can render some state that our component persists for us.

However, we said an important use case of component state is to handle _dynamic_ data.

A single static number isn’t very dynamic at all.

So now let’s walk through how to update component state.

Notice that we’ve added two methods to our class: `increment` and `decrement` .

`increment` and `decrement` are methods that _we_ are adding to our class component.

Unlike the `render` method, `increment` and `decrement` were not already a part of our class component.

This is why `increment` and `decrement` are written as arrow functions, **_so that they are automatically bound to our class component._**

The alternative is using a declaration syntax function with the bind method to bind the context of our methods to the class component.

The more interesting thing is what is going on within the bodies of these methods.

Each calls the `setState` function.
-----------------------------------

*   `setState` in fact _is_ provided to us by React.

It is the standard way to update a component's state.

It's the _only_ way you should ever update a component's state. It may seem more verbose than necessary, but there are good reasons for why you should be doing it this way.

So the way to use `setState` to update a component's state is to pass it an object with each of the state keys you wish to update, along with the updated value.
----------------------------------------------------------------------------------------------------------------------------------------------------------------

In our `increment` method we said "I would like to update the `aNumber` property on my component state by adding one to it and then setting the new value as my new `aNumber` ".

The same thing happens in our `decrement` method, only we're subtracting instead of adding.

Then the other new concept we’re running into here is how to actually call these methods we’ve added to our class.

![](https://miro.medium.com/max/1690/1*k8t5QBcMvHDX521sd4pC4g.png)

We added two HTML button tags within our `render` function, then in their respective `onClick` handlers, we specify the method that should be called whenever this button gets clicked. So whenever we click either of the buttons, our state gets updated appropriately and our component will re-render to show the correct value we're expecting.

Another common state pattern you’ll see being used in React components is iterating over an array in our state object and rendering each array element in its own tag.

> This is often used in order to render lists.

Additionally, we want to be able to easily update lists and have React re-render our updated list.

We’ll see how both of these are done and how they work together within a single component in order to create the behavior of a dynamic list.

The first change to note is that our state object now has an ‘ingredients’ array, and a ‘newIngredient’ field that has been initialized to an empty string.

The ingredients array contains the elements that we’ll want to render in our list.

The `addIngredient` and `handleIngredientInput` methods we've added to our class receives a parameter called 'event'.

This event object is part of the browser's API.

When we interact with some DOM element, **such as clicking on an HTML button, the _function that is invoked upon that button being clicked_ actually receives the event object.**

*   So when we type some input into an input tag, we're able grab each character that was typed into the input field through the event object parameter.
*   The `handleIngredientInput` method is what gets invoked every time the user presses a key to enter text in the input box for adding a new ingredient.
*   Every character the user types gets persisted in the `newIngredient` field on the state object.

We're able to grab the text in the input box using `event.target.value`

**Which holds the value of the string text that is currently in the input box**.

> We use that to update our `newIngredient` string field.

Breaking down the `addIngredient` method, we see this `event.preventDefault()` invocation.

This is because this method will be used upon submitting a form, and it turns out that submitting a form triggers some default form behavior that we don't want to trigger when we submit the form (**namely refreshing the entire page**).

> `event.preventDefault()` will prevent this default form behavior, meaning our form will only do what we want it to do when it is submitted.

![](https://miro.medium.com/max/1766/1*RN_y7Bk4tb-LLG8vNqGHHA.png)

Next, we store a reference to `this.state.ingredients` in a variable called `ingredientsList` .

So we now have a copy of the array that is stored in our state object.

**We want to update the copy of the ingredients array first instead of directly updating the actual array itself in state.**

Now we push whatever value is being stored at our `newIngredient` field onto the `ingredientsList` array so that our `ingredientsList` array is now more up-to-date than our `this.state.ingredients` array.

So all we have to do now is call `setState` appropriately in order to update the value in our state object.

Additionally, we also set the `newIngredient` field back to an empty string in order to clear out the input field once we submit a new ingredient.

Now it's ready to accept more user input!

![](https://miro.medium.com/max/944/1*LXx7WeP_5wFRfYa45snSEA.png)

Looking at our render function, first note the `this.state.ingredients.map` call.

This is looping through each ingredient in our `ingredients` array and returning each one within its own div tag.

This is a very common pattern for rendering everything inside an array.

Then we have an HTML form which contains an input field.

The purpose of this form is to allow a user to add new ingredients to the list. Note that we’re passing our `addIngredient` method to the form's `onSubmit` handler.

This means that our `addIngredient` method gets invoked whenever our form is submitted.

Lastly, the input field has an `onChange` handler that invokes our `handleIngredientInput` method whenever there is some sort of change in the input field, namely when a user types into it.

![](https://miro.medium.com/max/1612/1*S7s9FfaPVlKGyaSwFeId_w.png)

Notice that the `value` field in our input tag reads off of `this.state.newIngredient` in order to know what value to display.

So when a user enters text into the input field, the `onChange` handler is invoked every time, which updates our `this.state.newIngredient` field, which the input field and then renders.

A single isolated component isn’t going to do us much good.

> The beauty of React lies in the fact that it allows us to compose modular components together.
> 
> Let’s start off with the component we just saw, but let’s change its name to `_ParentComponent_` .

The only two other differences in this component are that we’re importing a `ChildComponent` and then using it inside our `this.state.ingredients.map` call.

`ChildComponent` is another React component.

Notice that we're using it just as if it were any other HTML tag.

**This is how we lay out our component hierarchy: the ChildComponent is rendered within the ParentComponent.**

We can see this to be the case if we open up the developer console and inspect these elements.

Note also that we’re passing each ingredient as a ‘thing’ to the ChildComponent component.

This is how a parent component passes data to a child component. It doesn’t need to be called ‘thing’; you can call it whatever you want.

Conceptually though, **every piece of data that a parent component passes down to a child component is called a ‘prop’ in React lingo.**

Let’s take a look now at the Child Component. It serves two purposes:

1.  to render the props data that it gets from a parent component,
2.  to add the ability for a user to click on it and have it toggle a strikethrough, indicating that the item is ‘complete’.

The overall structure of the child component is nothing we haven’t seen. It’s just another class component with its own s**tate object and a method called** `**handleClick**` **.**

**A component accesses its props via the** `**this.props**` **object.**

_Any prop a parent component passes down to a child component is accessible inside the child component's_ `_this.prop_` _object._

So our child component keeps its own state that tracks whether the component has been clicked or not.

Then at the top of the `render` function, it uses a ternary condition to determine whether the div tag that is being rendered should have a strikethrough or not.

The `handleClick` method is then invoked via an `onClick` handler on the div tag; it does the work of toggling the `this.state.clicked` Boolean.

The overall structure of React applications can be represented as a hierarchical tree structure, just like how the DOM itself is structure. There is an overarching root component at the top of the hierarchy that every other component sits underneath. Specifying that a component should be a child of some parent component is as simple as throwing it in the parent component’s render function, just like how we did it in this example

![](https://miro.medium.com/max/968/0*aqqfHMjBXT8PWYJC)


[Source](https://bryanguner.medium.com/introductory-react-part-2-cda01615a186)
