Sure, here's your formatted `README.md` file with styling:

```markdown
# Socket.io Cheatsheet

## Server-side

```javascript
io.on("connection", (socket) => {

  // Basic emit
  socket.emit(/* ... */);

  // To all clients in the current namespace except the sender
  socket.broadcast.emit(/* ... */);

  // To all clients in room1 except the sender
  socket.to("room1").emit(/* ... */);

  // To all clients in room1 and/or room2 except the sender
  socket.to("room1").to("room2").emit(/* ... */);

  // To all clients in room1
  io.in("room1").emit(/* ... */);

  // To all clients in namespace "myNamespace"
  io.of("myNamespace").emit(/* ... */);

  // To all clients in room1 in namespace "myNamespace"
  io.of("myNamespace").to("room1").emit(/* ... */);

  // To individual socketid (private message)
  io.to(socketId).emit(/* ... */);

  // To all clients on this node (when using multiple nodes)
  io.local.emit(/* ... */);

  // To all connected clients
  io.emit(/* ... */);

  // WARNING: `socket.to(socket.id).emit()` will NOT work, as it will send to everyone in the room
  // named `socket.id` but the sender. Please use the classic `socket.emit()` instead.

  // With acknowledgement
  socket.emit("question", (answer) => {
    // ...
  });

  // Without compression
  socket.compress(false).emit(/* ... */);

  // A message that might be dropped if the low-level transport is not writable
  socket.volatile.emit(/* ... */);

});
```

## Client-side

```javascript
// Basic emit
socket.emit(/* ... */);

// With acknowledgement
socket.emit("question", (answer) => {
  // ...
});

// Without compression
socket.compress(false).emit(/* ... */);

// A message that might be dropped if the low-level transport is not writable
socket.volatile.emit(/* ... */);
```

## Reserved Events

On each side, the following events are reserved and should not be used as event names by your application:

- connect
- connect_error
- disconnect
- disconnecting
- newListener
- removeListener

```javascript
// BAD, will throw an error
socket.emit("disconnecting");
```
```

