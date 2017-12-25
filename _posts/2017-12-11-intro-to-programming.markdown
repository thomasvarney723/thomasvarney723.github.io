---
layout: post
title:  "An interactive introduction to programming with the world's nicest language"
date:   2017-12-11 22:44:00 -0600
categories:
---

<meta charset="utf-8">

In this short tutorial, we’ll cover the minimal knowledge necessary to begin writing programs. Programming is actually a lot like math.

Wait! Don’t leave just yet! Fortunately, it's nothing like the math classes you’ve likely been subjected to in school.

Programming differs from math in two important ways. Firstly, when writing programs you’re always accompanied by a partner. As with any good group-work the division of labor in this relationship is rather lopsided. Your partner in this case is, of course, the computer. While being far more rational than you (someone had to say it), the computer is too stupid to think for itself and will do virtually anything you ask it to. Its toil frees you from solving for x for the zillionth time in a cramped chair and desk. Delegating this task of evaluation to the computer turns an otherwise monotonous task into a creative one.

Secondly, and most importantly, programming languages have collections. Most math curricula in schools deal exclusively with scalar types. That is every value, or placeholder for a value, in an expression is a single value. 4 is a scalar value as is 273.45. Numbers, in this case, and their accompanied operations like addition  are frequently insufficient for all but the most boring of programs. Collections enable us to group many values together and manipulate them as one value.

You may already know that a program is just a group of smaller programs specified in a particular order. Let’s say you want to write a sequence of steps to sort a collection of numbers. One possible solution might go something like this: 

1. Take the first number in the collection and place the rest of the numbers into one of two collections on either side. Lesser numbers go in the group to the left, greater numbers to the right. 
2. Repeat step 1 again on both of the new collections unless they are empty. 
3. Finally, concatenate (string together into a collection) all the collections back into one group in their new order.

![Quicksort]({{ "/assets/quicksort.gif" | absolute_url }})

Treating the numbers as a collection allows us to easily express a procedure to sort it. Notice that terms like "first", "rest", "left", "right", "empty" and "concatenate" are operations appropriate for collections just as arithmetic is for numbers.

While the steps above make for a perfectly reasonable program, English might as well be Greek to your dim-witted pal the computer. We’ll need to write our program in terms even it can understand. This is where a programming language comes in.

<br>

The language we’ll be using is a simple one comprised of only three things: functions, data and application. We’ve already mentioned numbers and collections, they fall into the category of data. Data is static and there is no more to it than what you see. Functions are the opposite, they're the doers that make a program worth writing at all.

Application is how we combine functions and data to build new forms. If you think of functions as verbs and data as nouns, application is how we form sentences. Application is expressed with a grouping of parenthesis in which the first element is always a function and any subsequent elements are inputs to the function. At least one whitespace character must seperate each element. Let’s multiply some numbers.

<pre><code class="language-klipse">
(* 3 -4.9 11/7)
</code></pre>

In the more familiar mathematical syntax this is equivalent to "3 x -4.9 x 11/7".

Often we say that we "call" a function on some inputs or we "pass" some inputs to a function and are given back a "result" or "return value". Inputs to a function may also be called "arguments" or "parameters" to that function. Whatever the vernacular, it's always the case that we apply a function to zero or more inputs and the computer gives us back exactly one output.

All the code in this tutorial can be edited and the computer will reevaluate it. The output is displayed just below each code snippet. Try swapping one of the inputs for <code>"eight"</code> in the previous example. Because strings, as they're called, have no meaning in the context of addition the computer will complain loudly.

Chaining computations can be achieved by nesting expressions and this can be done to any depth. The output of each subexpression becomes the input to another.

<pre><code class="language-klipse">
(/ 2 (- 3 5 (+ 1 2) -10))
</code></pre>

Note that delimiters such as parens must always be balanced for code to be valid. The previous expression is equivalent to ‘2 / (3 - 5  - (1 + 2) - -10)’.

Now what about those collections? Vectors, one type of collection, are notated with square brackets instead of parens. Vectors too can be nested to any depth. <code>[\$ "Hickey" -> [cat true]]</code> is a vector of four items. Vectors can contain a mix of different types; in this case: a character, string, macro and another vector containing a function and a boolean. Also note that ordering matters.

<pre><code class="language-klipse">
(= [\$ "Hickey" -> [cat true]] 
   ["Hickey" [cat true] \$ ->])
</code></pre>

Put the elements of the two vectors in the same order and you'll see the computer will treat them as equal.

Vectors have functions relevant for the type of data they are.

<pre><code class="language-klipse">
(first [3 2 1])
</code></pre>

<pre><code class="language-klipse">
(rest [3 2 1])
</code></pre>

