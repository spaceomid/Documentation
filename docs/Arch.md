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

    subgraph Domain_Layer[Domain Layer]
        style ELK fill:#d500f933;
        style ELKDrone fill:#d500f933;
        style ELKHodhod fill:#d500f933;
        style ELKSmsEmail fill:#d500f933;
        style ELKGEE fill:#d500f933;
        style ELKHodhod fill:#d500f933;
        style ELKDrone fill:#d500f933;
        style ELKFinancial fill:#d500f933;
        style ELKSOE fill:#d500f933;
        style BucketGEE fill:#00c85333
        style BucketSOE fill:#00c85333
        ELKHodhod[(ELK Hodhod)]
        BucketGEE[(Bucket GEE)]
        ELKGEE[(ELK GEE)]
        BucketSOE[(Bucket SOE)]
        ELKSOE[(ELK SOE)]
        ELK[(ELK Handler)]
        ELKFinancial[(ELK Financial)]
        ELKDrone[(ELK Drone)]
        ELKSmsEmail[(ELK Sms Email)]
    end

    Presentation_Layer -- REST --> Internet
    
    subgraph Application_Services_Layer[Application Services Layer]
        style Gateway fill:#00c85333
        style OSE fill:#00c85333
        style Financial fill:#00c85333
        style DroneBackend fill:#00c85333
        style MapDataHandler fill:#00c85333
        style HodhodServer fill:#00c85333
        style MessageSender fill:#00c85333
        style GEE fill:#00c85333
        MapDataHandler --RabbitMQ--> OSE[Space Omid Engine ]
        MapDataHandler --RabbitMQ--> GEE[Google Earth Engine ]
        MapDataHandler --RabbitMQ--> TPE[Third Party Engine ]
        GEE --> BucketGEE[(Bucket GEE)]
        OSE[Space Omid Engine ] --REST--> ELKSOE[(ELK SOE)]
        OSE --> BucketSOE[(Bucket SOE)]
        Gateway -- REST --> Financial
        Gateway -- REST --> DroneBackend[Drone Backend]
        Gateway -- REST --> MapDataHandler[Map Data Handler] 
        Gateway -- REST --> HodhodServer[Hodhod Server]
        Gateway -- REST --> MessageSender[Message Sender]   
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
        style Google fill:#00c85333
        WIFI_ReceiverTransceiver -- RADIO --> Satellite
        Satellite -- RADIO --> HodhodServer
        Internet -- REST --> WIFI_ReceiverTransceiver
        Internet -- REST --> Gateway
        MapDataHandler --REST--> ELK[(ELK Handler)]
        HodhodServer --REST--> ELKHodhod[(ELK Hodhod)]
        Financial --REST--> ELKFinancial[(ELK Financial)]
        MapDataHandler --RabbitMQ--> Publisher[Publisher]
        Publisher --ws--> Streaming_
        Streaming --ws--> Internet
        MessageSender --REST--> ELKSmsEmail[(ELK Sms Email)]
        DroneBackend --REST--> ELKDrone[(ELK Drone)]
        GEE --GRPC--> Google([Google])
        GEE --REST--> ELKGEE[(ELK GEE)]
    end
```

[Gateway](https://gateway.spaceomid.ir)
<br />
[Financial](http://financial.nobicode.ir)
<br />
[ِDrone](https://drone.spaceomid.ir/swagger)
<br />
[Message Sender](https://message-sender.spaceomid.ir/swagger)
