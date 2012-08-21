# JavaScript Quiz

Note: The intent of this quiz isn't to be a brain-buster. It is meant for recruiters to present to front-end developer candidates. The intent to weed out some "Just use jQuery" applicants, but allow those that know JavaScript to pass fairly easily.

## Intro Questions

01. When might comparative type coercion occur? How would you avoid it? How would you change a "falsy" or "truthy" value into a real boolean?

02. Describe how variable scope works. Explain how to create a closure using a self-executing anonymous function (also called IIFE: immediately-invoked function expression).

03. Explain briefly how prototypical inheritance differs from class-based, "classical" inheritance.

04. Describe how the "module pattern" works. Explain how the "revealing module pattern" expands upon it.

05. How does a client-side MVC (or MVVM) approach work? What is your preferred MV* JS framework?

## Additional Questions

06. Why do these yield different results?

        "1" + 2 +  3 ; // Equals "123"
         3  + 2 + "1"; // Equals "51"
         3  + 2 +  1 ; // Equals 6

07. Why isn't `0.3` the result of the following addition? How do you work around this issue?

        0.1 + 0.2; // Equals 0.30000000000000004

08. Describe how variable hoisting works, and how to avoid bugs that arise from it.

09. How do these differ?

        function foo(){}

        // versus

        var foo = function(){};

10. When would you use a function's `call()` method? &mdash; When would you use a function's `apply()` method?

11. Explan how to check if a variable is an array.

12. In the following example, what is foo aliased to? (Hint: It is what `this` means.)

        (function(foo) {
          // What is 'foo' aliased to?
        })(this);

13. In JavaScript (and the DOM), variables we consider universal are actually mutable: e.g. `window`, `document`, and `undefined`. How would you write code to ensure these were predictably available for use? Meaning, assuming someone had injected this code, how would you work around it? (Hint: See the previous question.)

        var window = '';
        var document = 0;
        var undefined = true;

14. In one line of code, how you would make a copy of an array?

15. What is the difference between `setInterval` and `setTimeout`? &mdash; Bonus: What is the lowest cross-browser increment that each can accurately use?

16. Explain how `delete` works. What types of things cannot be deleted?

17. Describe how event delegation works, and when you should use it to handle UI interaction.

18. What does this snippet of code do?

        var foo = bar ? bar : 0;

19. When might you write something like this, and what is it shorthand for?

        foo && foo.bar();

20. How do `parseInt` and `parseFloat` differ? When would you use a number's `toFixed()` method? &mdash; In what instance might the following code snippet actually make sense to use?

        var my_number = my_string - 0;