<pre><code class="language-klipse">
; Vectors' indicies begin at zero.
; Text after a semicolon to the end of the line is a comment.
; Comments aren't evaluated.

(nth [3 2 1] 1)
</code></pre>

<pre><code class="language-klipse">
(conj [3 2 1] "go!")
</code></pre>

<pre><code class="language-klipse">
(concat [5 4] [] [3 2 1] [0])
</code></pre>

Many functions return a vector written with parens instead of square brackets such as in the examples containing <code>rest</code> and <code>concat</code>. Don't worry about this apparent inconsistency for now.

Functions, data and application are all well and good but what’s the point of applying a function to data when we get the same result every time? We can just as easily write the result instead of the expression. There isn’t a point. To do any useful work, we need to build new functions.

<br>

Let’s say you want the ability to test whether a number is less than 6. Testing 17 can be written like <code>(< 17 6)</code>. To make this more general so we can apply it to any number, we first insert a variable name where we want the input to our function to be substituted. You can choose any name you like for the variable. Then wrap the expression in the <code>fn</code> function and place your variable name in a vector as the first argument to <code>fn</code>. 

<pre><code class="language-klipse">
(fn [a-number] 
  (< a-number 6))
</code></pre>

Note the use of a hyphen in place of a space in our variable name. Because whitespace is used to seperate elements, we must use something else in lieu of spaces. All whitespace characters are equivelant in this language so indentation has no meaning, however, it can be employed to make the structure of code more apparent.

We can now use our new function just as we can a built-in like <code>+</code>.

<pre><code class="language-klipse">
((fn [a-number]
   (< a-number 6))
 17)
</code></pre>

This works but is cumbersome. If we intend to use this same function in more than one place in our program it’s helpful to bind the definition to a name so that we may refer to it again.

<pre><code class="language-klipse">
(def less-than-6? 
  (fn [cool-number]
    (< cool-number 6)))

(less-than-6? 17)
</code></pre>

That’s more like it!

Making functions that take only one input may seem limiting. You can add as many variables as you like and refer to them as many times as you like. Simply include each name in the vector of inputs.

<pre><code class="language-klipse">
(def weird-fn 
  (fn [w x y z] 
    (< (- y) y x (* z z))))

(weird-fn -2 3 2 4)
</code></pre>

When defining a function, the order of variable names in the vector of inputs is the same order used when calling it. In the previous expression, <code>-2</code> will be substituted for (the absent) <code>w</code>, <code>3</code> will be substituted for <code>x</code>, <code>2</code> for <code>y</code> and <code>4</code> for <code>z</code>.

Now that we know how to define functions, let’s get back to sorting!

<br>

As test data for our sorting function, let’s use <code>[6 5 8 11 3 2 7 9 4 1 10 12]</code>.

Our english program says to take the first item in this collection. Easy enough.

