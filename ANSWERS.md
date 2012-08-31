# JavaScript Quiz &mdash; with Answers

**Note:**

If you've skipped the questions and come straight here, or have found this page because you're trying to cheat: Tisk, tisk!

Joking aside though, if you're a job applicant skimming these answers so that you can make (fake?) it through an interview, bear in mind that a cheat sheet isn't the same as knowledge. You should still strive to understand these concepts.

**:)**

## Intro Questions

01. When might comparative type coercion occur? How would you avoid it? How would you change a "falsy" or "truthy" value into a real boolean?

    **Answer:**

    Type coercion occurs when comparing values of different types. For instance, if you're comparing a number with a string, they will be changed on the fly (coerced) into a loose "truthy" or "falsy" comparison. To avoid type coercion, to ensure you are comparing values strictly and taking their potentially differing types into account, always use triple-equals `===` instead of the more commonly used (in other languages) double-equals `==`. Likewise, when comparing if two values are *not* the same, use `!==` instead of `!=`.

    ```js
    // This is good
    if (a === b) {}
    if (a !== b) {}

    // This is bad
    if (a == b) {}
    if (a != b) {}
    ```

    Sometimes you will have a variable that may be "truthy" or "falsy" itself, but need to infer a real `true` or `false` boolean from it. In such cases, you can use double negation `!!`, to say "not not something," the result of which is either `true` or `false`.

    ```js
    // Is always a real boolean
    var real_boolean = !!something;
    ```

02. Describe how variable scope works. Explain how to create a closure using a self-executing anonymous function (also called IIFE: immediately-invoked function expression).

    **Answer:**

    Variables in JavaScript are implicitly global (a very bad thing) unless you declare them with a preceding `var` keyword. Doing so ensures that the variable is scoped no higher than the nearest containing function. A self-executing anonymous function (aka IIFE) is a function that immediately runs, keeping the variables inside it safely quarantined away from the global scope.

    For more on this topic:

    http://benalman.com/news/2010/11/immediately-invoked-function-expression

    ```js
    // These are functions
    // used as closures...

    // This is good
    (function() {
      var foo = 'bar';
    })();

    // This is bad
    (function() {
      foo = 'bar';
    })();
    ```

03. Explain briefly how prototypal inheritance differs from class-based, "classical" inheritance.

    **Answer:**

    Classical and prototypal inheritance both involve having a base template from which other things are created. For example, one might have a class named `Dog`, from which you could create an instance of a dog, named `sparky`. If you changed something related to `Dog`, then `sparky` would immediately receive those attributes as well.

    Class based languages distinguish between templates (classes) and instances created from classes, whereas prototypal languages do not. The "super class" of an object in JavaScript is simply another instance.

    ```js
    // Creating a base Dog, which is alive.
    function Dog() {}
    Dog.prototype.is_alive = true;

    // All instances of Dog will have 4 legs.
    Dog.prototype.legs = 4;

    // Sparky is alive, has 4 legs, and is brown.
    var sparky = new Dog();
    sparky.color = 'brown';

    // Now sparky has 2 wings, as do all other dogs!
    Dog.prototype.wings = 2;

    // We just killed all dogs, and sparky too. Oh no!
    Dog.prototype.is_alive = false;
    ```

04. Describe how the "module pattern" works. Explain how the "revealing module pattern" expands upon it.

    **Answer:**

    The "module pattern" expands upon the concept of a self-executing anonymous function, by having a `return` at the end, which exposes some properties/methods as publicly accessible (and therefore, mutable). The result of this `return` is assigned to a variable, which serves as an app/module "namespace."

    The "revealing module pattern" works in much the same way, except instead of bundling up all properties/methods into a single object literal, local variables are assigned to properties of an object literal at the end of the closure.

    ```js
    // Module Pattern
    var MY_APP_ONE = (function() {
      // Private variables
      var secret_1 = 'Hello';
      var secret_2 = 'World';

      // Publicly exposed
      return {
        // MY_APP_ONE.foo
        foo: function() {
          // Do stuff
        },
        // MY_APP_ONE.bar
        bar: function() {
          // Do stuff
        }
      }
    })();

    // "Revealing" Module Pattern
    var MY_APP_TWO = (function() {
      // Private variables
      var secret_1 = 'Hello';
      var secret_2 = 'World';

      // MY_APP_TWO.foo
      function foo() {
        // Do stuff
      }

      // MY_APP_TWO.bar
      function bar() {
        // Do stuff
      }

      // "Revealed" here,
      // otherwise private
      return {
        foo: foo,
        bar: bar
      }
    })();
    ```

