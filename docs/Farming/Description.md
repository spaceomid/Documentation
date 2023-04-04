### Description
This project is Web application which assist farmer in farming operations.

### Diagram


``` mermaid
    flowchart TB
    
    subgraph Handler
        CachingTiles
    end

    Map --subscribe/channel--> SocketServer
    Map --Rest--> Gateway
    Gateway --Rest--> Handler
    Handler --Rabbit MQ--> A[GEE Service]
    Handler --Rabbit MQ--> Publisher
    Publisher --subscribe--> SocketServer    
    Publisher --publish--> SocketServer
    A[GEE Service] --Rabbit MQ--> Handler
    
``` 


### User flow

```mermaid
    stateDiagram-v2

    HomePage(Admin) --> Auth,Login
    Auth,Login --> AdminDashboard
    AdminDashboard --> UserActivityMonitoring

    HomePage(User) --> Register,Auth,Login
    Register,Auth,Login --> UserDashboard
    UserDashboard --> AccessToHistoryOfResults
    UserDashboard --> DrawPolygon


```

### Technologies

* :simple-django:{.grey} Django
* :simple-react:{.grey} React


### Team
* Ms. Moradi
* Mr. TalebElm