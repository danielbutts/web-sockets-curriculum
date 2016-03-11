# Set Up
These instructions go through how to set up your sockets when not using the express generator!

### Not using the Express Generator
In the command line:
```
npm init
npm install socket.io express -S
touch app.js
echo node_modules > .gitignore
```
Then open up your app.js and set up your socket:
```js
var Express = require('express');
var Socket = require('socket.io');
var http = require('http');
```
*Keep in mind that 'Express' and 'Socket' are capitalized above!*

Continue in the app.js...
```js
var app = Express();
var server = http.createServer(app);
var io = Socket(server);
```
So what's going on this last bit? First we define app, that's just setting up our express middleware. Then we create a http server that is going to use our express as middleware. And lastly we include the socket in on everything and let it use our Express server.

Now head into your package.json file and add a start key with the value 'nodemon app.js' to your scripts object so it looks something like this:
```
"scripts": {
  "start": "nodemon app.js",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```
Once you've done that, go ahead and install nodemon in the command line...
```
npm install nodemon -D
```
Next your going to create a 'public' folder with an 'index.html' and 'main.js' file in there.
Now we have to tell our middleware where we're going to hosting our static sites. How do we do that?

```js
app.use(Express.static('public'));
```

Now let's get our localhost running and setup....remember how to do that?

```js
var port = 3000;
server.listen(port, function(){
  console.log('Now listening on port: ' + port);
})
```
**Question:** Why do we write 'server.use' instead of our normal 'app.use' here?

Next we have to bring in the socket CDN in our Index.html! Check which version of Socket.io you're using (in your package.json) and go grab that CDN!
I have version 1.4.5 here for you:

*https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.js*

Awesome! You can throw in a console.log in your main.js so you can make that's wired up too! Then let's start our server!
```js
npm start
```

CHECK IN: How is everything? Is your server running correctly? What about your console?

**Question:** Where do we go to manipulate our Client now? What about our Server?

- Your Client side is going to consist of your browser and your public folder files!
- Your Server side consists of your app.js and your running nodemon!


To debrief your index.html should look like...
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Socket Chat</title>
  </head>
  <body>
    Hello World
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.js" charset="utf-8"></script>
    <script src="main.js" charset="utf-8"></script>
  </body>
</html>
```

and your App.js should look like....
```js
var Express = require('express');
var Socket = require('socket.io');
var http = require('http');

var app = Express();
var server = http.createServer(app);
var io = Socket(server);

app.use(Express.static('public'));

var port = 3000;
server.listen(port, function(){
  console.log('Now listening on port: ' + port);
})
```

__ARE WE READY TO SET UP OUR FIRST SOCKET???__

Go back into your app.js and let's get your first socket set up!
```js
io.on('connection',function(socket){
  console.log('We are entering the chat room');
})
```

In your main.js write
```js
var socket = io();
```

That's it! How can I check if my socket exists? Where should I see my console.logs?!?! Does Chrome web tools allow me to see when a site is using web sockets?

**Google It!**

If you did things correctly, we should see 'We are entering the chat room' logged out on the server side, and if we go under chrome web tools -> Network -> WS and refresh our browser, we should see a web socket!

__You're Fully Set Up Now!__
