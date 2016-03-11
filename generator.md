# Set Up
These instructions go through how to set up your sockets when not using the express generator!

### If you use the Express App Generator
Generate your app!
```
express --git socket-chat
cd socket-chat
npm install
echo node_modules > .gitignore
```
Now we need to hook up our socket middleware. Because we're using the generator our socket code needs to go in our bin -> www folder right after we create our http server. So we can type in something like this...

```js
// this first line should already be there
var server = http.createServer(app);
// This is talking about the socket.js file you're about to make
var Socket = require('../io');
Socket(server);
```

**Question:** Why did we have to hook up our socket in our www file instead of our app.js?

*The bin file is where the generator runs the http server, that is what you need access to in order to fire your sockets, otherwise in app.js you only have access to your app.*

Now create a io.js file that lives in your lib file , add this code...
```js
var Socket = require('socket.io');
module.exports=function(server){
  var io = Socket(server)
  io.on('connection', function(socket){
    console.log('Now entering the chat room');
  })
}
```
**Question:** What is happening here?

There we are actually setting up our socket! We require socket.io and set up our socket connection (io.on!)

Now that the server side of our socket is set up, let's work on the client side!

In your views folder, in layout.jade, go ahead and add your socket CDN and a connection to your main.js (in your public javascripts folder)

```html
body
  block content
  script(src='https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.js')
  script(src='/javascripts/main.js')
```

And now finally let's fire the socket function and get it running. In your main.js add
```js
var socket = io();
```

Start your nodemon, open your web tools and make sure your socket is there!

__You're Fully Set Up Now!__
