# faux_twitter
This is an application that mimics all of twitter features

The code is written in FSharp and uses F# actors.

Running the application:
Server part: run in an IDE. I have used Jetbrains Rider v 2020.3
Client part: I have designed a simple HTML based User Interface with bootstrap CSS to mimic a twitter
application. Open the ‘UI.html’ file in any browser, preferably Chrome or Mozilla FireFox.

Implementation:
Rest API:
I was able to achieve the rest services required as a part of this project using the package “suave.io ”.
There are 2 types of requests, one is the POST requests that accepts requests like ‘/register’, ‘/login’,
‘/logout’, ‘/newtweet’, and ‘/follow’ which are sent by the HTML file to the backend F# file in order to
fetch data from the API and performs said operations. The other type of requests the server accepts is a
GET request which accepts requests like ‘/gettweets/%s’, ‘/getmentions/%s’, ‘/gethashtags’. As soon as
the server receives any of these requests, it starts delegating work to the other functions and actors
accordingly as per the request.

The Application works in the following order of steps:
1. Initially, we start the server on an IDE and then open the client in a browser and when a client
successfully logs in to the server, a WebSocket connection is initiated by the client with “/websocket”
URL request.
2. As soon as the server accepts this request, the client and server will start exchanging handshake
messages and the client will send its username and password through the WebSocket to the server which
is validated there.
3. Once these details are received by the server through websocket, the server then stores a WebSocket
reference with the client id.
4. Whenever actor needs to push a live update to the client, it picks the necessary WebSocket address and
puts message to client on WebSocket.
5. On client side when it receives a message from server via WebSocket it displays to the user in activity
monitor tab.
