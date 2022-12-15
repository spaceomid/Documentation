### Description

This project is mobile application for communication purpose.
Messenger app that you can use it when you can't connect to the internet network in emergency situations or ...

### Technologies

-   Javascript, Typescript
-   React, React Native
-   Expo

!!! HodHod_Project_Sructure info

    ``` mermaid
        stateDiagram-v2
            state fork_state <<fork>>
            HodHod --> fork_state
            fork_state --> Client
            fork_state --> Server
            fork_state --> Satellite

            Client --> App
            Client --> Device

            App --> Data_Collector
            App --> Communicator

            state Communicator_state <<fork>>
            Communicator --> Communicator_state
            Communicator_state --> Login,Register,Auth
            Communicator_state --> Communication_over_wifi_to_device
            Communicator_state --> Save,Edit,ShowStatus_messages
            Communicator_state --> Create,Edit,Delete,Update_chats

            state Data_Collector_state <<fork>>
            Data_Collector --> Data_Collector_state
            Data_Collector_state --> Login,Register,Auth
            Data_Collector_state --> Communication_over_wifi_to_device
            Data_Collector_state --> Data_Logger
            Data_Collector_state --> Setting
    ```

### Feature List

-   Authentication
-   Communication over wifi
-   Messenger features
-   Change device default setting
-   ...

### Team

-   Mr. Zarei
