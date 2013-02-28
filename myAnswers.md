## Intro Questions

01. <strong>When might comparative type coercion occur? How would you avoid it? How would you change a "falsy" or "truthy" value into a real boolean?</strong><br />
When using functions like indexOf, search, comparing undefined objects, etc.  I avoid it buy using strict comparison operators (=== !==) false == 0 (true) false === 0 (false). Changing from truthy/falsy is as simple as using the double not,  !undefined == true, !!undefined == false 

02. <strong>Describe how variable scope works. Explain how to create a closure using a self-executing anonymous function (also called IIFE: immediately-invoked function expression).</strong><br />Variable scope is dependent on where it is declared and how it is declared.  

    ```js
    var x = 1;
    var y = 'a';
    
    var obj = {
        x: 2,
        y: 'b',
        foo: function() {
            var x = 3;
            
            console.log( x, this.x, window.x); // 3 2 1
            console.log( y, this.y); // a b 
        }
    }
    ```

03. <strong>Explain briefly how prototypal inheritance differs from class-based, "classical" inheritance.</strong><br />Prototypal inheritance can change on the fly (polymorphism) so if the parent object is changed, so will the descendent objects. Also when 'searching' for a property on an object, all ancestors are examined as well for said reason.  Classical inheritance is bound to the state of the parent when created and only the object is examined (data is 'copied' to descendent classe).

04. <strong>Describe how the "module pattern" works. Explain how the "revealing module pattern" expands upon it.</strong><br />

05. <strong>How does a client-side MVC (or MVVM) approach work? What is your preferred MV* JS framework?</strong><br />MVC (Model View Controller) works by separating the data, display and handling into 3 separate parts.  Client side MVC works just like the back end, but instead of the model being (generally) a database result set, its a json object returned by the server.  Ember.js is currently my MVC of choice.

## Additional Questions

06. <strong>Why do these yield different results?</strong><br />

    ```js
    '1' + 2 +  3 ; // Equals '123'
     3  + 2 + '1'; // Equals '51'
     3  + 2 +  1 ; // Equals 6
    ```
Because javascripts loose typed nature and the order in which it process things.  '1'+2+3 reads as string '1'+2 = '12'+3 = '123', 3 + 2 = 5 + '1' = '51'

07. <strong>Why is `0.3` *not* the result of the following addition? How do you work around this peculiarity?</strong><br />

    ```js
    0.1 + 0.2; // Equals 0.30000000000000004
    ```
This is because of javascripts floating point precision.  To fix: 
    ```js
    Math.floor((.1 + .2)*10)/10 // Depending on the accuracy you are looking for, 10, 100, 100... 100000000
    ```

08. <strong>Describe how variable hoisting works, and how to avoid bugs that may arise from it.</strong><br />

09. <strong>How do these differ?</strong><br />

    ```js
    function foo() {}

    // versus

    var foo = function() {};
    ```

10. <strong>When might you use a function's `call()` method, or its `apply()` method?</strong><br />
When ever you need to pass context to a function.  

    ```js
      setTimeout(function(a,b){ ... do something within this object ... }.call(this, var1, var2), 1000);      
    ```

11. <strong>Explain how to determine if a variable is an array or an object. (*Hint:* `typeof` lies!)</strong><br />
Using the Object.prototype.toString and passing in the variable as the context.

    ```js
    var x = [0]; 
    Object.prototype.toString.call(x) === "[Object Array]" // true
    ```
    
12. <strong>In the following example, what is foo aliased to? (*Hint:* It is what `this` means.)</strong><br />

    ```js
    (function(foo) {
      // What is 'foo' aliased to?
    })(this);
    ```
`window`

13. <strong>In JavaScript (and the DOM), some global variables are actually mutable, such as: `window`, `document`, and `undefined`. How would you write code to ensure these were predictably available for use? Assuming someone had injected this code, how would you work around it? (*Hint:* See the previous question.)</strong><br />

    ```js
    var window = '';
    var document = 0;
    var undefined = true;
    ```

14. <strong>In one line of code, how you would make a copy of an array?</strong><br />

    ```js
    var x = [1,2,3,4,5]
    var y = Array.prototype.slice.call(x)
    y.push( 6 );
    console.log( x, y );
    ```

15. <strong>What is the difference between `setInterval` and `setTimeout`? *Bonus:* What is the lowest cross-browser increment that each can accurately use?</strong><br />`setInterval` is an on going timer, use clearInterval to stop it.  `setTimeout` is a one and done timer, use `clearTimeout` to cancel it before it has run

16. <strong>Explain how `delete` works. What types of things cannot be deleted?</strong><br />

17. <strong>Describe how event delegation works, and when you should use it to handle UI interaction. Example markup&hellip;</strong><br />

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
Event delegation works by assigning one click event to a containing element and then using the event.target attribute to determine which element was actually clicked.  Best use case would to minimize code and events when grouped items preform similiar or identical actions.

18. <strong>What does this snippet of code do?</strong><br />

    ```js
    var foo = bar ? bar : 0;
    ```
Ternary if statment.  if bar is true, defined, etc use bar's value, else 0

19. <strong>When might you write something like this, and what is it shorthand for?</strong><br />

    ```js
    foo && foo.bar();
    ```
quickly checks if foo exists before calling a function on a potentially undefined object

20. <strong>How do `parseInt` and `parseFloat` differ? When would you use a number's `toFixed()` method? In what instance might the following code snippet actually make sense to use?</strong><br />

    ```js
    var my_number = my_string - 0;
    ```
`parseInt` parses a string to an interger value (no decimal) and `parseFloat` parses a string to a floating point value (decimal).  You would want to use `toFixed()` for displaying the a value (monetary?) to the user, especially since it returns a string.  You can use the example to quickly convert a string to an number.

21. <strong>Write a function named `sum` that returns the total of any number of parameters. Example&hellip;</strong><br />

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

    ```js
    function sum() {
        var argLength = arguments.length,
            total = 0,
            x;
        for ( x = 0; x < argLength; x++ ) {
            if ( arguments[x] && parseFloat( arguments[x] ) ) {
                total = Math.floor((total + parseFloat(arguments[x]))*1000)/1000;
            }
        }
        //document.write(total + "<br />");
        return total;
    }
    ```
