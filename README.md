# ReactJs Questions and Answers
### 1. The bad way to bind event handlers in React
See the example:
```
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
