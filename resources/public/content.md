## Parinfer

Illustrating a simple editor feature
that may simplify how we write Lisp.

### TLDR

- perhaps an intuitive alternative to [paredit]
- adjust indentation to affect nesting (without hiding parens)
- a natural way to keep your code properly formatted

[paredit]:http://danmidwood.com/content/2014/11/21/animated-paredit.html

 <textarea id="code-intro">
</textarea>

### Background

In Lisp, parentheses tend to bunch together at the end of a line. This
[convention] can be jarring at first if you are used to curly braces in other
languages being on their own lines:

[convention]:https://en.wikipedia.org/wiki/Indent_style#Lisp_style

 <div class="two-col">
<div class="col">
<div class="caption">Lisp Style</div>
<textarea id="code-lisp-style">
(defn foo [a b]
  (let [x (+ a b)]
    (println "The sum is" x)))
</textarea>
</div>

<div class="col">
<div class="caption">C Style</div>
<textarea id="code-c-style">
(defn foo [a b]
  (let [
     x (+ a b)
    ]
    (println "The sum is" x)
  )
)
</textarea>
</div>
</div>

But the convention in Lisp favors high information density, while still
employing an indentation style not unlike Python for readability.  Indentation
allows you to _skim_ while the parens allow you to _inspect_:

- __on skimming__: indentation creates a natural nested hierarchy (siblings aligned, children indented)
- __on inspecting__: highlight matching parens with your cursor in any editor to verify structure

It's natural to switch between these modes when reading, allowing you to choose
the resolution at which to view it.

 <div class="two-col">
<div class="col">
<div class="title">Skimming</div>
<textarea id="code-skim">
(defn foo [a b]
  (let [x (+ a b)]
    (println "The sum is" x)))
</textarea>
</div>

<div class="col">
<div class="title">Inspecting</div>
<textarea id="code-inspect">
(defn foo [a b]
  (let [x (+ a b)]
    (println "The sum is" x)))
</textarea>
</div>
</div>

### The idea

Similar to the way that we quickly _skim_ code by using its indentation, I
believe that we should be able to quickly _sketch_ code using indentation as
well.  Here's how that might look:

<textarea id="code-idea1">
(defn foo [a b])
(+ a b) ;; <-- insert space at front
</textarea>

What you see above is the editor allowing you to influence the structure of
your code based on indentation. Here's another example with deeper nesting:

<textarea id="code-idea2">
(defn component []
  (html)
  [:div.container]
  [:h1 "title"])
</textarea>

As a side effect, this makes it easy for us to insert/delete a line without
rearranging the pile of parens:

<textarea id="code-idea3">
(defn component []
  (html
   [:div.container
    [:h1 "title"]]))
    |  <-- start inserting here, then remove it
</textarea>

I think the key here is that we are writing/editing code without explicitly
managing where our parentheses close.  As a result, our code remains
properly formatted.

### Try It

<textarea id="code-try">
</textarea>