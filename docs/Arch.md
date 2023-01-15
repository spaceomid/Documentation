# Project Architecture




``` mermaid
flowchart TB
    
    classDef Elk fill:#d500f933;
    
    style Gateway fill:#00c85333
    style Streaming fill:#448aff,stroke-width:4px,color:#fff
    
    subgraph Internet
    
    subgraph Web
    Map
    end
    
    subgraph Mobile
    Drone
    end
    
    end
    
        
    subgraph Firewall
    Gateway
    end
    
    Internet --REST--> Gateway
    Gateway --REST--> Financial
    Gateway --REST--> DroneBackend[Drone Backend]
    Gateway --REST--> MapDataHandler[Map Data Handler]     
        
    MapDataHandler --> ELKHandler[(ELK Handler)]:::Elk
    MapDataHandler --RabbitMQ--> OSE[Omid Space Engine ]
    MapDataHandler --RabbitMQ--> GEE[Google Earth Engine ]
    MapDataHandler --RabbitMQ--> TPE[Third Party Engine ]
    
    
    DroneBackend --REST--> ELKDrone[(ELK Drone)]:::Elk
     
    subgraph G.E.E.
    GEE
    Google
    BucketGEE
    ELKGEE
    end
    
    GEE --GRPC--> Google([Google])
    GEE --> ELKGEE[(ELK GEE)]:::Elk
    GEE --> BucketGEE[(Bucket GEE)]
    
    
    subgraph O.S.E.
    OSE
    end
    
``` 