05. How does a client-side MVC (or MVVM) approach work? What is your preferred MV* JS framework?

    **Answer:**

    A client-side MVC (model, view, controller) approach enforces "separation of concerns" across the front-end code of an app. You have *models* that handle the domain-specific information of your app, *controllers* that handle the user interactions (or programmatically triggered events), and *views* present information from the *model* in a palatable way to the user. A *view* also contains elements which are interacted with, that a *controller* observes (and if need be, informs a *model*).

    MVVM differs slightly from MVC, in that it has "models," "views," and "view models." A *view model* handles the observation of events (handled by a *controller* in MVC), as well as the data-binding between a *model* and a *view*.

    Answers for preferred MV* frameworks may include: Backbone.js, Ember.js, or Knockout.js. There are also MVC aspects to larger JS libraires, such as YUI and Dojo.

    Backbone.js (Model View Router)<br />
    http://backbonejs.org

    Ember.js (MVC)<br />
    http://emberjs.com

    Knockout.js (MVVM)<br />
    http://knockoutjs.com

    YUI App Framework (MVC)<br />
    http://yuilibrary.com/yui/docs/app

    Dojo MVC<br />
    http://dojotoolkit.org/reference-guide/1.8/dojox/mvc.html

    **Note:**

    MVC and/or MVVM in JavaScript differ from frameworks such as .NET MVC or Ruby on Rails, in that, the entirety of a client-side MVC is housed in the "V" of a server-side framework. That is, HTML/CSS/JS, sitting atop a server-side framework &mdash; which itself may (or may not) be MVC in nature.

## Additional Questions

06. Why do these yield different results?

    ```js
    '1' + 2 +  3 ; // Equals '123'
     3  + 2 + '1'; // Equals '51'
     3  + 2 +  1 ; // Equals 6
    ```

    **Answer:**

    When the JavaScript interpreter sees a string value (contained within quotes), it immediately begins type coercing all the following values into strings. In the first line, `'1'` is a string, thus `2` becomes `'2'` and `3` becomes `'3'`. They are simply appended to one another, the same way this might work&hellip;

    ```js
    'A' + 'B' + 'C'; // Equals 'ABC'
    ```

    On the second line, because `3` and `2` are real numbers, so those are first added together, yielding `5`. The next value `'1'` is actually a string, so `5` is converted to `'5'`, and it is string concatenated with `'1'`, yielding `'51'` as a string.

    On the third line, all the values are real numbers, so they are added together as expected, yielding the number `6`.

07. Why is `0.3` *not* the result of the following addition? How do you work around this peculiarity?

    ```js
    0.1 + 0.2; // Equals 0.30000000000000004
    ```

    **Answer:**

    Believe it or not, this is by design. It is simply how floating-point calculations work, but does not make sense when you encounter it in practical usage. In order to do math with any kind of decimal precision, you need to multiply values by `10`, do addition or subtraction as full integers, and then divide back by `10`. It is a laborious, but necessary step, especially when calculating anything related to money in the browser.

    More on floating-point arithmetic here&hellip;

    http://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html

08. Describe how variable hoisting works, and how to avoid bugs that may arise from it.

  Regardless of where you declare your variables within the scope of a function, the JavaScript interpreter will always move them to the beginning of the function in its internal understanding of the code. This phenomenon is called "hoisting." Since the process itself cannot be avoided, it is best to declare your variables at the top of a function's scope. Though, in practicality, it tends not to be an issue as long as you don't attempt to use variables before they are defined.

09. How do these differ?

    ```js
    function foo() {}

    // versus

    var foo = function() {};
    ```

    In the first case, a function named `foo` is being created. The interpreter parses function names before attempting to execute any code, so that function can be able called before it's declared. In the second case, an *anonymous* function is being defined with an expression and is assigned to a variable.

    Variables cannot be referenced before they are declared, and that function can't be called because it has no name. In practice, because of variable hoisting, one should always declare a function before using it, regardless of syntax.

    ```js
    // This breaks
    my_function_one();
    var my_function_one = function() {};

    // This works
    my_function_two();
    function my_function_two() {}
    ```

