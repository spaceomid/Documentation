# Project Architecture




``` mermaid
flowchart TB
    
    classDef Aero fill:#d5000033;
    classDef Elk fill:#d500f933;
    classDef cplus fill:#00c85333;
    
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
    
    Internet --> Gateway
    Gateway --> Financial
    Gateway --> DroneBackend[Drone Backend]
    Gateway --> MapDataHandler[Map Data Handler]     
        
    MapDataHandler --> ELKHandler[(ELK Handler)]:::Elk
    MapDataHandler --> OSE[Omid Space Engine ]
    MapDataHandler --> GEE[Google Earth Engine ]
    MapDataHandler --> TPE[Third Party Engine ]
    
    
    DroneBackend --> ELKDrone[(ELK Drone)]:::Elk
     
    subgraph G.E.E.
    GEE
    Google
    BucketGEE
    ELKGEE
    end
    
    GEE --> Google([Google])
    GEE --> ELKGEE[(ELK GEE)]:::Elk
    GEE --> BucketGEE[(Bucket GEE)]
    
    
    subgraph O.S.E.
    OSE
    end
    
``` 
