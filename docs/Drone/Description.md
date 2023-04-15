### Description
The drone system is responsible for managing the drones flight, the drones data and spraying teams.

### Diagram


``` mermaid
flowchart TB
    
    classDef Elk fill:#d500f933;
    
    style Gateway fill:#00c85333
    
    subgraph Internet
    
    subgraph Mobile
    Drone
    end
    
    end
    
        
    subgraph Firewall
    Gateway
    end
    
    Internet --Rest--> Gateway
    Gateway --Rest--> Financial
    Gateway --Rest--> DroneBackend[Drone Backend]
    
``` 


### Technologies

* :simple-xamarin:{.grey} MAUI
* :material-wifi-sync:{.grey} Direct WiFi
* :material-dot-net:{.grey} .net core

### Database

* :simple-elastic:{.grey} ElasticSearch

### Sub Project

* Drone (Mobile-Frontend). Implement via `MAUI`
* Drone server (Backend). Implement via `.net core`

### Mobile App

The mobile app is installing on the radio controller and consists of two parts, `mission` and `operation`

In the mission part, define the mission of the drone, including the scope of agricultural land, the scope of the barriers(`Add point`, `Delete Point`).
And the drone `settings` include height, spray width, pump efficiency, poison amount, poison flow rate, speed and height of returning home and the necessary explanations for this mission.
And by doing the `processing`, the mission, drone speed and the optimal path of the drone will be determined.
After this, if the pilot wants, he can manually change the angle of the drone's movement path.
And then the set mission template is `saved` and send to `drone backend` for storage.

In the operation part, the drone is connecting to the application, and after selecting the saved mission template and `sending` it to the drone, by sending the `start` command from the application, the spraying flight of the drone starts.
And in real time, the data of the `drone status` is sent to the application through wifi connection and mavlink protocol and it is shown on the operation page.
And by sending the `stop` command from the application, the drone returns to the home point.

On the `main page`, the saved mission `templates` can be `deleted`, viewed and selected for `editing` on the mission page and `open` for sending to the drone on the operation page.

On the registry page, by sending the mobile number and password to `gateway`, the token is sent to the user, and the imei code together with token is sent to the `Financial`.
And if the user subscribes to the drone application, the license will be sent to the app, and the user will enter the `main page` by restarting the application.

If the drone exits the auto mode during operation, the rest of the mission is `saved` and after the drone returns home to solve the problem, including charging the battery and filling the poison tank, by `sending the rest` of the mission from the application and the command to `start`, the drone for Carrying out the rest of the mission flies

### Drone Backend



### User flow
``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
  MainPage --> fork_state
  fork_state --> Mission
  fork_state --> Operation

  Mission --> Process
  Mission --> AddPoint
  Mission --> DeletePoint
  Mission --> Setting
  Operation --> Send
  Operation --> DroneStatus
  Operation --> Start
  Operation --> Stop

  state join_state <<join>>
  Mission --> join_state
  Operation --> join_state
  join_state --> Templates
  Templates --> Save
  Templates --> Open
  Templates --> Delete
```

### Team
* Mr Yaghini