10. When might you use a function's `call()` method, or its `apply()` method?

    The `call()` method takes any number of parameters, the first of which is the context of `this`. Let's say you wanted to set properties on a new instance of a constructor. Example&hellip;

    ```js
    function Human(first_name, last_name) {
      // Default to "John Doe"
      this.first_name = first_name || 'John';
      this.last_name = last_name || 'Doe';
    }

    // Pass in a new name
    function Person(first_name, last_name, gender) {
      Human.call(this, first_name, last_name);
      this.gender = gender || 'male';
    }

    // logs "John Doe is male"
    var john = new Person();
    console.log(john.first_name, john.last_name, 'is ' + john.gender);

    // logs "Pam Jones is female"
    var pam = new Person('Pam', 'Jones', 'female');
    console.log(pam.first_name, pam.last_name, 'is ' + pam.gender);
    ```

    The `apply()` method is similar to `call()`, except that it takes a single array as its second parameter (instead of an arbitrary number of parameters). It is typically used to run built-in functions from object prototypes. The following example can take any number of values and concatenate them into a single string&hellip;

    ```js
    // Take any number of parameters, stringify them
    function concatenate() {
      return String.prototype.concat.apply('', arguments);
    }

    // Outputs 'false1hello'
    concatenate(false, 1, 'hello');
    ```

11. Explain how to determine if a variable is an array or an object. (*Hint:* `typeof` lies!)

    **Answer:**

    If you only checked a variable's `typeof`, regardless if it were an object or an array, it would reply `'object'`.

    One possible answer to this question would be to check if it's an object, *and* determine if it has a numeric `.length` (which may be `0` if it's an empty array). However, this would also work for the `arguments` object (all the parameters passed into any given function), which is technically *not* an array. Additionally, this falls down if an object should have a `.length` property.

    ```js
    // Real array
    var my_array = [];

    // Imposter!
    var my_object = {};
    my_object.length = 0;

    // Potentially faulty
    function is_this_an_array(param) {
      if (typeof param === 'object' && !isNaN(param.length)) {
        console.log('Congrats, you have an array!');
      }
      else {
        console.log('Bummer, not an array');
      }
    }

    // Works
    is_this_an_array(my_array);

    // Works, but is incorrect
    is_this_an_array(my_object);
    ```

    Another way to answer this question would be to use a more obscure method, calling `toString()` to convert the variable in question to a string representation of its type. This will work for a real array, but fail for the `arguments` object, which when converted into a string is `[object Arguments]`. It also won't be fooled by an object with a numeric `.length` attribute.

    ```js
    // Real array
    var my_array = [];

    // Imposter!
    var my_object = {};
    my_object.length = 0;

    // Rock solid
    function is_this_an_array(param) {
      if (Object.prototype.toString.call(param) === '[object Array]') {
        console.log('Congrats, you have an array!');
      }
      else {
        console.log('Bummer, not an array');
      }
    }

    // Works
    is_this_an_array(my_array);

    // Not an array, yay!
    is_this_an_array(my_object);
    ```

    Also, though potentially unreliable in multi-frame DOM environments, `instanceof` is a perfectly suited operator.

    Further reading: *"Instanceof Considered Harmful&hellip;"*

    http://perfectionkills.com/instanceof-considered-harmful-or-how-to-write-a-robust-isarray

    ```js
    var my_array = [];

    if (my_array instanceof Array) {
      console.log('Congrats, you have an array!');
    }
    ```

    As of JavaScript 1.8.5 (ECMAScript 5), the aptly named `.isArray()` method serves this purpose&hellip;

    ```js
    var my_array = [];

    if (Array.isArray(my_array)) {
      console.log('Congrats, you have an array!');
    }
    ```

12. In the following example, what is foo aliased to? (*Hint:* It is what `this` means.)

    ```js
    (function(foo) {
      // What is 'foo' aliased to?
    })(this);
    ```

    **Answer:**

    In a browser, it is `window`. In Node.js, it is `global`.

    The context of the `this` keyword is always equal to the present scope in which it is used. At the global level (in a browser), `this` is the same as `window`, because there is no higher level of scope. In Node.js (running on a server), since there isn't actually a `window`, the highest level scope is simply called `global`.

