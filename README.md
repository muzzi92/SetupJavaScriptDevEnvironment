# How To Set Up A Sweet, Sweet JavaScript Development Environment #

If you're new to JavaScript, setting up a project can be a pain. It can also pave the way for for a lot of pitfalls and route errors. The following will guide you through the basic setup for a full-stack JS development environment, using Node JS, Express and Jasmine. As you can see below, it's nice to keep your tree clean and readable.

---

Hidden View                           |  Expanded View
:------------------------------------:|:--------------------------------------:
![](https://i.imgur.com/3GYrzix.png)  |  ![](https://i.imgur.com/kUS2zq1.png")

## Step One ##

[Download Node JS](https://nodejs.org/en/). Conveniently, downloading Node will also give you access to NPM on your machine. NPM is Node's package manager and allows you to install a multitude of other packages that will make your life easier, such as Express.

## Step Two ##

Create you're project directory. I'm sorry to state the obvious but we may as well start at the beginning.

```
mkdir myProject
```

## Step Three ##

Initialise NPM in your project directory to automatically create a `package.json` file. This file organises and stores all the packages that your project depends on.

```
npm init
```

## Step Four ##

Install Express JS. This framework will help you manage your routes as well as handle your requests and views.

```
npm install express --save
```
(The -- save will automatically list express in your package.json file after installing)

## Step Five ##

Create a views directory. It is good practice to keep HTML (or similar dynamic HTML) web pages in a views folder. Express will automatically look for a views folder when you tell it to render pages.

```
mkdir views
```

## Step Six ##

Make a public directory to house your JavaScript model code and CSS if you need it.

```
mkdir public
```
```
mkdir public/js
mkdir public/css
```
Create your javascript file in the js folder:
```
touch public/js/demoApp.js
```
Type in some code for test purposes:
```javascript
console.log('This should be visible in the console when the index page is loaded')
```

## Step Seven ##

Install EJS. EJS is a simple templating language that lets you generate HTML with plain JavaScript (similar to ERB for Ruby).

```
npm install ejs --save
```

## Step Eight ##

Create your first EJS file in views. Call it whatever you like, but this is what we will use to render our homepage for this demo.

```
touch views/index.ejs
```
Link your JS file with a script tag in the head and throw some text in the body so you can test everything is working later.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>title</title>
    <script type="text/javascript" src="demoApp.js"></script>
  </head>
  <body>
    <h1> Hello World </h1>
  </body>
</html>
```

## Step Nine ##

In order to keep the directory clean, we can avoid duplicating the HTML template in each view file by extracting them as partials.

```
mkdir views/partials
```
```
touch views/partials/header.js
touch views/partials/footer.js
```
In these files you can place the HTML skeleton tags that surround the body of each view.
So in "header.ejs", you can put:
``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>title</title>
    <script type="text/javascript" src="demoApp.js"></script>
  </head>
  <body>
```
and in "footer.ejs", put:
``` html  
  </body>
</html>
```

Now, at the top of each of your views files you include these partials at the top and bottom respectively. and hence avoid extra tags clogging up your files.
Here is how we would do that in our **index.ejs** file:
```html
<% include partials/header %>
<h1> Hello World </h1>
<% include partials/footer %>
```

## Step Ten ##

Create a lib folder in the root to house your jasmine files.
```
mkdir lib
```
Then simply [download](https://github.com/jasmine/jasmine/releases) the latest Jasmine standalone, move it to this newly created lib folder and unzip it.
```
unzip jasmine-standalone-3.1.0.zip
```

## Step Eleven ##

Create a controller file in the root of your project directory. This is where we will manage all out get/ post requests and load up the server from.

```
touch app.js
```

Now add the following lines of code to your app.js to get it set up:

``` javascript
var express = require("express");
var app = express();
```
This requires the express package and saves it to a variable, app, which you will use to call express methods on in this file.

```JavaScript
app.use(express.static("public"));
```
This tells express to look in the public directory when searching for our JS model.

```javascript
app.set("view engine", "ejs")
```
This nifty bit of code allows you to drop the ".ejs" at the end of your file names in your requests. A nice little luxury for small projects, a time saver for big projects.

``` javascript
app.get("/", function(req, res){
  res.render("index");
  });
```
This is our basic get request that renders our view, index.ejs, when the index (root) route is visited.

```javascript
app.listen(3000, function(){
  console.log("Serve's Up Dude!")
});
```
Last but not least, we need this line to load our server on to the localhost, port 3000. The console log message is simply for visual verification when your server is up and running.

## Finally ##

Now you will be able to throw the server up from your command line with:
```
node app.js
````
and go to port 3000 on your localhost to see your index.ejs file rendered:

http://localhost:3000/
