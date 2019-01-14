# Socket.io

## General

- WebSocket
  - Computer communications protocal which provides back-and-forth communication channels over a single TCP connection.
    - Interactive communication between browser and server
  - Provides an API for sending and receiving messages to/from event-driven responses
  - Cycle
    - Client connects to server with a handshake (HTTP upgrade)
    - Bidirectional communication between client and server
    - One side disconnects

- Socket.io is an express.js framework that creates a websocket
  - Has a server that integrates with Node.js HTTP server
  - Client library that loads on the browser side

- Setting up socket.io
  - Install module
    ```js
    npm install socket.io
    ```
  - Set up the Backend
    ```js
    var http = require('http').Server(app);
    var io = require('socket.io')(http);
    app.use('/socket-io',
      express.static('node_modules/socket.io-client/dist'));
    app.get('/', function (request, response) {
      response.render('chat.html');
    });
    io.on('connection', function(client){
      console.log('CONNECTED');
      client.on('disconnect', function () {
        console.log('EXITED');
      });
    });
    http.listen(8000, ...
    ```
  - Start the Front End
    ```html
    <script src="/socket-io/socket.io.js"></script>
    <script>
      var server = io();
      server.on('connect', function (s) {
        console.log('connected');
      });
    </script>
    ```
  - Communication (backend)
    ```js
    client.on('incoming', function(msg){
      io.emit('chat-msg', msg);
    });
    ```
  - Communcation (frontend)
    ```html
    <input id="message" onkeypress="send_message(event)">
    <pre id="chat-box"></pre>
    ```
    ```js
    server.on('chat-msg', function (msg) {
    var chat = document.getElementById("chat-box");
    chat.insertAdjacentHTML('beforeend', '\n' + msg);
    });
    function send_message (event) {
      var char = event.which || event.keyCode;
      if (char == '13') {
        var msg = document.getElementById("message");
        server.emit('incoming', msg.value);
        msg.value = '';
      }
    }
    ```
