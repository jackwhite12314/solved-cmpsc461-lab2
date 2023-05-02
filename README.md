Download Link: https://assignmentchef.com/product/solved-cmpsc461-lab2
<br>
<strong>Set-up: </strong>For this assignment, edit a copy of mulb.rkt, which is on the course website. In particular, replace occurrences of “CHANGE” to complete the problems. Do not use any mutation (set!, set-mcar!, etc.) anywhere in the assignment.

This assignment is built on top of MUL461 Part A. You will need to copy over your implementation for Part A before proceeding with the project to be able to pass the tests.

<strong>Overview: </strong>This project has to do with mul461 (a Made Up Language for CMPSC 461). mul461 programs are written directly in Racket by using the constructors defined by the structs defined at the beginning of mulb.rkt. This is the definition of mul461’s syntax for Part A:

<ul>

 <li>If <em>s </em>is a Racket string, then (mul461-var <em>s</em>) is a mul461 expression (a variable use).</li>

 <li>If <em>n </em>is a Racket integer, then (mul461-int <em>n</em>) is a mul461 expression (an integer constant).</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-+ <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression (an addition).</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461– <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression (a subtraction). If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-* <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression (a multiplication).</li>

 <li>If <em>b </em>is a Racket boolean, then (mul461-bool <em>b</em>) is a mul461 expression (a boolean constant).</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-and <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>should both evaluate to mul461-bool values.</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-or <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>should both evaluate to mul461-bool values.</li>

 <li>If <em>e </em>is a mul461 expression that evaluates to a mul461-bool value, then (mul461-not <em>e</em>) is a mul461</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-&lt; <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression that evaluates to a mul461-bool value if <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>evaluate to mul461-int</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-= <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression that evaluates to a mul461-bool value if <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>evaluate to mul461-int</li>

 <li>If <em>e</em><sub>1</sub>, <em>e</em><sub>2</sub>, and <em>e</em><sub>3 </sub>are mul461 expressions, then (mul461-if <em>e</em><sub>1 </sub><em>e</em><sub>2 </sub><em>e</em><sub>3</sub>) is a mul461 It is a condition where the result is <em>e</em><sub>2 </sub>if <em>e</em><sub>1 </sub>is a boolean constant of true else the result is <em>e</em><sub>3</sub>. Only one of <em>e</em><sub>2 </sub>and <em>e</em><sub>3 </sub>is evaluated.</li>

 <li>If <em>s </em>is a Racket string and <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-let <em>s e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression (a let expression where the value resulting from evaluating <em>e</em><sub>1 </sub>is bound to <em>s </em>in the evaluation of <em>e</em><sub>2</sub>).</li>

</ul>

This is additional syntax of the language for Part B. In Part B we are adding support for pairs and function (lambda expressions) and function calls into our mul461 language.

