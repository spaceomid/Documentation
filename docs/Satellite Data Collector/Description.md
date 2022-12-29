### Description

This project is mobile application for collect data from mobile app. and send to satellite.
you can use this application to monitor your logging data and change default settings in place or monitor logged data in any remote place using internet connection.

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

            state Client_state <<fork>>
            Client --> Client_state
            Client_state --> App
            Client_state --> Device


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

            Device --> Communicator_Collector
            state Communicator_Collector_state <<fork>>
            Communicator_Collector --> Communicator_Collector_state
            Communicator_Collector_state --> Connection_to_Sensors
            Communicator_Collector_state --> Wifi_Setting
            Communicator_Collector_state --> GPS
            Communicator_Collector_state --> SD_Card
            Communicator_Collector_state --> Direct_Communication_to_Satellite

    ```

### Feature List

1.  Authentication
    -   User Managment system for Login, Register,... or any synchronization between services
2.  Communication over wifi
    -   using wifi protocol and http as communication between device and phone
3.  Data Logging
    - log data to satellite and user phone in place
4.  Change device default setting
5.  ...

### Team

-   Mr. Zarei