13. In JavaScript (and the DOM), some global variables are actually mutable, such as: `window`, `document`, and `undefined`. How would you write code to ensure these were predictably available for use? Assuming someone had injected this code, how would you work around it? (*Hint:* See the previous question.)

    ```js
    var window = '';
    var document = 0;
    var undefined = true;
    ```

    Building upon the concept from the previous question, in order to protect against the overwriting of otherwise reliably available variables, we have to pass them back into the scope of a closure, re-aliased to their correct values. Note that we're not actually passing in a value for `undefined` because the browser's concept of nothingness is what we want it to be re-aliased to. Since a third parameter is not specified, `undefined` now means what it should: Nothingness.

    ```js
    (function(window, document, undefined) {
      // Now window, document, and undefined
      // are back to their original meanings.
    })(this, this.document);
    ```

14. In one line of code, how you would make a copy of an array?

    Acceptable answers would include using the `slice()` method, or concatenating with an empty array. Calling `slice()` with no parameters simply returns a copy of the original array (rather than a reference to it, like the last example below). Concatenating the contents of the `old_array` to an empty array `[]` freshly populates the new array with the values from the old one.

    ```js
    var old_array = [1, 2, 3];

    // This works
    var new_array_1 = old_array.slice();

    // This works too
    var new_array_2 = [].concat(old_array);

    // This does NOT work, because any edits to new_array_3
    // will alter the original, old_array. NOT what we want!
    var new_array_3 = old_array;
    ```

15. What is the difference between `setTimeout` and `setInterval`? *Bonus:* What is the lowest cross-browser increment that each can accurately use?

    Using `setTimeout` calls a function after a certain amount of time has elapsed. Using `setInterval` calls the function continuously, each time a specified duration has passed.

    ```js
    // In milliseconds
    var five_seconds = 5000;

    function call_me(str) {
      console.log('I was called from ' + str);
    }

    // This runs once, after 5 seconds
    setTimeout(function() {
      call_me('setTimeout');
    }, five_seconds);

    // This runs every 5 seconds
    setInterval(function() {
      call_me('setInterval');
    }, five_seconds);
    ```

    *Bonus:* The lowest increment that can be used reliably across various browsers is `15.6` milliseconds. This is due to an idiosyncrasy in Windows. More on that here&hellip;

    http://www.nczonline.net/blog/2011/12/14/timer-resolution-in-browsers

16. Explain how `delete` works. What types of things cannot be deleted?

    **Answer:**

    Using `delete` will destroy variables and properties, making them `undefined` when you try to access them. Things that cannot be deleted include properties of objects created from a prototype (but you can delete properties of the prototype itself). Additionally, if you call `delete` on an item in an array, the array's `.length` is unaffected.

    ```js
    //
    // Prototype example
    //

    function Automobile() {}
    Automobile.prototype.wheels = 4;

    var my_car = new Automobile();

    // Outputs 4
    delete my_car.wheels;
    console.log(my_car.wheels);

    // Outputs undefined
    delete Automobile.prototype.wheels;
    console.log(my_car.wheels);

    //
    // Array example
    //

    var my_array = ['zero', 'one', 'two'];

    // Outputs 3
    console.log(my_array.length);

    // Outputs 'one'
    console.log(my_array[1]);

    delete my_array[1];

    // Outputs undefined
    console.log(my_array[1]);

    // Outputs 3
    console.log(my_array.length);
    ```

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

    **Answer:**

    While you would typically use a library for DOM events, it's worth understanding how this works. Essentially, event delegation involves attaching an event listener to a higher-level element, and then determining if the event took place atop one of its children elements. The ability to watch for these events firing upwards to their parent is called "event bubbling." Here's how it would work&hellip;

    ```js
    function handle_special_clicks(ev) {
      var tag = ev.target.tagName.toLowerCase();

      if (tag === 'a') {
        // Don't follow the link
        ev.preventDefault();

        console.log('You clicked a special link!')
      }
    }

    (function(d) {
      var special = d.getElementById('special');

      // For modern browsers
      if (special.addEventListener) {
        special.addEventListener('click', handle_special_clicks, false);
      }
      // For older versions of IE
      else if (special.attachEvent) {
        special.attachEvent('click', handle_special_clicks);
      }
    })(this.document);
    ```

