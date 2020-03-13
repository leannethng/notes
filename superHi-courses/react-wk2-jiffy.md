# Jiffy

[Link to project](https://github.com/leannethng/Jiffy-App)

- With create react app , we can write methods inside component as arrow functions instead of using constructor and bind
- `onChange()` Fires when there’s a change in any of the form’s input elements, each keystroke
- Can not use `console.log(event.key);` to see key presses
- To see what key we use we need to use `onKeyPress()`

- I split out my components into different files but i need to access the state form one into another, have just added the search intot he base app for now and will figure out how to lift up state.

- Everytime the input is updated,
  - Runs the `handleChange` event
    - It sets the state with `setState()`
      - set the `searchTerm` and the `hintText`
  - `hintText` is being passed down into the userText Component in render `<userText />`
  - That component is being picked in the properties from where it is defined `const userHint`
  - Being rendered out inside where it is defined.

* Promise is a way for JS to wrap up async code that happens in the BG.
* fetch is wrapped inside a promise - making a promise that it will send something back, result or error etc. This style of using `fetch` is called a Promise chain (because the .then() bits are like a chain of data getting sent along).

```



async function getData() {
  // it starts by trying to run whatever code we tell it
  try {
    const response = await fetch('https://api.website.com/data')
    const data = await response.json()
    return doSomething(data)
    // if something goes wrong, it jumps down to the catch part
  } catch (error) {
    // we can then deal with the error separately
    alert(error.message)
  }
}



```

- asyncronous function by added async before the function `async function getData (){}`
- use `await` keyword inside `async` function.

## State

(Understanding state)[https://codeburst.io/react-js-understanding-state-e875911e921c]

## Random index

Created a closure to pull a random index fromt he object

```
// Create a random choice funtion which takes in an array and returns a random index number. This is a closure!
const randomChoice = arr => {
  const randIndex = Math.floor(Math.random()*arr.length);
  console.log(arr[randIndex]);
  return arr[randIndex];
};

randomChoice(data)

```

## Adding objects to an array

- Create and empty `gifs: []` array as a prop

```
class App extends Component {
  constructor(props){
    super(props)
    this.state = {
      // default states
      searchTerm:'',
      hintText: '',
      gif: null,
      // Creating an empty array for adding gifs to
      gifs: [],
    };
  }
```

Add it to the `setState`

```
      this.setState((prevState, props) => ({
        ...prevState,
        // gets the random result and puts it in the state
        gif: randomGif,

        // here we use spread to take previous gifs and then spread them out, ten add new random gif to the end
        gifs: [...prevState.gifs,randomGif ],

      }))

```

Use that to create multiple video elements

```
  render() {
    const { searchTerm, gif } = this.state;
    return(
      <div>
      {this.state.gifs.map(gif =>
        <video
          className='grid-item video'
          autoPlay
          loop
          src={gif.images.original.mp4}
        />)}
        </div>
    )
  };

```

## Splitting components into their own files

In app.js

```
 render() {
    // const { searchTerm, gif, gifs, index } = this.state;
    return(
      <div className="page">
        <Header />
        <Search
          // Items held in the state are passed down like this
          gifs={this.state.gifs}
          searchTerm={this.state.searchTerm}
          // methods/functions that manipulate state are passed down like this
          handleKeyPress={this.handleKeyPress}
          handleChange={this.handleChange}
        />
        {/* here we pass out userHint and all of our state using a spread operator */}
        <UserHint {...this.state} />
      </div>
    )
  };
```

- Push state down through components with `this.state`
- Push methods or functions that manipulate the state by binding `this` in the construction under the `this.state=`

`this.handleKeyPress = this.handleKeyPress.bind(this);`

- Then add into the component with `handleKeyPress={this.handleKeyPress}`

- In the new component file `Search.js` use `this.props` to call the properties.
  like `onChange={this.props.handleChange}`

- You can also declare the `this.props` below render like

```
render(){
    const { searchTerm, gifs } = this.props;
    return(
```

- Then just call the variable inside the return statement like `value={searchTerm}` instead of `value={this.props.searchTerm}`

### Using Refs

(Refs)[https://reactjs.org/docs/refs-and-the-dom.html]
