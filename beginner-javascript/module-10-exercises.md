# Shopping cart, local storage, event delegation

- Make a submit handler - Typically we don't need to use the default submit, just listen for the 'submit' event, use other JS to listen

- In the console you can right click and set the form as a global variable to access it.

- `console.dir` shows you all the variable you can use with it.

- because we have the input with an id called `item` we can use `e.currentTarget.item.value` to grab the input.

- Every time we have a list of item, it is best to give each a unique id so that they can be easily accessible.

- The button has an X with is the multiply sign `&times`, to help ith accessibility, add in an aria-label with `<button aria-label="Remove ${item.name}">&times;</button>` as that is what the screen reader will say.
