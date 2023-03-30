---
subtitle: This part will describe Socket Cluster Server
---
# socket cluster server
For this service we are using [SocketCluster](https://socketcluster.io/) and it is Dockerized and fully finctional, we just made some minor changes to fit it to our needs(will be mentioned in this page)  
in order to access it and view the code or run it change your Directory to `./socketserver`  

# How to use socket server
After running this service you need to create socket object in your clients and send connection request and Handshake(these parts are discussed in details in socket clients section)  
>#### permissions
> Every client that has access to our server can create a channel or listen to one that already exists, However to publish to a channel the client needs to have auth token and provide it in its request(to get this Token check API Reference below).  
On every connection will be print on the console so you are sure that handshake was successful.  
On every disconnection the id of the client will be printed on the console  

PN: there was some problem using the command mentioned in the original documentation for running the server with docker, the way we overcome this problem is by building and running the dockerfile manually using CMD(it is hosted on kuber, so dont need to create DockerCompose).  
the total number of connection will be printed on every new connection(wont be printed on disconnect!)



# API Renference
- In order to make a socket connection to the server read the clients documents.  
- To get the Auth token to for publisher [GET] `/jwt`


