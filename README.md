# ReactJs Questions and Answers
### 1. The bad way to bind event handlers in React
See the example:
```
import React, {Component} from 'react';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'app'
    }
  }
  nameChangeHandler() {
    this.setState({name: 'Salim'})
  }
  render() {
    return (
      <p>Hi, {this.state.name}!</p>
      <button onClick={this.nameChangeHandler.bind(this)}>Change Name</button>
    );
  }
}
```
This is a dynamic binding inside ```render()``` method.
In this case, when render() method is called second time, ```this.handleClick.bind(this)``` will be called and bind the handler again. This call will generate a brand-new handler, which is completely different than the handler used when render() was called the first time.
Following is also a bad way to bind this with fat arrow function inside render():
```
import React, {Component} from 'react';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'app'
    }
  }
  nameChangeHandler() {
    this.setState({name: 'Salim'})
  }
  render() {
    return (
      <p>Hi, {this.state.name}!</p>
      <button onClick={() => this.nameChangeHandler()}>Change Name</button>
    );
  }
}
```
### 2. Right way to bind event handlers in React:

A) Bind handler inside constructor 
```
import React, {Component} from 'react';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'app'
    }
    this.nameChangeHandler = this.nameChangeHandler.bind(this);
  }
  nameChangeHandler() {
    this.setState({name: 'Salim'})
  }
  render() {
    return (
      <p>Hi, {this.state.name}!</p>
      <button onClick={this.nameChangeHandler}>Change Name</button>
    );
  }
}
```
B) Bind handler with fat arrow function
```
import React, {Component} from 'react';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'app'
    }
  }
  nameChangeHandler = () => {
    this.setState({name: 'Salim'})
  }
  render() {
    return (
      <p>Hi, {this.state.name}!</p>
      <button onClick={this.nameChangeHandler}>Change Name</button>
    );
  }
}
```
C) Auto binding with ```react-autobind``` package. This is absolutely a great way of binding ```this```, writing clean code and saving more efforts. See the code:
```
import React, {Component} from 'react';
import autoBind from 'react-autobind';

class App extends Component {
  constructor(props) {
    super(props);
    autoBind(this);
    this.state = {
      name:'app'
    }
  }
  nameChangeHandler() {
    this.setState({name: 'Salim'})
  }
  render() {
    return (
      <p>Hi, {this.state.name}!</p>
      <button onClick={this.nameChangeHandler}>Change Name</button>
    );
  }
}
``` 
D) Also we can use ```lodash-decorators``` for auto binding. See the folowing code:
```
import React, {Component} from 'react';
import { BindAll } from 'lodash-decorators';

@BindAll()
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'app'
    }
  }
  nameChangeHandler() {
    this.setState({name: 'Salim'})
  }
  render() {
    return (
      <p>Hi, {this.state.name}!</p>
      <button onClick={this.nameChangeHandler}>Change Name</button>
    );
  }
}
```
#### 3. How to create a single onChange handler for multiple input ?
Here I have created a single ```changeHandler``` for name and age field. See the code:
```
import React, {Component} from 'react';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'',
      age:'',
    }
  }
  
 changeHandler = event => {
		this.setState({[event.target.name]:event.target.value})
	}
  
  render() {
    return (
      <input name="name" onChange={this.changeHandler} />
			<input name="age" onChange={this.changeHandler} />
			<p>Name: {this.state.name} Age: {this.state.age}</p>
    );
  }
}
```
