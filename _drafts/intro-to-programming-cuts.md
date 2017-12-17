<pre><code class="language-klipse">
(def less-than?
  (fn [x y]
      (< ()))))
      </code></pre>

<pre><code class="language-klipse">
(less-than? 17 6 11)
</code></pre>

You may have noticed that our less-than? function doesn\u2019t do anything the built in < doesn\u2019t. Our function would be simpler if we merely applied the function < to our data. Although we typically do this with parens Clojure gives us an apply function aswell. The following is similar to our last definition of less-than?\u2019

<pre><code class="language-klipse">
(def less-than?
  (fn [coll]
      (apply < coll))))
      </code></pre>

It may be helpful to think of every expression as an application of apply, a function and a collection of input. In fact, this is actually what\u2019s going on under the hood when the computer evaluates your code.

(apply a-function [input0 input1 input2 input3 ...])

You\u2019ll notice that if we now call less-than? with 17 6 and 11 as we did previously we\u2019ll receive some sort of error from the computer about using the wrong number of arguments.  Now we must wrap our numbers in a vector when calling less-than? on it. This has two consequences. On the plus side we can now test any amount of numbers by including them in our vector. However, imagine if less-than? were a component in a larger program. By expecting a collection of potentially many numbers instead of exactly three numbers we\u2019ve introduced a bug anywhere less-than? is invoked. Fortunately we can have our cake and eat it too.

<pre><code class="language-klipse">
(def less-than?
  (fn [& numbers]
      (apply < numbers))))
      </code></pre>

The & in the function definition means that it can accept any number of arguments and they will be put into a collection that can be referred to as numbers.

<pre><code class="language-klipse">
(less-than? 17 6 11)
</code></pre>

All that for a function that is no better than <... Now that we know how to define functions, let\u2019s get back to sorting!






Although a programming language is necessary for developing a program which runs on a computer, it\u2019s important to realize that any language will do and that thinking precisely and procedurally is the key. Clojure is the nicest language I know because of how little it gets in your way. Both its syntax and semantics are far smaller and simpler than most every other programming language. This puts a minimal amount of distance between you and the logic you intend to express.

At this point you know nearly everything required to write a program of any magnitude in Clojure. Although Clojure isn\u2019t always a good fit for every application, any software you can think of, be it an operating system, webpage, pacemaker or sorting program, is merely a group of smaller functions composed to synthesize a new function. In fact, most of Clojure\u2019s built-in functions are themselves comprised of yet more primitive functions. Their difference is not a fundamental one but a matter of degree.