# Tips to Learning Recursion

Recursion is something that can take a long time to wrap your head around. In a simple problem of producing all permutations of a set, I wanted to explore why you can or cannot do certain things and why.

Here are some questions I had when learning about recursion:

## When do you use recursion vs. a `while` or `for` loop?

You can almost always refactor to use whichever one you'd want - they're all different versions of the same thing.

[EXAMPLES HERE]

## When do you use or not use a subroutine?

You can always choose to do either. If your recursive function needs to build up and return something (as it does in the case of permutations), it often makes sense to create the results outside the closure of a subroutine, build it with the subroutine, and then return what you've built at the end of your function.

However, if you wanted to do this without a subroutine, you would just have to add the thing you're building as a parameter to the main function. Often choosing to do a subroutine or a not just depends on what you want to pass in to each recursive call as arguments.

[EXAMPLE HERE]

## Where do you need `return`?

While I was learning recursion, if my function wasn't working I would just start adding in `return` statements and guessing until I found what worked - in the base case, before the recursive call, etc.

Instead of guessing, think through (and pseudocode out!):
1. What does your function need to return overall?
2. If you're using a subroutine, what does your subroutine need to return? Anything, or does it just need to have side effects (like building up a results array) and not itself return anything.

Often if you need your recursive function to actually return the thing in your base case, you would need to add a return within each base case, _as well as_ before each recursive call. The latter is the one I would often forget and be stumpted by while trying to debug. If you base case is what that recursive call will turn into, you of course would need to return that recursive call as well, otherwise your result from the base case will not be preserved or saved in any way.

[EXAMPLE]

Another likely scenario is returning from your base cases a true or false, and then using that recursive call (which will therefore evaluate to true or false) to determine what you want the function as a whole to return.

[EXAMPLE]

And finally there's sometimes a hidden sneaky base case - one that goes after all the recursive calls. If you get through all the recursive calls and have yet to return (for example you didn't find the element you were looking for), you'll want to return after the last recursive call has completed. This will only run in the first call to your recursive function (can't work its way down because it's placed after those recursive calls).

[EXAMPLE]

## When do you pass parameters to your subroutine?

Often you can do either for things you are building up/storing. Anything you need to update with each run of your subroutine often makes sense to be a parameter (likely what your if statements for your base cases are checking for). However if you wanted to keep these things outside the scope of your subroutine, you can still use them inside your subroutine of course. Just be careful that however you manipulate them (pushing, adding, etc.) you will have to undo after the recursive call for any type of loop to work properly.

One advantage of putting immutable elements as parameters is that there will automatically be new copies made with each recursive call. Be careful when putting mutable elements (arrays or objects) as parameters without first copying them as there may be unintended consequences.

# Helpful questions to think through when debugging

1. Am I returning what I intended to return?
    - Are my base cases returning as they should be?
    - Am I putting a return before my recursive call?

2. Are there mutable arguments? Am I keeping track of the manipulations to them properly?
    - If you have loops inside your recursion, anything you do to mutable arguments you'll likely have to undo after the recursive call for your loop to function properly.

3. Have I thought through all the different base case options?

4. Within a recursive call, will it know when to stop?
    - Do your base cases stop after running? Either with an empty return statement, or because the recursive part is in an else block?
