# React Cheat Sheet
render
------

    render() {
      return <div />;
    }

constructor
-----------
```js
    constructor(props) {
      super(props);
      this.state = {
        list: props.initialList
      };
    }
    
    // where props aren't used in constructor
    
    constructor() {
      super();
      this.state = {
        list: []
      };
    }
```


componentWillMount
------------------
```js
    componentWillMount() {
      // invoked once.
      // fires before initial 'render'
    }
```


componentDidMount
-----------------
```js
    componentDidMount() {
      // good for AJAX: fetch, ajax, or subscriptions.
    
      // invoked once (client-side only).
      // fires before initial 'render'
    }
```


componentWillReceiveProps
-------------------------
```js
    componentWillReceiveProps(nextProps) {
      // invoked every time component recieves new props.
      // does not before initial 'render'
    }
```



shouldComponentUpdate
---------------------
```js
    shouldComponentUpdate(nextProps, nextState) {
      // invoked before every update (new props or state).
      // does not fire before initial 'render'.
    }
```


componentWillUpdate
-------------------
```js
    componentWillUpdate(nextProps, nextState) {
      // invoked immediately before update (new props or state).
      // does not fire before initial 'render'.
    
      // (see componentWillReceiveProps if you need to call setState)
    }
```



**✖ this.setState**

componentDidUpdate
------------------
```js
    componentDidUpdate(prevProps, prevState) {
      // invoked immediately after DOM updates
      // does not fire after initial 'render'
    }
```


componentWillUnmount
--------------------
```js
    componentWillUnmount() {
      // invoked immediately before a component is unmounted.
    }
```


setState (function)
-------------------
```js
    // good for state transitions
    
    this.setState((prevState, props) => {
      return {count: prevState.count + props.step};
    });
```



setState (object)
-----------------
```js
    // good for static values
    
    this.setState({mykey: 'my new value'});
    
    ```

setState (optional callback)
----------------------------
```js
    // fires after setState
    // prefer componentDidUpdate
    
    this.setState(
      (prevState, props) => ({ count: prevState.count + props.step }),
      () => console.log(this.state.count)
    );
```


forceUpdate
-----------
```js
    // forces a re-render; AVOID if possible
    
    this.forceUpdate();
```





displayName
-----------
```js
    displayName: "MyComponent"
    
    
    ```

defaultProps
------------
```js
    class Greeting extends React.Component {
          render() {
            return <h1>Hi {this.props.name}</h1>
          }
        }
        
        CustomButton.defaultProps = {
          name: 'guest'
        };
```



Children.map
------------
```js
    React.Children.map(this.props.children, (child, i) => {
        return child;
    })
```




Children.forEach
----------------
```js
    React.Children.forEach(this.props.children, (child, i) => {
      console.log(child + ' at index: ' + i);
    })
```



Children.count
--------------
```js
    React.Children.count(this.props.children);
```




Children.only
-------------
```js
    React.Children.only(this.props.children);
```




Children.toArray
----------------
```js
    React.Children.toArray(this.props.children)
```


Context (example)
-----------------
```js
    // requires 'prop-types' library
    
    import { string } from "prop-types";
    
    class Cowboy extends React.Component {
      childContextTypes: {
        salutation: string
      }
    
      getChildContext() {
        return { salutation: "Howdy" };
      }
    
      render() {
        return React.Children.only(this.props.children);
      }
    }
    
    const Greeting = (props, context) =>
      <div>{context.salutation} {props.name}.</div>
    
    Greeting.contextTypes = {
      salutation: PropTypes.string
    }
    
    // <Greeting name="Michael" />
    // => Michael.
    
    // <Cowboy><Greeting name="Michael" /></Cowboy>
    // => Howdy Michael.
    
```


contextTypes
------------
```js
    // add to the context-aware component
    // requires 'prop-types' library
    
    contextTypes: {
      color: PropTypes.string
    },
```


childContextTypes
-----------------
```js
    // add to the context provider
    // requires 'prop-types' library
    
    childContextTypes: {
      color: PropTypes.string
    },
```


getChildContext
---------------
```js
    // add to the context provider
    
    getChildContext() {
      return {color: "purple"};
    }

```