<ul>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-cons <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression (a paircreator).</li>

 <li>If <em>e </em>is a mul461 expression, then (mul461-car <em>e</em>) is a mul461 expression (getting the first part of a pair).</li>

 <li>If <em>e </em>is a mul461 expression, then (mul461-cdr <em>e</em>) is a mul461 expression (getting the second part of a pair).</li>

 <li>(mul461-null) is a mul461 expression (holding no data, much like () in ML or null in Racket). Notice (mul461-null) is a mul461 expression, but mul461-null is not.</li>

 <li>If <em>e </em>is a mul461 expression, then (mul461-isnull <em>e</em>) is a mul461 expression (testing for (mul461-null)) that should evaluates to mul461 expression of boolean value (mul461-bool #t) or (mul461-bool #f).</li>

 <li>If <em>s</em><sub>1 </sub>and <em>s</em><sub>2 </sub>are Racket strings and <em>e </em>is a mul461 expression, then (mul461-fun <em>s</em><sub>1 </sub><em>s</em><sub>2 </sub><em>e</em>) is a mul461 expression (a function). In <em>e</em>, <em>s</em><sub>1 </sub>is bound to the function itself (for recursion) and <em>s</em><sub>2 </sub>is bound to the (one) argument.</li>

 <li>If <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>are mul461 expressions, then (mul461-call <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>) is a mul461 expression (a function call).</li>

 <li>(mul461-closure <em>f env</em>) is a mul461 value where <em>f </em>is mul461 function (an expression made from mul461-fun) and <em>env </em>is an environment mapping variables to values. Closures do not appear in source programs; they result from evaluating functions.</li>

</ul>

In Part A, A mul461 <em>value </em>is a mul461 integer constant, a or a mul461 boolean constant.

In Part B, A mul461 value from Part A is still a value, and for the case of pairs, the definition of a mul461 <em>value </em>is recursive: a mul461 expression (mul461-null) is a mul461 value. If <em>v</em><sub>1</sub>, <em>v</em><sub>2 </sub>are mul461 values, then (mul461-cons <em>v</em><sub>1 </sub><em>v</em><sub>2</sub>) is also a mul461 value. A mul461 (mul461-fun …) evalutes to a mul461 value as a (mul461-closure f env) with its current environment. The env for f in the closure is implemented as static scoping with deep-binding.

You should assume mul461 programs are syntactically correct (e.g., do not worry about wrong things like (mul461-int “hi”) or (mul461-int (mul461-int 37)). But do <em>not </em>assume mul461 programs are free of type errors like (mul461-+ (mul461-bool #t) (mul461-int 7)) or (mul461-not (mul461-int 3)).

<strong>Warning: </strong>What makes this assignment challenging is that you have to understand mul461 well and debugging an interpreter is an acquired skill.

<strong>Turn-in Instructions: </strong>Turn in your modified mulb.rkt to gradescope.

<strong>Problems:</strong>

<ol>

 <li><strong>Implementing the </strong>mul461 <strong>Language: </strong>Write a mul461 interpreter, i.e., a Racket function eval-exp that takes a mul461 expression e and either returns the mul461 value that e evaluates to under the empty environment or calls Racket’s error if evaluation encounters a run-time mul461 type error or unbound mul461</li>

</ol>

A mul461 expression is evaluated under an environment (for evaluating variables, as usual). In your interpreter, use a Racket list of Racket pairs to represent this environment (which is initially empty) so that you can use <em>without modification </em>the provided envlookup function. Here is a description of the semantics of mul461 expressions:

<ul>

 <li>All values evaluate to themselves. For example, (eval-exp (mul461-int 17)) would return (mul461-int 17), <em>not </em></li>

 <li>A variable evaluates to the value associated with it in the environment.(This case for var is done for you.)</li>

 <li>An addition/subtraction/multiplication evaluates its subexpressions and, assuming they both produce integers, produces the mul461-int <em>n </em>that is their sum/difference/product. (Note the case for addition is done for you to get you pointed in the right direction.)</li>

 <li>An <em>&lt; </em>or = comparison evaluates its subexpressions and, assuming they both produce integers, produces the mul461-bool <em>b </em>that is the result of comparing the two integer values.</li>

 <li>An and/or evaluates its subexpressions and, assuming they both produce booleans, produces the mul461-bool <em>b </em>that is their and/or boolean operation result.</li>

 <li>A not evaluates its subexpression and, assuming it produces a boolean, produces the mul461-bool <em>b </em>that is the logical negation of its subexpression result.</li>

 <li>An if evaluates its first expression to a value <em>v</em><sub>1</sub>. If it is a boolean, then if it is mul461-bool #t, then if evaluates to its second subexpression, else it evaluates its third subexpression. Only one of <em>e</em><sub>2 </sub>and <em>e</em><sub>3 </sub>should be evaluated. Do not evaluate both <em>e</em><sub>2 </sub>and <em>e</em><sub>3</sub>.</li>

 <li>A let expression evaluates its first expression to a value <em>v</em>. Then it evaluates the second expression to a value, in an environment extended to map the name in the let expression to <em>v</em>.</li>

</ul>

Here is additional description of the semantics of mul461 expressions from Part B:

<ul>

 <li>All values evaluate to themselves. For example, (mul461-null), (mul461-closure f env) are already mul461</li>

 <li>For a pair creater expression (mul461-cons <em>e</em><sub>1 </sub><em>e</em><sub>2</sub>), you should first evaluate the sub-expressions <em>e</em><sub>1 </sub>and <em>e</em><sub>2 </sub>to mul461 values <em>v</em><sub>1 </sub>and <em>v</em><sub>2</sub>, and the original pair will evaluate to (mul461-cons <em>v</em><sub>1 </sub><em>v</em><sub>2</sub>)</li>

 <li>For mul461-car and mul461-cdr, you should first evaluate the subexpression <em>e </em>to mul461 value <em>v</em>. If <em>v </em>is not of the form (mul461-cons <em>v</em><sub>1 </sub><em>v</em><sub>2</sub>), then you should raise a type error similar to when adding non-integers. Assume <em>e </em>evaluates to (mul461-cons <em>v</em><sub>1 </sub><em>v</em><sub>2</sub>), then (mul461-car e) should evaluate to <em>v</em><sub>1 </sub>and (mul461-cdr e) should evaluate to <em>v</em><sub>2</sub>.</li>

 <li>For (mul461-isnull e), you should first evaluate <em>e </em>to a value <em>v</em>. If <em>v </em>is (mul461-null), then the testing expression should evaluate to mul461-bool #t; other wise the testing expression should evaluate to mul461-bool #f.</li>

 <li>For a mul461 expression <em>e </em>that is (mul461-fun fname formal body), it should be evaluated to a closure (mul461-closure e env) where env is the current env that provides mapping for all potential free vars in <em>e</em>.</li>

 <li>For a function call mul461 expression (mul461-call f actual), you should first evaluate <em>f </em>to <em>v</em><sub>1 </sub>and actual to <em>v</em><sub>2</sub>, and then make sure that <em>v</em><sub>1 </sub>is a closure (or otherwise a type error should be raised). Assume <em>v</em><sub>1 </sub>is a closure of the form (mul461-closure (mul461-fun fname formal body) env), then you should add these two bindings to the env in the closure (formal: <em>v</em><sub>2</sub>, fname:<em>v</em><sub>1</sub>, env) and evaluate body with this new environment that binds the formal parameter to the actual argument value and binds the function name to the function closure for recursive functions.</li>

</ul>

<ol start="2">

 <li><strong>Expanding the Language: </strong>mul461 is a small language, but we can write Racket functions that act like mul461 macros so that users of these functions feel like mul461 is larger. The Racket functions produce mul461 expressions that could then be put inside larger mul461 expressions or passed to eval-exp. In implementing these Racket functions, do not use closure (which is used only internally in eval-exp). Also do not use eval-exp (we are creating a program, not running it).

  <ul>

   <li>Write a Racket function makelet* that takes a Racket list of Racket pairs ’((<em>s</em><sub>1 </sub>. <em>e</em><sub>1</sub>) …(<em>s<sub>i </sub></em>. <em>e<sub>i</sub></em>) …(<em>s<sub>n </sub></em>. <em>e<sub>n</sub></em>)) and a final mul461 expression <em>e<sub>n</sub></em><sub>+1</sub>. In each pair, assume <em>s<sub>i </sub></em>is a Racket string and <em>e<sub>i </sub></em>is a mul461 makelet* returns a mul461 expression whose value is <em>e<sub>n</sub></em><sub>+1 </sub>evaluated in an environment where each <em>s<sub>i </sub></em>is a variable bound to the result of evaluating the corresponding <em>e<sub>i </sub></em>for 1 ≤ <em>i </em>≤ <em>n</em>. The bindings are done sequentially, so that each <em>e<sub>i </sub></em>is evaluated in an environment where <em>s</em><sub>1 </sub>through <em>s<sub>i</sub></em><sub>−1 </sub>have been previously bound to the values <em>e</em><sub>1 </sub>through <em>e<sub>i</sub></em><sub>−1</sub>.</li>

   <li>Write a Racket function makelist that takes a Racket list of mul461 expressions, and creates a mul461 expression that is essentially a list of these mul461 expressions using mul461-cons and mul461-null. Do not evaluate any of the expressions.</li>

  </ul></li>

 <li><strong>Using the Language: </strong>We can write mul461 expressions directly in Racket using the constructors for the structs and (for convenience) the functions we wrote in the previous problem.

  <ul>

   <li>Write a function makefactorial that gives a racket integer n, returns a mul461 expression that is similar to <em>n </em>∗ ((<em>n </em>− 1) ∗ (<em>n </em>− 2)<em>… </em>∗ 1) using mul461 For example (makefactorial 3) should return this value:</li>

  </ul></li>

</ol>

(mul461-* (mul461-int 3) (mul461-* (mul461-int 2) (mul461-int 1))).

<ul>

 <li>Bind to the Racket variable mul461-filter a mul461 function that acts like filter (as we used in Racket). Your function should be curried: it should take a mul461 function and return a mul461 function that takes a mul461 list and applies the function to every element of the list returning a new mul461 list with all the elements for which the function returns (mul461-bool #t). Recall a mul461 list is (mul461-null) or a pair where the second component is a mul461</li>

 <li>Bind to the Racket variable mul461-map a mul461 function that acts like map (as we used in Racket). Your function should be curried: it should take a mul461 function and return a mul461 function that takes a mul461 list and applies the function to every element of the list, returning a new mul461 list with all the elements be the return value of the function.</li>

</ul>