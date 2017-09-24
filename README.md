## Welcome to the Intro to Sockets!

First, go through the Socket-Intro.ipynb

Then, go through the steps outlined below.

Open up two command prompts. Activate iPython in each.

### Create a Server

In your first python interpreter, create a server socket and prepare it for connections:

```In [1]: import socket```

```In [2]: server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM, socket.IPPROTO_IP)```

```In [3]: server_socket.bind(('127.0.0.1', 50000))```

```In [4]: server_socket.listen(1)```

```In [5]: conn, addr = server_socket.accept()```

At this point, you should not get back a prompt. The server socket is waiting for a connection to be made.

### Create a Client

In your second interpreter, create a client socket and prepare to send a message:

```In [1]: import socket```

```In [2]: client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM, socket.IPPROTO_IP)```

Before connecting, keep your eye on the server interpreter:

```In [3]: client_socket.connect(('127.0.0.1', 50000))```

### Send a Message Client->Server

As soon as you made the connection above, you should have seen the prompt return in your server interpreter. The accept method finally returned a new connection socket.

When you’re ready, type the following in the client interpreter:

```In [4]: client_socket.sendall('Hey, can you hear me?'.encode('utf8'))```

### Receive and Respond

Back in your server interpreter, go ahead and receive the message from your client:

```In [6]: msg = conn.recv(4096)```

```In [7]: msg```

```Out[8]: b'Hey, can you hear me?'```

Send a message back, and then close up your connection:

```In [9]: conn.sendall('Yes, I can hear you.'.encode('utf8'))```

```In [10]: conn.close()```

### Finish Up

Back in your client interpreter, take a look at the response to your message, then be sure to close your client socket too:

```In [5]: from_server = client_socket.recv(4096)```

```In [6]: from_server```

```Out[6]: b'Yes, I can hear you.'```

```In [7]: client_socket.close()```

And now that we’re done, we can close up the server socket too (back in the server interpreter):

```In [11]: server_socket.close()```

You’ve just run your first client-server interaction!
