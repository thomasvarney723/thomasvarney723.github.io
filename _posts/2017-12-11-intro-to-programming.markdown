---
layout: post
title:  "An introduction to programming using the nicest language I know"
date:   2017-12-11 22:44:00 -0600
categories: jekyll update
---

{% include klipse.html %}

In this short tutorial, we’ll cover the minimal knowledge necessary to begin writing programs. As it turns out programming is a lot like math.

Wait! Don’t leave just yet! Fortunately, programming is nothing like the math classes you’ve likely been subjected to in school.

Programming differs from math in two important ways. Firstly, when writing programs you’re always accompanied by a partner. As with any good group-work the division of labor in this relationship is rather lopsided. Your partner in this case is, of course, the computer. While being far more rational than you (someone had to say it), the computer can’t think for itself and will do virtually anything you ask it to. Its toil frees you from solving for x for the zillionth time in a cramped chair and desk. Delegating the task of evaluation turns an otherwise dry task into a creative one.

Secondly, and most importantly, programming languages have collections! Most math curriculum through high school deals almost exclusively with scalar types. That is every value, or placeholder for a value, in an expression is indivisible. 4 is a scalar value as is 273. Numbers, in this case, and their accompanied operations like addition are frequently insufficient for all but the most boring of programs. Collections in a programming language allow us to do more by wrapping many values together into one value and manipulating it irrespective of what’s inside.

You may already know that a program is just a series of smaller procedures specified in a particular order. Let’s say you want to write a series of steps to sort a collection of numbers. One possible solution might go something like this: 

1. Take the first number in the unsorted collection and place the remaining numbers into one of two groups on either side. Lesser numbers go in the group to the left, greater numbers to the right. 
2. Repeat this procedure on both of the new groups until they are empty. 
3. Finally, from left to right, concatenate (string together into a collection) all the numbers back into one group in their new order.

Treating the numbers as a collection allows us to easily express a procedure to sort it. Notice that terms like ‘first’, ‘left’, ‘right’ and ‘concatenate’ are operations appropriate for collections just as arithmetic is for numbers.

While the steps above make for a perfectly reasonable program, English might as well be Greek to your servile pal the computer. We’ll need to write our program in terms even it can understand. This is where a programming language comes in.
The language we’ll be using is a simple one comprised of only three things: functions, data and application. We’ve already mentioned numbers and collections, they fall into the category of data. Data is static and there is little more to it than what you see. Functions, little programs in their own right, are the doers that make a program worth writing at all. In our english program ‘first’, ‘left’, ‘right’ and ‘concatenate’ acted as functions.

Application is how we combine functions and data to build new forms. If functions were verbs and data nouns, application would be how we form sentences. Application is expressed with a grouping of parenthesis in which the first element is always a function and any subsequent elements are inputs to the function. Let’s multiply some numbers.

<pre><code class="language-klipse">
(* 3 -4.9 5/7)
</code></pre>

In the more familiar mathematical syntax this is equivalent to ‘3 x -4.9 x 5/7’.  All the code in this tutorial is editable and the computer’s output from each snippet is displayed just below it. Try swapping one of the inputs for false. Because false has no meaning in the context of addition the computer will complain loudly.

Chaining computations can be achieved by nesting expressions and this can be done to any depth.

<pre><code class="language-klipse">
(/ 2 (- 3 5 (+ 1 2) -10))
</code></pre>

This is equivalent to ‘(3 - 5  - (1 + 2) - -10) / 2’.

Now what about those collections I promised you? Vectors, one type of collection, are notated with square brackets instead of parens. Vectors too can be nested to any depth. [\$ "Hickey" > [99999999 true]] is a vector of four items. Vectors can contain a mix of different types; in this case: a character, string, function and another vector containing an integer and a boolean. Also note that ordering matters.

<pre><code class="language-klipse">
(= [\$ "Hickey" > [99999999 true]] 
   ["Hickey" [99999999 true] \$ >])
</code></pre>

Put the elements of the two vectors in the same order and you'll see the computer will see them as equal.

Vectors have functions appropriate for their type just as numbers do.

<pre><code class="language-klipse">
(conj [3 2 1] "go")
</code></pre>

<pre><code class="language-klipse">
(nth [3 2 1] 1)
</code></pre>

<pre><code class="language-klipse">
(first [3 2 1])
</code></pre>

<pre><code class="language-klipse">
(last [3 2 1])
</code></pre>

<pre><code class="language-klipse">
(rest [3 2 1])
</code></pre>

<pre><code class="language-klipse">
(butlast [3 2 1])
</code></pre>

