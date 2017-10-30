# Functions First

Ideas on teaching programming to beginners with functional javascript.

## Why Functional Programming?

![](https://cdn-images-1.medium.com/max/1600/1*AM83LP9sGGjIul3c5hIsWg.png)

In my case, I stumbled upon functional javascript when trying to answer some basic questions about difficulties I was facing in a project:
 - As my project got more complex, I started having a hard time understanding it and it diminished my motivation to work on it and increased my fear that something would break when changing anyhting. **I wanted to know if this was avoidable?**
 - It seemed that there were always hundreds of different ways to do the exact same thing even with the same programming language, but **I wondered if there was a "right way" or a least a "better way"? And I wondered about what would be the criteria that would make it right or better?**

For me, functional javascript and functional programming in general have provided exactly the answers that have satisfied me to these two questions and launched me into my journey into the functional programming world after 20 years developing software and being unaware that a different way to program existed.

### Dealing with Complexity

> Simplicity is prerequisite for reliability.
> Edsger W Dijkstra

Complexity and reliability are addressed in functional programming by breaking programs down into smaller components. Other programming styles also do this, but functional programming breaks programs into **functions** (particularly pure functions) and functions have very unique properties because of how simple they are, which end up providing:

 - **composability**: which means that the way to put together the smaller parts of your program doesn't add complexity by using [a simple way to put parts together as a whole](#a-simple-way-to-put-parts-together-as-a-whole)
 - **ease to reason about**: [a way to take into account what programmers need to have in their head](#a-way-to-take-into-account-what-programmers-need-to-have-in-their-head)

> #### What's a simple function example?
> ```
> const increment = x => x + 1
> ```
> This declares an `increment` function, which takes an argument `x` and returns `x + 1` in other words it adds the number `1` and `x` together and then returns the result. Let's break the syntax of this line down:
> ```
> const A_FUNCTION_NAME = A_FUNCTION_DEFINITION
> ```
> So what's on the left of the `=` sign is the name of the function, in our case `increment` and what's on it's right is its definition. Let's further break down the function definition
> ```
> const A_FUNCTION_NAME = FUNCTION_ARGUMENT(S) => FUNCTION_RETURNED_RESULT
> ```
> So now we're focusing on the left side of the `=` sign, which has two things on each side of the `=>` arrow sign. What's on the left of the `=>` is the function's argument, in our case `x` (there can also be several arguments which we will see later), and what's on the right of the `=>` arrow is what the function returns, in this case it adds `x` (which is the function's argument) with `1`.
> So to recap, you can think of a function as a little software machine, which takes things on it's right and then returns things on its left. Our `increment` function takes anything as an input on its right and calls it `x` then it adds what we passed to it as `x`, adds `1` to it, and returns that as an output.
> Ok so now let's do exactly that with the `increment` function. Let's pass it a few numbers and see what happens.
> Our little machine can be fed some input, which in programming is said "calling the function" or "passing some arguments to a function" with the following syntax:
> ```
> increment(1) 
> // returns 2
> ```
> We use the name of the `increment` function and add parenthesis after it, then inside the parenthesis we put the input. This calls the function and returns `2` in this case.
> or
> ```
> increment(99) 
> // returns 100
> ```
> Simple enough? Let me know if anything is unclear by [asking a question!](https://github.com/iilab/functions-first/issues/new?labels=question)

### The Reusable Way

When going down this path, a strong gut feeling for what is accidental complexity (that you can get rid of) as opposed to intrisic complexity (the complexity of the problem you're solving) starts developing and it helps make sense and find the essential parts behind the hundred possible ways to solve a problem. In fact, thinking about software this way starts delivering on **reusability** in 2 main areas:
 - **thinking reuse**: to me this is the most important. You start recognising the same intrisic problem much more, and then ways in which different intrisic problems compose together, and this makes you not just a better functional programmer, but a programmer who can see these patterns even in non functional code. Then you'll start seeing that a lot of the most expert programmers out there, specifically the ones writing libraries or frameworks for other programmers, very often have a functional background or at least understand these issues very well. 
 - **code reuse**: since functions behave in a well known fashion and that composing them together also behaves in a well known fashion, then the building blocks you create using these compositions of functions are also well behaved and some of these functions, particularly higher-order functions, will deal with abstract problems that can effectively be reused in other programs. Even better, at some point these abstract problems start taking the shape of the most exciting branch of mathematics, category theory. What that means is that as you progress as a programmer on this path, you'll start to engage with a branch of math where experts discuss fascinating topics such as "Was category theory discovered?" or in other words, is it a pre-existing thing that is in the universe that we find out there and learn about rather than a human made thing? Or is it something which is a feature of the human mind? A pre-existing thing that is in our consciousness, a feature of how we break things down to better understand them, that we find in here and also discover but in our own minds?

> #### An example of very reusable function.
> Imagine you're given some bag of numbers and you'd like to increment all the numbers in the bag.
> A example of such a bag in Javascript is an Array which you write like this: `[1,2,3]` this bag contains the numbers 1, 2 and 3.
> What we'd like to do is apply the `increment` function to all the numbers in the bag, and get a new bag with the incremented numbers.
> You can do this as simply as this:
> ```
> [1,2,3].map(increment) 
> // returns [2,3,4]
> ```
> What this means is exactly what I wrote earlier: **apply the increment function to each element of the Array and return the result**. So that what `map` does. It **applies __any__ function to each element of __a bag-like thing__ and returns the result**. In our case we specifically `map` the `increment` function to the `[1,2,3]` Array (which is a bag-like thing).
> If you've programmed before then this might start feeling alien, so welcome to starting to unlearn things :) If this feels like it makes sense then welcome to one of the most used and useful pattern in programming. In fact `map` (and its sibling `reduce`) are at the heart of what runs the Google search engine. [No kidding](https://en.wikipedia.org/wiki/MapReduce#Uses).
> Let me know if anything is unclear by [asking a question!](https://github.com/iilab/functions-first/issues/new?labels=question)

Unlearning what I knew of programming and allow myself to be a beginner of functional programming has made me a better programmer, I think in many ways a better systems thinker as well and a happier and more enthusiastic software engineer.

For beginners in programming, the motivation is different than for experienced developers. Learning functional programming for experienced developers is often an experience of unlearning previously hardly acquired know-how, so it makes sense to consider starting to program with a functional approach and bypass the unlearning experience altogether.

### A simple way to put parts together as a whole

> #### Incrementing Twice by Composition 
> What if we often increment numbers twice in a row? Of course, you could notice that incrementing twice is basically adding `2` and you could write a function that does exactly that. But let's say we'd like to instead apply the increment function twice, how would we proceed?
> Well the intuition that helps me think about this is to picture that we need to put our little software machines back to back. Feed a number in the first one, get the output, then feed the output to the next one and get the output of that. And that's exactly what **function composition** does! Perfect now hopefully the syntax for this will also be crystal clear... Well... Sorry there's a twist, or let's call it a historical artifact that I should explain before moving forward since it's pervasive in functional programming. Here's how its frequently done:
> ```
> increment(increment(2))
> ```
> Ok, so it might look innocuous at first sight, but the metaphor of software machines with things coming in the right and going out the left is not very visually adequate since the `2` is added to the left. In other languages, there are alternative styles of writing this, which mean that the visual metaphor holds better. In effect (this is not real code) it looks like `2#increment#increment`.
> Ok so now, we'd like to avoid having to write this and create a sligthly larger software machine which takes a number and returns the twice incremented result. We'll call this `incTwice`. We can declare `incTwice` like this:
> ```
> const incTwice = x => increment(increment(x))
> ```
> Simple enough! And that's a simple example of function composition for you, where we reused the `increment` smaller function to create another one `incTwice` which we now can call in the usual way:
> ```
> incTwice(1)
> // returns 3
> ```

Composition is the universal glue out of which functional programs are created. As long as the parts are functions, then the glue holds very well and does exactly what's expected with no surprises (yes, you've guessed it, there are cases where your glue won't hold and we'll talk about this in a **pure functions** section). You can keep building larger programs out of smaller ones, and you can unglue and reglue parts all day long. In fact, that's one of the most amazing aspects of building programs with function composition, they are much much easier to reorganise if new needs arise, or if you think of a better way to glue things together or make your functions more reusable.  That's called **refactoring**, which is reorganising programs without changing what the overall program does, but usually to immprove its overall structure.

### A way to take into account what programmers need to have in their head

In other programming approaches, as programs grow, the programmer often needs to have increasing amounts of information in their head in order to keep understanding the program. 

The major contributor to this, and the most frequent source of bugs, is the state of your application. If an increasing number of your program's parts can modify your application's state (including some parts that are written by colleagues), then you need to keep all these as possibilities in your head to 

> #### Example
> ```
> exampleCode()
> ```

## What next?

Sounds interesting and you're based in Berlin, then why not join our Berlin meetup and learn more? Otherwise take a look at some resources 

## Resources

> TODO: Find resources that are accessible for beginners in programming.

### Videos

Beginner:

Advanced:

[![](https://img.youtube.com/vi/-6BsiVyC1kM/0.jpg)](https://www.youtube.com/watch?v=-6BsiVyC1kM)

### Articles

Beginner:

Intermediate:
  - https://medium.com/@lunde.andrews/easing-into-functional-programming-in-javascript-30056bcc49a9

Advanced:
  - https://bethallchurch.github.io/JavaScript-and-Functional-Programming/
  - https://medium.com/@drboolean/free-er-monads-in-js-f5a59e7abc82

### Books

Beginner:

Advanced:
  - https://www.gitbook.com/book/drboolean/mostly-adequate-guide/details 
