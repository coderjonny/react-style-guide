# :recycle: React Style Guide :scroll:
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

  - Don't change state in a child component without letting the parent component know. Deeply nested components are really hard and can be confusing at times if you use too much state and instead of using props data.
  - Class methods, should do one thing. (Single Responsibility Principle)
  - Learn about .bind(); because you're most likely going to be using a scoped ```this``` in a function inside of a function.

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
    
    //<PeopleList> --> <Person>
    
    var Person = React.createClass({

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

  - Comments
    - Write a comment at the top of the component if the component belongs to a parent.

## Mixins
  - Use more mixins.
  - Once you see duplicated functionality in your components, use a Mixin. DRY.
  - I like to prefix mixin methods with ```_mxn_```, so in my components I write ```this._mxn_functionName``` and I know it's from a mixin.

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
  - React dev console chrome extension
  - react-rails gem (if you're using rails)
  - an editor that supports vertical split screens for managing hiearchy and thinking about one-way data flow.


# React Native
  - TBA
