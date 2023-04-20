---
subtitle: This part will describe Socket Cluster Client subscriber
---
# socket cluster Client
For this service we are using Nodejs for handling requests and [socketcluster-client](https://socketcluster.io/docs/api-socket-cluster-client/) for creating socket object to connect to socket server and listen on a channel(Wont have privilage to publish data on channel)  
**THIS IS FOR TEST ONLY AND SHOULD BE USED AS SAMPLE CODE TO IMPLEMENT CLIENTS!**
in order to access it and view the code or run it change your Directory to `./socketsub`  

# How socket client sub works
This part is the trickiest part that does the heavy liftings(creating channels for each client, get data grom rabit and publish it to the client that requested it, using multiThreading to handle multiple request at same time).  
it contains different files and we describe each one here:  
- `./socketsub/util`  
it has `sc.js` file that creates a socket objects and return it.    
- `./socketsub`  
In this directory 
there is only one *.js* file:  
> `server.js`  
Is used connect ot server and listen on incoming data on channel and print it  



