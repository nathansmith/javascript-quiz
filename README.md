# JavaScript Quiz

**Note:**

The purpose of this quiz isn't to be a brain-buster. It is meant for recruiters to present to front-end developer candidates.

The intent is to weed out some "Just use jQuery" applicants, but allow those that know JavaScript to pass fairly easily.

## Intro Questions

01. When might comparative type coercion occur? How would you avoid it? How would you change a "falsy" or "truthy" value into a real boolean?

02. Describe how variable scope works. Explain how to create a closure using a self-executing anonymous function (also called IIFE: immediately-invoked function expression).

03. Explain briefly how prototypal inheritance differs from class-based, "classical" inheritance.

04. Describe how the "module pattern" works. Explain how the "revealing module pattern" expands upon it.

05. How does a client-side MVC (or MVVM) approach work? What is your preferred MV* JS framework?

## Additional Questions

06. Why do these yield different results?

    ```js
    '1' + 2 +  3 ; // Equals '123'
     3  + 2 + '1'; // Equals '51'
     3  + 2 +  1 ; // Equals 6
    ```

07. Why is `0.3` *not* the result of the following addition? How do you work around this peculiarity?

    ```js
    0.1 + 0.2; // Equals 0.30000000000000004
    ```

08. Describe how variable hoisting works, and how to avoid bugs that may arise from it.

09. How do these differ?

    ```js
    function foo() {}

    // versus

    var foo = function() {};
    ```

10. When might you use a function's `call()` method, or its `apply()` method?

11. Explain how to determine if a variable is an array or an object. (*Hint:* `typeof` lies!)

12. In the following example, what is foo aliased to? (*Hint:* It is what `this` means.)

    ```js
    (function(foo) {
      // What is 'foo' aliased to?
    })(this);
    ```

13. In JavaScript (and the DOM), some global variables are actually mutable, such as: `window`, `document`, and `undefined`. How would you write code to ensure these were predictably available for use? Assuming someone had injected this code, how would you work around it? (*Hint:* See the previous question.)

    ```js
    var window = '';
    var document = 0;
    var undefined = true;
    ```

14. In one line of code, how you would make a copy of an array?

15. What is the difference between `setInterval` and `setTimeout`? *Bonus:* What is the lowest cross-browser increment that each can accurately use?

16. Explain how `delete` works. What types of things cannot be deleted?

17. Describe how event delegation works, and when you should use it to handle UI interaction. Example markup&hellip;

    ```html
    <ul id="special">
      <li>
        <a href="#">Special link 1</a>
      </li>
      <li>
        <a href="#">Special link 2</a>
      </li>
      <li>
        <a href="#">Special link 3</a>
      </li>
    </ul>
    ```

18. What does this snippet of code do?

    ```js
    var foo = bar ? bar : 0;
    ```

19. When might you write something like this, and what is it shorthand for?

    ```js
    foo && foo.bar();
    ```

20. How do `parseInt` and `parseFloat` differ? When would you use a number's `toFixed()` method? In what instance might the following code snippet actually make sense to use?

    ```js
    var my_number = my_string - 0;
    ```

21. Write a function named `sum` that returns the total of any number of parameters. Example&hellip;

    ```js
    // Should equal 15
    sum(1, 2, 3, 4, 5);

    // Should equal 0
    sum(5, null, -5);

    // Should equal 10
    sum('1.0', false, 1, true, 1, 'A', 1, 'B', 1, 'C', 1, 'D', 1, 'E', 1, 'F', 1, 'G', 1);

    // Should equal 0.3, not 0.30000000000000004
    sum(0.1, 0.2);
    ```
22. What will be the output of the following program ?
    ```js
    var someVar = 7;
    function func(someVar) {
    someVar=4;
    console.log(someVar);
    }
    func();
    console.log(someVar);
    ```

23. What will be the output of the following program ?
    
```js
    var someVar = 5;
    function func() {
    someVar=3;
    console.log(someVar);
    }
    func();
    console.log(someVar);
```

## BONUS Question

When the following code is pasted into a browser's console, what does it output?

```js
(function(window) {

  var hello = 'Hello World';

  var arr = [
    '\x21',
    '\x6E',
    '\x61',
    '\x6D',
    '\x74',
    '\x61',
    '\x42'
  ];

  var str = '';
  var i = 16;

  while (i--) {
    str += 1 * hello;
    str += i % 2 === 0 ? '\x2C\x20' : '';
  }

  str = str.replace(/\x4E+/g, '\x6E');
  str = str.replace(/\x6E\x2C/g, '\x2C');
  str = str.slice(0, 1).toUpperCase() + str.slice(1, str.length);

  str += arr.reverse().join('');

  window.console.log(str);

})(this);
```
