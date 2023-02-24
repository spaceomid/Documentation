# Project Architecture




``` mermaid
flowchart TB
    
    classDef Elk fill:#d500f933;
    
    style Gateway fill:#00c85333
    style Streaming fill:#448aff,stroke-width:4px,color:#fff
    
    subgraph Internet
    
    subgraph Web
    Map
    DataGatheringDashboard[Data Gathering Dashboard]
    end
    
    subgraph Mobile
    Drone
    MessengerApp
    end
    
    end

    subgraph Firewall
    Gateway
    end
    
    subgraph WIFI_ReceiverTransceiver[WIFI and Receiver Transceiver]
    subgraph Hardware
    subgraph Modem
    DataGatheringHW
    MessengerHW
    end
    end
    end

    subgraph Satellite
        SatelliteHardware[Satellite Hardware]
    end

    WIFI_ReceiverTransceiver --RADIO--> Satellite
    Satellite --RADIO--> HodhodServer

    Internet --REST--> WIFI_ReceiverTransceiver

    Internet --REST--> Gateway

    Gateway --REST--> Financial
    Gateway --REST--> DroneBackend[Drone Backend]
    Gateway --REST--> MapDataHandler[Map Data Handler] 

    Gateway --REST--> HodhodServer[Hodhod Server]
    Gateway --REST--> MessageSender[Message Sender]   

    MapDataHandler --> ELKHandler[(ELK Handler)]:::Elk
    MapDataHandler --RabbitMQ--> OSE[Omid Space Engine ]
    MapDataHandler --RabbitMQ--> GEE[Google Earth Engine ]
    MapDataHandler --RabbitMQ--> TPE[Third Party Engine ]

    HodhodServer --REST--> ELKHodhod[(ELK Hodhod)]
    MessageSender --REST--> ELKSmsEmail[(ELK Sms Email)]
    
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

[Gateway](https://gateway.spaceomid.ir)
<br />
[Financial](http://financial.nobicode.ir)
<br />
[ِDrone](https://drone.spaceomid.ir/swagger)
<br />
[Message Sender](https://message-sender.spaceomid.ir/swagger)
