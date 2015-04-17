# React Style Guide :recycle:
A style guide for managing sane react components.

# React.js
## Components
  
  - Don't get fancy with manipulating child DOM elements. Map over them and create child components instead.
    
    ```javascript
    render: function() {
      var people = this.props.people.map(function (person,position) {
        if (person){
          return (
            <Person
              person = {person}
              handleUpdate = {this.handleUpdate}
              style = {this.stageStyles(position)}
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
    ```
    
  - Once you see duplicated functionality in your components, use a Mixin. DRY.
  - Don't change state in a child component without letting the parent component know. Deeply nested components are really hard and can be confusing at times if you use too much state and instead of using props data.
  - Class methods, should do one thing. (Single Responsibility Principle)
  - Learn about .bind(); because you're most likely going to be using a scoped ```this``` in a function inside of a function. 

    ```javascript    
    render: function(){
      var editPositionState = function () {
        return this.props.stage.position === this.state.editPosition;  // this.props is undefined
      };
      var editPositionState = function () {
        return this.props.stage.position === this.state.editPosition;  // this.props works!
      }.bind(this);
      // or you can do it the lame way and grab this.props
      // before a function and assign it to a variable.
    }
    ```
  - Make sure the ```render``` method is at the end of the file. And use multi-line if a component has more than two properties.

      ```javascript
      
      <Component
        propertyOne={...}
        propertyTwo={...}
        propertyThree={...}
        …
      />
      ```
  - Use less state and more ```this.props``` in your render method.
  - ###Organization

    ```javascript
    React.createClass({

        propTypes: {},
        mixins: [],

        getInitialState: function() {},
        getDefaultProps: function() {},

        componentWillMount: function() {},
        componentWillReceiveProps: function() {},
        componentWillUnmount: function() {},

        someMethod: function() {},
        dynamicCss: function() {},

        render : function() {}

    })
    ```
  
## Comments
  - Write a comment at the top of the file of who the parent is for the component.
  
## Mixins
  - Use more mixins.
  - I like to prefix mixin methods with ```_mxn_```, so in my components I write ```this._mxn_functionName``` and I know it's from a mixin.
  
## CSS styles in your components
  - I still think about this a lot but it's very nice and useful when you're creating dynamic css styles for your components.
  - abstract your css into a class method for dynamic CSS.

    ```javascript
      cssStyles: function(){...},
    ```
## Testing
  - Jest best practices...

## tools
  - React dev console chrome extension
  - react-rails gem (if you're using rails)
  - an editor that supports vertical split screens for managing hiearchy and thinking about one-way data flow.


# React Native
  - TBA
