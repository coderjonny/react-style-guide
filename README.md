# :recycle: React Style Guide :scroll:
A best practices style guide for managing sane react components.

# React.js

## Components

  - ###Organization
    ```javascript
    
    //<PeopleList>
    //    |
    //    V
    var Person = React.createClass({
        
        // Defaults and initialization properties at the top
        
        propTypes: {},
        getInitialState: function() {},
        getDefaultProps: function() {},

        // Life-cycle methods here
        componentWillMount: function() {},
        componentWillReceiveProps: function() {},
        componentWillUnmount: function() {},

        // Instance methods (any application logic should be refactored out into the Store)
        someHelperMethod: function() {},
        someOtherInstanceMethod: function() {},
        dynamicCss: function() {},

        // The most important method in a react class. Make sure to keep it simple as possible.
        render : function() {},
        
        // Actions handlers down here prefixed with _
        
        _addPoints: function() {}

    })
    ```
    
  - ### Props & State
    - Don't pass props to state. 
      ```javascript
      
        componentDidMount: function(){
          this.setState({ people: this.props.people })
          // BAD: usually a code smell if you're pass down props to state.
        }
      ```
    - Note: replaceState effects entire state, setState merges with the current state.
      ```javascript
      
         this.setState({ isEditing: true });
         ... (later) ... 
         this.replaceState({ isActive: true }); // isEditing no longer part of current state
         this.setState({ isActive: true }); // isActive merges into current state
      ```

  - ###Comments
    - Write a comment at the top of the component class if the component belongs to a parent component, especially if the parent component is passing in ```props```.

  - ###Methods
  - Class instance methods should do one thing. (Single Responsibility Principle)
  - Don't change state in a child component without letting the parent component know. Deeply nested components are really hard and can be confusing at times if you use too much state and instead of using props data.
  - Use less state and more ```this.props``` in your render method.
  - Learn about ```.bind();``` because you're most likely going to be using a scoped ```this``` in a function inside of a function.

    ```javascript
    render: function(){
      var editPositionState = function () {
        // this.props is undefined
        return this.props.stage.position === this.state.editPosition;  
      };
      var editPositionState = function () {
        // this.props works!
        return this.props.stage.position === this.state.editPosition;
      }.bind(this);
      // or you can do it the lame way and grab this.props
      // before a function and assign it to a variable.
    }
    ```
    - or if your using a ES6 transpiler like [Babeljs](https://babeljs.io/) use [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) to keep the correct context.
    ```javascript
    render: function(){
      var editPositionState = () => {
        // this.props works!
        return this.props.stage.position === this.state.editPosition;
      }
    }
    ```


  - Use multi-line jsx if a component has more than two properties.

      ```javascript

      <Component
        propertyOne={...}
        propertyTwo={...}
        propertyThree={...}
        …
      />
      ```

  - Don't get fancy with manipulating child DOM elements. Map over them and create child components instead.
      ```javascript
      // Good
      render: function() {
        var people = this.props.people.map(function (person) {
          if (person){
            return (
              <Person
                person = {person}
                handleUpdate = {this.handleUpdate}
                key = {person.id}/>
            );
          }
        }, this);
  
        return (
          <ul>
            {people}
          </ul>
        )
      }
      
      //Better
      render: function() {
  
        return (
          <ul>
            {
              this.props.people.map(function (person) {
                if (person){
                  return (
                    <Person
                      person = {person}
                      handleUpdate = {this.handleUpdate}
                      key = {person.id}/>
                  );
                }
              }, this);
            }
          </ul>
        )
      }
      ```
      - If it's a simple iteration over an array, render out each of the elements in an array inside jsx.


## Mixins
  - Don't use mixins.. thinking about composable components instead. Mixins will get [deprecated](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750)

## CSS styles in your components
  - Useful when you're creating dynamic css styles for your components and it can be fun!
  - CSS should be unique for a component. 
  - Abstract your css into a class method if it's dynamic CSS. 
  - Throw in that class method of all your inline styles defined into ```style={...}```
    ```javascript
      cssStyles: function(){...},
      
      render: function(){
        return (
          <div style={this.cssStyles()}
            css styles created in JS!
          </div>
        )
      }
    ```

## Testing
  - Jest best practices...

## Tools
  - React dev console [chrome extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
  - react-rails gem (if you're using rails)
  - an editor that supports vertical split screens for managing hiearchy and thinking about one-way data flow.

## Other guides
[airbnb's react/jsx style guide](https://github.com/airbnb/javascript/tree/master/react)

# React Native
  - TBA
