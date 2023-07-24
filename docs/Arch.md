# Project Architecture




``` mermaid
flowchart TB
    
    classDef Elk fill:#d500f933;
    
    style Gateway fill:#00c85333
    style Streaming fill:#448aff,stroke-width:4px,color:#fff
    style Streaming_ fill:#448aff,stroke-width:4px,color:#fff
    
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
    MapDataHandler --RabbitMQ--> Publisher[Publisher]
    Publisher --ws--> Streaming_
    Streaming --ws--> Internet

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

``` mermaid
flowchart LR

    subgraph Presentation_Layer[Presentation Layer]
        subgraph Web
            Map
            DataGatheringDashboard[Data Gathering Dashboard]
        end
        subgraph Mobile
            Drone
            MessengerApp
        end
    end

    Presentation_Layer -- REST --> Internet
    
    subgraph Application_Services_Layer[Application Services Layer]
        style Gateway fill:#00c85333
        style Financial fill:#00c85333
        style DroneBackend fill:#00c85333
        style MapDataHandler fill:#00c85333
        style HodhodServer fill:#00c85333
        style MessageSender fill:#00c85333
        Gateway -- REST --> Financial
        Gateway -- REST --> DroneBackend[Drone Backend]
        Gateway -- REST --> MapDataHandler[Map Data Handler] 
        Gateway -- REST --> HodhodServer[Hodhod Server]
        Gateway -- REST --> MessageSender[Message Sender]   
    end
    
    subgraph Domain_Layer[Domain Layer]
        style ELK fill:#d500f933;
        style ELKDrone fill:#d500f933;
        style ELKHodhod fill:#d500f933;
        style ELKSmsEmail fill:#d500f933;
        style ELKGEE fill:#d500f933;
        style ELKHodhod fill:#d500f933;
        style ELKDrone fill:#d500f933;
        ELK[(ELK)]
        ELKDrone[(ELK Drone)]
        ELKHodhod[(ELK Hodhod)]
        ELKSmsEmail[(ELK Sms Email)]
        ELKGEE[(ELK GEE)]
    end
    
    subgraph Infrastructure_Layer[Infrastructure Layer]
        style WIFI_ReceiverTransceiver fill:#00c85333
        subgraph WIFI_ReceiverTransceiver[WIFI and Receiver Transceiver]
        subgraph Modem
        DataGatheringHW
        MessengerHW
        end
        end
        style Modem fill:#00c85333
        style DataGatheringHW fill:#00c85333
        style MessengerHW fill:#00c85333
        style Satellite fill:#00c85333
        style GEE fill:#00c85333
        style Google fill:#00c85333
        style BucketGEE fill:#00c85333
        style OSE fill:#00c85333
        WIFI_ReceiverTransceiver -- RADIO --> Satellite
        Satellite -- RADIO --> HodhodServer
        Internet -- REST --> WIFI_ReceiverTransceiver
        Internet -- REST --> Gateway
        MapDataHandler --> ELK
        MapDataHandler --RabbitMQ--> OSE[Omid Space Engine ]
        MapDataHandler --RabbitMQ--> GEE[Google Earth Engine ]
        MapDataHandler --RabbitMQ--> TPE[Third Party Engine ]
        MapDataHandler --RabbitMQ--> Publisher[Publisher]
        Publisher --ws--> Streaming_
        Streaming --ws--> Internet
        HodhodServer --REST--> ELKHodhod[(ELK Hodhod)]
        MessageSender --REST--> ELKSmsEmail[(ELK Sms Email)]
        DroneBackend --REST--> ELKDrone[(ELK Drone)]
        GEE --GRPC--> Google([Google])
        GEE --> ELKGEE[(ELK GEE)]
        GEE --> BucketGEE[(Bucket GEE)]
    end
```

[Gateway](https://gateway.spaceomid.ir)
<br />
[Financial](http://financial.nobicode.ir)
<br />
[ِDrone](https://drone.spaceomid.ir/swagger)
<br />
[Message Sender](https://message-sender.spaceomid.ir/swagger)
