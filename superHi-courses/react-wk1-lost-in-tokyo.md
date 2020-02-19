# Lost in Tokyo Notes

[Link to project](https://github.com/leannethng/Lost-in-Tokyo)

### Toggling Overlay Video

- setState should be used with functions as relying on the value of `this` can not give correct results in a larger app

- [Using a function in `setState` instead of an object](https://medium.com/@wisecobbler/using-a-function-in-setstate-instead-of-an-object-1f5cfd6e55d1)

```
  toggleInfo(e){

    this.setState((prevState, props) => {
      return {
        showInfo: !prevState.showInfo
        }

    })
  }
```
