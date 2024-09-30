In JavaScript, `call`, `apply`, and `bind` are methods that allow you to control the context (`this`) in which a function is executed. Here's a breakdown of each method:

### 1. **`call()`**:
   - **Description**: Invokes a function with a specified `this` value and individual arguments.
   - **Syntax**: `functionName.call(thisArg, arg1, arg2, ...)`
   - **Use Case**: Use `call` when you want to invoke a function immediately and pass arguments individually.
   
   - **Example**:
     ```js
     const person = {
       name: 'Alice',
       greet: function(greeting) {
         console.log(`${greeting}, my name is ${this.name}`);
       }
     };
     
     const anotherPerson = { name: 'Bob' };
     person.greet.call(anotherPerson, 'Hello'); // Output: Hello, my name is Bob
     ```
   - **Explanation**: The `greet` function from `person` is called with `anotherPerson` as the `this` context, so the `name` becomes "Bob".

### 2. **`apply()`**:
   - **Description**: Similar to `call`, but it takes arguments as an array instead of listing them individually.
   - **Syntax**: `functionName.apply(thisArg, [arg1, arg2, ...])`
   - **Use Case**: Use `apply` when you want to invoke a function immediately and pass arguments as an array.
   
   - **Example**:
     ```js
     const person = {
       name: 'Alice',
       greet: function(greeting) {
         console.log(`${greeting}, my name is ${this.name}`);
       }
     };
     
     const anotherPerson = { name: 'Bob' };
     person.greet.apply(anotherPerson, ['Hi']); // Output: Hi, my name is Bob
     ```
   - **Explanation**: Like `call`, but here the arguments are passed as an array.

### 3. **`bind()`**:
   - **Description**: Creates a new function that, when invoked, has its `this` value set to the specified value. Unlike `call` and `apply`, `bind` **does not execute the function immediately**; it returns a new function that can be invoked later.
   - **Syntax**: `functionName.bind(thisArg, arg1, arg2, ...)`
   - **Use Case**: Use `bind` when you want to set the context for a function but call it later.
   
   - **Example**:
     ```js
     const person = {
       name: 'Alice',
       greet: function(greeting) {
         console.log(`${greeting}, my name is ${this.name}`);
       }
     };
     
     const anotherPerson = { name: 'Bob' };
     const greetBob = person.greet.bind(anotherPerson, 'Hey');
     greetBob(); // Output: Hey, my name is Bob
     ```
   - **Explanation**: `bind` creates a new function (`greetBob`) with `this` bound to `anotherPerson`, and it can be invoked later.

### Key Differences:

| **Method**   | **Execution**       | **Arguments Passed**                | **Use Case**                           |
|--------------|---------------------|-------------------------------------|----------------------------------------|
| `call()`     | Immediate execution  | Arguments passed individually       | Invoke a function with a specific `this` value and individual arguments. |
| `apply()`    | Immediate execution  | Arguments passed as an array        | Similar to `call`, but arguments are passed as an array. |
| `bind()`     | Delayed execution    | Returns a new function with `this` set | Create a new function with a specific `this` value, for later invocation. |

### Example Showing All Three:
```js
const person = {
  name: 'Alice',
  greet: function(greeting, timeOfDay) {
    console.log(`${greeting}, ${this.name}. Good ${timeOfDay}`);
  }
};

const anotherPerson = { name: 'Bob' };

// Using call
person.greet.call(anotherPerson, 'Hello', 'morning'); // Output: Hello, Bob. Good morning

// Using apply
person.greet.apply(anotherPerson, ['Hi', 'afternoon']); // Output: Hi, Bob. Good afternoon

// Using bind
const greetBob = person.greet.bind(anotherPerson, 'Hey', 'evening');
greetBob(); // Output: Hey, Bob. Good evening
```

In summary:
- `call` and `apply` invoke the function immediately with a different `this` context.
- `bind` returns a new function with `this` bound to the specified context, which you can call later.
