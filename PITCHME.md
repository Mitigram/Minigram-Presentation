# Minigram

---?color=linear-gradient(90deg, #5384AD 65%, white 35%)
@title[Agenda]

@snap[north-west h4-white]
#### Agenda
@snapend

@snap[west span-55]
@ul[list-spaced-bullets text-white text-04]
- Current state of Mitigram
- Modern JavaScript 
- Package management, bundling, task runners and transpiling
- ES2015 (ES6) and beyond...
- TypeScript
- Frontend libraries and frameworks
- Redux 
- DOM and virtual DOM
- React
- Vue
- Angular
- Minigram project
- Feature comparison and discussions
- Bring Mitigram in to the modern era
- Web Components
- Angular Elements
@ulend
@snapend

@snap[east span-45]
@img[shadow](assets/img/JSLogo.png)
@snapend

---

#### Using JavaScript the “old-school” way

```HTML
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mitigram Marketplace</title>
  <script src="index.js"></script>
</head>
<body>
  <h1>Hello from HTML!</h1>
</body>
</html>
```
---

```JavaScript
// index.js
console.log("Hello from JavaScript!");
```
---

#### Including Moment.js

```HTML
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mitigram Marketplace</title>
  <script src="moment.min.js"></script>
  <script src="index.js"></script>
</head>
<body>
  <h1>Hello from HTML!</h1>
</body>
</html>
```
---

```JavaScript
// index.js
console.log("Hello from JavaScript!");
console.log(moment().startOf('day').fromNow());
```
---

#### Package management

@ul[list-spaced-bullets text-02]
- Bower - 2013 - https://bower.io/
- npm - 2015 - https://www.npmjs.com/
- yarn - 2016 - https://yarnpkg.com
@ulend

#### Using NPM

```
$ npm init
```
```JSON
{
  "name": "your-project-name",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```
```
$ npm install moment --save
```

---

#### Installing moment using NPM

```
$ npm install moment --save
```
```JSON
{
  "name": "modern-javascript-example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "moment": "^2.22.2"
  }
}
```

---

#### Using moment from NPM

```HTML
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript Example</title>
  <script src="node_modules/moment/min/moment.min.js"></script>
  <script src="index.js"></script>
</head>
<body>
  <h1>Hello from HTML!</h1>
</body>
</html>
```

---

#### Using a JavaScript module bundler (webpack)

Most programming languages provide a way to import code from one file into another. JavaScript wasn’t originally designed with this feature, because JavaScript was designed to only run in the browser, with no access to the file system of the client’s computer (for security reasons). So for the longest time, organizing JavaScript code in multiple files required you to load each file with variables shared globally.

In 2009, a project named CommonJS was started with the goal of specifying an ecosystem for JavaScript outside the browser. 

The most well-known of implementation of CommonJS modules is node.js.

---

```JavaScript
// index.js
var moment = require('moment');
console.log("Hello from JavaScript!");
console.log(moment().startOf('day').fromNow());
```

This is all great for node.js, but if you tried to use the above code in the browser, you’d get an error saying require is not defined. The browser doesn’t have access to the file system.

This is where a module bundler comes in.

---

We need a module bundler to find all require statements (which is invalid browser JavaScript syntax) and replace them with the actual contents of each required file. 

Around 2015, webpack eventually became the more widely used module bundler (fueled by the popularity of the React frontend framework, which took full advantage of webpack’s various features).

---

```
$ npm install webpack webpack-cli --save-dev
```

```JSON
{
  "name": "modern-javascript-example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "moment": "^2.19.1"
  },
  "devDependencies": {
    "webpack": "^4.17.1",
    "webpack-cli": "^3.1.0"
  }
}
```

---

```
$ ./node_modules/.bin/webpack index.js --mode=development
```

This command will run the webpack tool that was installed in the node_modules folder, start with the index.js file, find any require statements, and replace them with the appropriate code to create a single output file (which by default is dist/main.js). 

---

```HTML
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript Example</title>
  <script src="dist/main.js"></script>
</head>
<body>
  <h1>Hello from HTML!</h1>
</body>
</html>
```
---

This is tedious, and will get even more tedious as we use webpack’s more advanced features (like generating source maps to help debug the original code from the transpiled code).

```JavaScript
// webpack.config.js
module.exports = {
  mode: 'development',
  entry: './index.js',
  output: {
    filename: 'main.js',
    publicPath: 'dist'
  }
};
```

```
$ ./node_modules/.bin/webpack
```

---

#### Advantages of bundling

- We are no longer loading external scripts via global variables (yay!)
- Any new JavaScript libraries will be added using require statements in the JavaScript
- Having a single JavaScript bundle file is often better for performance.
- And now that we added a build step, there are some other powerful features we can add to our development workflow!
- Transpiling code for new language features - ES6 and beyond!

---

### JavaScript versions

|     |                       |                                                                                                                     |   |   |
|-----|-----------------------|---------------------------------------------------------------------------------------------------------------------|---|---|
| 1   | ECMAScript 1 (1997)   | First Edition.                                                                                                      |   |   |
| 2   | ECMAScript 2 (1998)   | Editorial changes only.                                                                                             |   |   |
| 3   | ECMAScript 3 (1999)   | Added Regular Expressions.Added try/catch.                                                                          |   |   |
| 4   | ECMAScript 4          | Never released.                                                                                                     |   |   |
| 5   | ECMAScript 5 (2009)   | Added "strict mode". Added JSON support. Added String.trim(). Added Array.isArray(). Added Array Iteration Methods. |   |   |
| 5.1 | ECMAScript 5.1 (2011) | Editorial changes.                                                                                                  |   |   |
| 6   | ECMAScript 2015       | Added let and const. Added default parameter values. Added Array.find(). Added Array.findIndex().                   |   |   |
| 7   | ECMAScript 2016       | Added exponential operator (**). Added Array.prototype.includes.                                                    |   |   |
| 8   | ECMAScript 2017       | Added string padding. Added new Object properties. Added Async functions. Added Shared Memory.                      |   |   |
| 9   | ECMAScript 2018       | Added rest / spread properties. Added Asynchronous iteration. Added Promise.finally(). Additions to RegExp.         |   |   |

---

### Browser support

JavaScript has had modules for a long time implemented via libraries (require.js), not built into the language. 

ES6 is the first time that JavaScript has built-in modules.

ECMAScript 3 is fully supported in all browsers.

ECMAScript 5 is fully supported in all modern browsers.

Internet Explorer does not support ES6.

Safari 10 and Edge 14 were the first browsers to fully support ES6.

Chrome 68 and Operd 55 support ES7.

---

### Using babel

- CoffeeScript - 2010 - http://coffeescript.org/
- TypeScript - 2012 - https://www.typescriptlang.org
- babel - 2014 - https://babeljs.io/

```
$ npm install @babel/core @babel/preset-env babel-loader --save-dev
```





### Arrows
Arrows are a function shorthand using the `=>` syntax.  They are syntactically similar to the related feature in C#, Java 8 and CoffeeScript.  They support both statement block bodies as well as expression bodies which return the value of the expression.  Unlike functions, arrows share the same lexical `this` as their surrounding code.

```JavaScript
// Expression bodies
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);
var pairs = evens.map(v => ({even: v, odd: v + 1}));

// Statement bodies
nums.forEach(v => {
  if (v % 5 === 0)
    fives.push(v);
});

// Lexical this
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
}
```

---

## Add Some Slide Candy

![IMAGE](assets/img/presentation.png)

---?color=linear-gradient(180deg, white 75%, black 25%)
@title[Customize Slide Layout]

@snap[west span-50]
## Customize the Layout
@snapend

@snap[east span-50]
![IMAGE](assets/img/presentation.png)
@snapend

@snap[south span-100 text-white]
Snap Layouts let you create custom slide designs directly within your markdown.
@snapend

---?color=linear-gradient(90deg, #5384AD 65%, white 35%)
@title[Add A Little Imagination]

@snap[north-west h4-white]
#### And start presenting...
@snapend

@snap[west span-55]
@ul[list-spaced-bullets text-white text-09]
- You will be amazed
- What you can achieve
- *With a little imagination...*
- And **GitPitch Markdown**
@ulend
@snapend

@snap[east span-45]
@img[shadow](assets/img/conference.png)
@snapend

---

@snap[north-east span-100 text-pink text-06]
Let your code do the talking!
@snapend

```sql zoom-18
CREATE TABLE "topic" (
    "id" serial NOT NULL PRIMARY KEY,
    "forum_id" integer NOT NULL,
    "subject" varchar(255) NOT NULL
);
ALTER TABLE "topic"
ADD CONSTRAINT forum_id
FOREIGN KEY ("forum_id")
REFERENCES "forum" ("id");
```

@snap[south span-100 text-gray text-08]
@[1-5](You can step-and-ZOOM into fenced-code blocks, source files, and Github GIST.)
@[6,7, zoom-13](Using GitPitch live code presenting with optional annotations.)
@[8-9, zoom-12](This means no more switching between your slide deck and IDE on stage.)
@snapend


---?image=assets/img/presenter.jpg

@snap[north span-100 h2-white]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