<pre><code class="language-klipse">
(first [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

Those to be placed on either side can be selected with <code>rest</code>.

<pre><code class="language-klipse">
(rest [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

Splitting the rest of the elements in our collection into the lesser and greater groups is the trickiest part of the program. We can go to the trouble of writing a bespoke function that does this for us but I think you’ll find that <code>filterv</code> does just what we’re looking for.

<pre><code class="language-klipse">
(def lesser-numbers
  (fn [coll]
    (filterv (fn [x]
    	       (< x (first coll)))
             (rest coll))))

(lesser-numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

<code>filterv</code> takes a function and a collection and returns only the elements of that collection which return <code>true</code> when applied to the function. Here we’ve selected the elements that are less than the first number in the collection.

Notice how the function passed to <code>filterv</code> refers to  <code>coll</code>, the variable in the surrounding function. Functions can reference anything in or surrounding them. A variable defined locally, a variable defined in a surrounding function, something <code>def</code>-ed in the program, a built-in function - these are all said to be "in scope". If a function uses the same name for a variable as something that is already in scope it won't affect either one. However, the variable name in the inner function will overshadow the outer variable, function or data preventing the outer variable, function or data from being referenced in the inner function. Scoping can be a strange concept until you've worked with it, luckily none of the code here does any overshadowing. 

If you take the output of <code>(lesser-numbers [6 5 8 11 3 2 7 9 4 1 10 12])</code> and repeatedly call <code>lesser-numbers</code> on it, you’ll begin to see the far left branch of our evaluation tree. Though you can do this by hand it can also be demonstrated directly in the language.

<pre><code class="language-klipse">
(def lesser-numbers
  (fn [coll]
    (filterv (fn [x]
    	       (< x (first coll)))
             (rest coll))))

(take-while not-empty
            (iterate lesser-numbers
                     [6 5 8 11 3 2 7 9 4 1 10 12]))
</code></pre>

![Left Evaluation Branch]({{ "/assets/left-branch.png" | absolute_url }})

Testing ideas like this by giving the computer snippets of code and examining the return value is akin to having a conversation with the computer in which you can bounce ideas off it (“Do these pants go with my shoes?”).

To collect elements which go in the right-side group we need only to select the elements which didn’t make the cut for the left-side group. We can do this in the same way but slip <code>not</code> into the function we pass to <code>filterv</code>.

<pre><code class="language-klipse">
((fn [coll]
   (filterv (fn [x]
    	      (not (< x (first coll))))
            (rest coll)))
 [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

The repeating aspect of our sorting function will be accomplished by simply calling our sorting function again on each of our left and right groups. Defining a function in terms of itself? What a concept!

Because concatenation is done only once at the end of our sorting function, we’ll pass the left group, first number and right group all to <code>concat</code> so that all the recursions take place before the concatenation. The first element must be placed in a vector because <code>concat</code> works on collections.

<pre><code class="language-klipse">
(def sort-numbers
  (fn [coll]
    (concat                             
     (sort-numbers                     
      (filterv (fn [x]                     ; <-- left group
                 (< x (first coll))) 
               (rest coll)))         
     [(first coll)]                         ; <-- first number
     (sort-numbers 
      (filterv (fn [x]                     
                 (not (< x (first coll)))) ; <-- right group
               (rest coll))))))

#_(sort-numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

Note that the functions passed to each <code>filterv</code> both have variables named <code>x</code>. One <code>x</code> doesn't overshadow the other because neither function surrounds the other.

We’re almost there! If you now apply <code>sort-numbers</code> to our test data by uncommenting the last expression, you’ll receive some sort of "call stack overflow" error. This is because there is nothing that stops the recursion from terminating. At the two places where we call <code>sort-numbers</code>, our function goes around and around. It’s for this reason <code>(take-while not-empty </code> was needed in the example showing the left evaluation branch. We need the recursion to stop when some criteria is met. According to our english program the terminating condition, sometimes called the "base case", is when the collection no longer has anything in it. <code>if</code> is a supremely useful function that will enable us to insert this check. <code>if</code> takes three arguments: a test, an output if the test evaluates to <code>true</code> and an output if the test evaluates to <code>false</code>. The test for if our variable <code>coll</code> is empty can be written simply as <code>(= [] coll)</code> and the false branch of our <code>if</code> function will contain the logic we've already covered.

<pre><code class="language-klipse">
(def sort-numbers
  (fn [coll]
    (if (= [] coll)
      []
      (concat
       (sort-numbers 
        (filterv (fn [x]
                   (< x (first coll)))
                 (rest coll)))
       [(first coll)]
       (sort-numbers
        (filterv (fn [x]
                   (not (< x (first coll))))
                 (rest coll)))))))

(sort-numbers [6 5 8 11 3 2 7 9 4 1 10 12])
</code></pre>

Returning an empty vector in the case that our collection is empty works because <code>concat</code>-ing any vector with an empty vector returns the same vector. Another way to think about this is that we are going to recurse until we get to a collection that we know to be sorted - an empty one.

As it turns out, the algorithm we’ve just implemented is known as Quicksort, one of many different sorting algorithms. What did you expect for your first program, a general purpose artificial intelligence? Surely, a sorting function is a necessary component so you’re part-way there!

<br>

The language we’ve been using is known as ClojureScript and it’s one of the world's nicest languages because of its simplicity. It has far fewer syntax and semantics than most all other programming languages. This raw simplicity makes it more powerful than other languages, not less.

ClojureScript is a dialect of Clojure and designed to run in a web browser. The code we’ve explored here works in both languages. If you’re interested in playing more with Clojure, <a href="repl.it">repl.it</a> has a browser-based environment with a scratch area. <a href="clojurescriptkoans.com">clojurescriptkoans.com</a> and <a href="4Clojure.com">4Clojure.com</a> offer little puzzles to cut your teeth on. A cheatsheet of built-in functions can be found at <a href="https://clojure.org/api/cheatsheet">https://clojure.org/api/cheatsheet</a>

Keep in mind that you learn to program by doing it, not just reading about it, so get to it!

Some of the information in this post may only be approximately true but further refinements will have to be left for another time.

Happy computing!

<style>
body {
  background: #b3d9ff;
}
</style>

<link rel="stylesheet" type="text/css" href="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css">

<script> console.log("hello from script tag.") </script>

<script>
  window.klipse_settings = {
    selector: '.language-klipse'// css selector for the html elements you want to klipsify
  };
</script>

<script src="https://storage.googleapis.com/app.klipse.tech/plugin/js/klipse_plugin.js"></script>
