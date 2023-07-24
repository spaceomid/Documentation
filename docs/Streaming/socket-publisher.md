---
subtitle: This part will describe Socket Cluster Client publisher
---
# socket cluster Publisher
For this service we are using Flask for handling requests and [socketcluster-client-python](https://github.com/sacOO7/socketcluster-client-python) for creating socket object to connect to socket server and publish data and creating channels(sending requests for creating channels both for clients and Rabbit service).  
in order to access it and view the code or run it change your Directory to `./socketpub`  

# How socket client publisher works
This part is the trickiest part that does the heavy liftings(creating channels for each client, get data grom rabit and publish it to the client that requested it, using multiThreading to handle multiple request at same time).  
it contains different files and we describe each one here:  
- `./socketpub/util`  
it has `sc.py` file that creates a socket objects(take an argument Delay):  
*Delay* is the number of seconds that it waits for server to response(it also tries to connect each second meaning if you set Delay to 10 it will try to connect to server 10 times in 10 seconds).  
`socketServerAdd = os.getenv("SOCKET_SERVER_ADD", 'localhost')` and `socketServerPort = os.getenv("SOCKET_SERVER_PORT", '8000')` are server address and port respectively, first check for env variabled(in docker or kuber) if didnt provided(like in local test) use default values.  
The `connect_to_socket_server_multithread` function is used to have multiple objects for handling more request, it uses multi threading and has two arguments, *Delay* and *max_connection* that will specify number of objects that we need  
- `./socketpub`  
In this directory we have three *.py* file and one docker file:  
> `connection.py`  
Is used to connect to RabbitMQ  
> `reciever.py`  
Is used to handle RabbitMQ Events  
> `app.py`  
Is the main flask app that contains routes(check the API renference for more information).  




# API Renference 
- To Check if publisher is working [GET] `/`
- To create a Channel with clientID name so client can listen on it and publisher send data over it for that client [POST] `/v1/create-channel-client`
- To tell flask to generate fake data [GET] `/v1/publish-data-over-ch` **TEST ONLY**
- To create a Channel to listen for Rabbit [GET] `/v1/create-rabbit-ch` **DEPRICATED**