18. What does this snippet of code do?

    ```js
    var foo = bar ? bar : 0;
    ```

    **Answer:**

    This is called a *ternary* and is shorthand for a quick if/else statement. That could be written out more verbosely as&hellip;

    ```js
    var foo; // undefined

    if (bar) {
      foo = bar;
    }
    else {
      foo = 0;
    }
    ```

19. When might you write something like this, and what is it shorthand for?

    ```js
    foo && foo.bar();
    ```

    **Answer:**

    This is sometimes referred to as "short circuiting" a logical operator. You can think of it as a ternary with no `else` condition. Basically, the part before `&&` is evaluated, and if it is "truthy" (in this case, ensuring the existence of `foo`), the part after the `&&` is evaluated. Since `foo.bar()` is a function, it is executed.

    This could be written out more verbosely as&hellip;

    ```js
    if (foo) {
      foo.bar();
    }
    ```

    This is helpful when logging things to the `console`, which may not be present and available in every browser. For testing purposes, it can be useful to have a `log` function, which proxies for `console.log`&hellip;

    ```js
    // This allows you to log things, if console
    // is available, but takes no action, if not.
    function log() {
      console && console.log(arguments);
    }

    // Use like this
    log(1, 2, 3, 4, 5);
    ```

20. How do `parseInt` and `parseFloat` differ? When would you use a number's `toFixed()` method? In what instance might the following code snippet actually make sense to use?

    ```js
    var my_number = my_string - 0;
    ```

    **Answer:**

    The `parseInt` function will take a number or string, and convert it into a whole number. This is not the same as `Math.round()`, because it simply removes everything after a decimal point. It will also remove any string values that follow a number.

    The `parseFloat` function will convert any number or string into a decimal representation, also culling any string values that follow. Also, `parseInt` requires a "radix" (usually `10`) to be passed in as the second parameter. Otherwise, values such as `09` change to `0` instead of `9`.

    Using `parseFloat` alone will not retain (nor add) a certain number decimal points. For instance, `'1.50'` (a string representing one dollar and fifty cents) would simply become `1.5`. To ensure a string representation of the correct number of decimal points, `toFixed()` must be used.

    ```js
    var radix = 10;

    // Equals 1
    parseInt('1.5', radix);

    // Equals 1
    parseInt('1.5 Hello World!', radix);

    // Equals NaN (not a number)
    parseInt('Hello World! 1.5', radix);

    // Equals 1.5
    parseFloat('1.50');

    // Equals '1.50'
    parseFloat('1.5000').toFixed(2);
    ```

    Occasionally, you may want to check to ensure that a user really has typed in a real number, and not one that consists of numbers *and* non-numeric characters. You could write a regular expression, but a simple way to check is to subtract zero. If this yields `NaN`, you know the user didn't enter what can be considered a "real" number.

    ```js
    // Assuming this is what a user typed...
    // <input id="amount" name="amount" value="1.50 ABC" /> dollars

    (function(d) {
      var value = d.getElementById('amount').value - 0;

      // Is it not a number?
      if (isNaN(value)) {
        // Tell the user:
        // "You must enter a value number"
      }
      else {
        // Process the value
      }
    })(this.document);
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

    **Answer:**

    To handle an arbitrary number of parameters passed into a function, JavaScript gives us the handy, built-in variable called `arguments`. Here, we can use `parseFloat`, to ensure we filter out any non-numeric values that might be passed in, while still allowing string representations of numbers to be converted. Also, values are multiplied by `10`, totaled, then divided by `10`, to account for any decimal oddities due to floating-point arithmetic.

    ```js
    function sum() {
      // Start from zero
      var total = 0;

      // Floating-points, bah!
      var ten = 10;

      // Undefined, set in the loop
      var value;

      // Something to iterate on
      var i = arguments.length;

      // Loop through all the parameters
      while (i--) {
        // Multiply by 10, to account for peculiarities
        // of doing addition with floating-point numbers.
        value = parseFloat(arguments[i]) * ten;

        // Is it not, not a number?
        // Then hey, it's a number!
        if (!isNaN(value)) {
          total += value;
        }
      }

      // Divide back by 10, because we multiplied by
      // 10 to account for floating-point weirdness.
      return total/ten;
    }
    ```
