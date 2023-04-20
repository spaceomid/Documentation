# Socket cluster server and client documentation  

``` mermaid
graph LR
  A[RabbitMQ] -->|PushdData| B{Publisher};
  B -->|publish-data-on-channel| C[Socket-Server];
  C -->|Listen-on-channel| D[Client(Web,Mobile)];
```


This documentation provides information about socket cluster server and clients(both publisher and subscriber).  
there is also a README.md file available to this project for quick reference.  

# **SocketCluster server and clients(Publisher)**  
These three services are  designed in a way to create channel between RabbitMQ and clients so they can have realtime data exchange

## **Technologies Used in Project**  
* **SocketCluster**
* **Node.js**
* **flask**
* **Docker**

# **Getting Started**  
Since the project is using Docker and placed on kubernetes, the images contain all required libraries and dependencies and you just need to have Docker installed(all three services are capable of running in local mode without docker too), however, if you want to run each part separately or outside docker, you need to make sure these items are installed on your machine:  
1. Node.js
2. Docker
3. python  
For flask check the requierments file and install them(inside Venv)  
for nodejs just type 'npm install'  

## **General WorkFLow of the Project**  
* When all services are up and running, you should send a request to publisher(flask) service to create a channel to RabbitMQ service and listen on it for incoming data:   
>this can be done through `/v1/create-rabbit-ch`.  

* Then you need to send request from sub client(s) to publisher(flask) service to create a channel for that client with its clientID **(request POST method and send json)**
> this can be done through `/v1/create-channel-client`.
you need to include JSON Body that contains name, email, password  
* After last two steps the publisher will share Rabbit data via channel to the user that requested it
* **PN: the socketsub service is for test porpuses only and shouldn`t be used in production!**

## **General API Reference**  
**Last Update: 3/13/2023**  
only should be called once in the project startup:  
[GET] `/v1/create-rabbit-ch`  
should be called by client and contains JSON file wiht Client id:  
[POST] `/v1/create-channel-client`  
**ONLY SHOULD BE USED IN TEST MODE TO GENRATE FAKE DATA!**:  
[GET] `/v1/publish-data-over-ch`  
is a way to make sure publisher(flask) service is up and running and responsive:  
[GET] `/`  

<!-- ## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files. -->