Sometimes when the output is a vector, it will be shown with parens instead of square brackets as in the examples containing rest and butlast. Don’t worry about this for now.

Built-in functions, scalar data and collections of data are all well and good but what’s the point of writing an expression that returns the same result every time? We could just as easily write the output instead of the expression. There isn’t a point. To do any useful work, we need to build our own functions that can return a different output depending on the input.

</br>

Let’s say you want the ability to test whether a number is less than 6. Testing 17 could be written like (< 17 6). To make this more general so we can apply it to any number, we first insert a variable name where we would like the input to our function to be substituted. You can choose any name you like for the variable. Then wrap the list in the fn function and place your variable name in a vector as the first input to fn. 

<pre><code class="language-klipse">
(fn [a-number] 
  (< a-number 6))
</code></pre>

Delimiters such as parens and square brackets must be balanced for code to be valid. Indentation has no meaning in this language but it can be used to make grouping more obvious. We can now use our new function just as we would a built-in like +.

<pre><code class="language-klipse">
((fn [a-number] (< a-number 6))
  17)
</code></pre>

This works but is cumbersome. If we intend to use this same function in more than one place in our program it’s helpful to bind the definition to a name so that we may refer to it again.

<pre><code class="language-klipse">
(def less-than-6? 
  (fn [cool-number] (< cool-number 6)))
</code></pre>

<pre><code class="language-klipse">
(less-than-6? 17)
</code></pre>

That’s more like it!

You may want to do more with your function by allowing another input or two. You can add as many variables as you like and refer to them as many times as you like in the body of the function. Simply include each name in the vector of inputs.

<pre><code class="language-klipse">
(def less-than? 
  (fn [tester one-testee two-testee] 
    (< tester one-testee two-testee))))
</code></pre>

<pre><code class="language-klipse">
(less-than? 17 6 11)
</code></pre>

You may have noticed that our less-than? function doesn’t do anything the built in < doesn’t. Our function would be simpler if we merely applied the function < to our data. Although we typically do this with parens Clojure gives us an apply function as well. The following is similar to our last definition of less-than?’

<pre><code class="language-klipse">
(def less-than? 
  (fn [coll] 
    (apply < coll))))
</code></pre>

It may be helpful to think of every expression as an application of apply, a function and a collection of input. In fact, this is actually what’s going on under the hood when the computer evaluates your code.

(apply a-function [input0 input1 input2 input3 ...])

You’ll notice that if we now call less-than? with 17 6 and 11 as we did previously we’ll receive some sort of error from the computer about using the wrong number of arguments.  Now we must wrap our numbers in a vector when calling less-than? on it. This has two consequences. On the plus side we can now test any amount of numbers by including them in our vector. However, imagine if less-than? were a component in a larger program. By expecting a collection of potentially many numbers instead of exactly three numbers we’ve introduced a bug anywhere less-than? is invoked. Fortunately we can have our cake and eat it too.  

<pre><code class="language-klipse">
(def less-than? 
  (fn [& numbers] 
    (apply < numbers))))
</code></pre>

The & in the function definition means that it can accept any number of arguments and they will be put into a collection that can be referred to as numbers.

<pre><code class="language-klipse">
(less-than? 17 6 11)
</code></pre>

All that for a function that is no better than <... Now that we know how to define functions, let’s get back to sorting!

As test data for our sorting function, let’s use [6 5 8 11 3 2 7 9 4 1 10 12].
For convenience sake while developing we can bind this to a name.

