# JavaScript

The console is part of the web browser and allows you to log messages, run JavaScript code, and see errors and warnings. \


#### JS Basics

Example function used to generate output to the console:

```javascript
console.log("Hello Humans!");
```

Enclosed text in quotes:

```javascript
console.log("I love free cyber training");
```

Quotes are not needed for numbers:

```javascript
console.log(1337);
```

The console.log() function can be used as many times as needed:

```javascript
console.log("Hello Humans!");
console.log("Take me to your leader");
```

#### JavaScript in HTML

You can add JavaScript code in an HTML document using the \<script> tag:

```html
<body>
    <script>
      console.log("JavaScript in HTML");
    </script>
</body>
```

Alert Box display messages with the alert() function

```html
<body>
    <script>
      console.log("JavaScript in HTML");
      alert("I may be testing XSS now");
    </script>
</body>
```

#### Comments

Comments are used to describe code and other information\
\
A single-line comment starts with `//`

Multi-line comments start with `/*` and end with `*/` making everything in between a comment

<pre><code><strong>//I wonder if I can display two messages in the same script tag
</strong><strong>
</strong><strong>/* The code below
</strong>should uffice for
<strong>for testing */
</strong><strong>
</strong><strong>&#x3C;body>
</strong>    &#x3C;script>
      console.log("JavaScript in HTML");
      alert("I may be testing XSS now");
    &#x3C;/script>
&#x3C;/body>
</code></pre>

