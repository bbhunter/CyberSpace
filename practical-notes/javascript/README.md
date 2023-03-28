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
      alert("I think I can learn XSS now");
    </script>
</body>
```

#### Comments

Comments are used to describe code and other information\
\
A single-line comment starts with `//`

Multi-line comments start with `/*` and end with `*/` making everything in between a comment

<pre class="language-javascript"><code class="lang-javascript"><strong>//I wonder if I can display two messages in the same script tag
</strong><strong>
</strong><strong>/* The code below
</strong>should suffice
<strong>for testing */
</strong><strong>
</strong><strong>&#x3C;body>
</strong>    &#x3C;script>
      console.log("JavaScript in HTML");
      alert("I think I can learn XSS now");
    &#x3C;/script>
&#x3C;/body>
</code></pre>

#### Logic

JavaScript uses the basic programming operators for math such as `+`. `-`, `/`,  `*`, including `(`, and `)`, for order of operations.

```javascript
/* 30 days
1 day = 24 hours
1 hour = 60 minutes
1 minute = 60 seconds */

//Aproximately how many seconds are in a year?
console.log(60*60*24*30);
```

#### Variables

* variable names must begin with a letter, an underscore `_` or a dollar sign `$`
* variable names cannot contain spaces
* variable names can only contain letters, numbers, underscores, or dollar signs.
* variable names are case-sensitive, which means that, for example, Name and name variables are different

Create a variable (initialize) in JS with `let` or `var`:

```javascript
let name;
name = "Martian";
```

OR

```javascript
let name = "Martian";
let number = 1337
```

Note: the use of let is recommended instead of var when decalring variables

Remembering the definition of variable, remember that they can change on they fly:

```javascript
let num = 7331;
num = 1337;
//num = 7;
console.log(num);
```

#### Constants

Constants must have a value when declared and they cannot change their value.

```javascript
const cyberpsace = 'green';
console.log(color); color = 'blue'; //confirm this will not work
```