<pre><code class="language-klipse">
(def numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

Our english program says to take the first item in this collection. Easy enough.

<pre><code class="language-klipse">
(first numbers)
</code></pre>

Those to be placed on either side can be selected with rest.

<pre><code class="language-klipse">
(rest numbers)
</code></pre>

Splitting the rest of the elements in our collection into the lesser and greater groups is probably the trickiest part of this whole program. We could go to the trouble of writing a bespoke function that does this for us but I think you’ll find that filterv does just what we’re looking for.

<pre><code class="language-klipse">
(def lesser-numbers
  (fn [coll]
    (filterv (fn [another]
    	      (< another (first coll)))
            (rest coll)))

(lesser-numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

filterv takes a function and a collection and returns only the elements of that collection which return true when applied to the function. Here we’ve selected the elements that are less than the first number in the collection. If you repeatedly take the output of this expression and pass it back into the same function you’ll begin to see the far left branch of our evaluation tree. Though you can do this by hand it can also be demonstrated directly in the language.

<pre><code class="language-klipse">
(take-while not-empty
            (iterate lesser-numbers
                     [6 5 8 11 3 2 7 9 4 1 10 12]))
</code></pre>
 
We’ll need this repeating behavior in our program.

Testing ideas like this by giving the computer snippets of code and examining the return value is akin to having a conversation with the computer in which you can bounce ideas off it (“Do these pants go with my shoes?”). Delegating the work of evaluating your code leaves you free to focus on expressing the logic your program requires.

To collect elements which go in the right-side group we need only to select the elements which didn’t make the cut for the left-side group. We can do this in the same way but slip not into the function we pass to filter.

<pre><code class="language-klipse">
((fn [coll]
  (filter (fn [another]
	    (not (< another (first coll))))
          (rest coll)))
 numbers)
</code></pre>

The repeating aspect of our sorting function will be accomplished by simply applying our sorting function again to each of our left and right groups. Defining a function in terms of itself? What a concept!

Because concatenation is done only once at the end of our sorting function, we’ll wrap concat around the body of our function so that all the recursions take place before the concatenation. Also, the first element that we used to compare to the rest of our elements will need to be concatenated between the left and right groups. It must be placed in a vector because concat only operates on collections. Try concat with a naked scalar type and you’ll see it throws an error.

<pre><code class="language-klipse">
(concat [1 2 3] 4 [5 6 7])
</code></pre>

<pre><code class="language-klipse">
(def sort-numbers
  (fn [coll]
    (concat
      (sort-numbers 
         (filter (fn [another]
                   (< another (first coll)))
                 (rest coll)))
      [(first classmates)]
      (sort-numbers 
         (filter (fn [another]
                   (not (< another (first coll))))
                 (rest coll))))))

#_(sort-numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

We’re almost there! If you now apply sort-numbers to our test data by uncommenting the last line, you’ll receive some sort of stack overflow error. This is because there is nothing that stops the recursion from terminating. At the two places where we call sort-numbers, our function goes around and around. It’s for this reason (take-while not-empty ... was needed in the example showing the left evaluation branch. We need evaluation to stop when some criteria is met. According to our english program the terminating condition is when the collection no longer has anything in it. if is a supremely useful function that will enable us to insert this check. if takes three inputs: a test, an output if the test evaluates to true and an output if the test evaluates to false. Our test for an empty collection can be written simply as (= [] coll) and the false branch of our if function will contain the logic we've already covered.

<pre><code class="language-klipse">
(def sort-numbers
  (fn [coll]
    (if (= [] coll)
        []
        (concat
          (sort-numbers 
            (filter (fn [another]
                      (< another (first coll)))
                    (rest coll)))
          [(first numbers)]
          (sort-numbers
            (filter (fn [another]
                      (not (< another (first coll))))
                    (rest coll)))))))
</code></pre>

Returning an empty vector in the case that our collection is empty works because concat-ing any collection with an empty collection returns the same collection. Another way to think about this is that we are going to recurse until we get to a collection that we know to be sorted - an empty one.

<pre><code class="language-klipse">
(sort-numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

As it turns out, the algorithm we’ve just implemented is known as Quicksort, one of many different sorting algorithms. What did you expect for your first program, a general purpose artificial intelligence? Surely, a sorting function is a necessary component so you’re part-way there!

The language we’ve been using is known as ClojureScript and it’s the nicest language I know because of its simplicity. It has far fewer syntax and semantics than most all of the numerous other programming languages in existence. This raw simplicity puts a minimal amount of distance between you and the logic you intend to express.

ClojureScript is a variant of Clojure and designed to run in a web browser. The code we’ve explored here works in both languages. If you’re interested in playing more with Clojure. a cheatsheet of built-in functions can be found at https://clojure.org/api/cheatsheet. Head over to repl.it for a Clojure environment with a scratch area. 4Clojure and clojurekoans offer little puzzles to cut your teeth on.

Although a programming language is necessary for developing a program which runs on a computer, it’s important to realize that any language will do and that thinking precisely and procedurally is the key. Clojure is the nicest language I know because of how little it gets in your way. Both its syntax and semantics are far smaller and simpler than most every other programming language. This puts a minimal amount of distance between you and the logic you intend to express.

At this point you know nearly everything required to write a program of any magnitude in Clojure. Although Clojure isn’t always a good fit for every application, any software you can think of, be it an operating system, webpage, pacemaker or sorting program, is merely a group of smaller functions composed to synthesize a new function. In fact, most of Clojure’s built-in functions are themselves comprised of yet more primitive functions. Their difference is not a fundamental one but a matter of degree.

Some of the information in this post may only be approximately true but further refinements will have to be left for another time.

Happy computing!