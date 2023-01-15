### Description
This project is mobile application for spraying farm landing via drone device.

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
    
    Internet --> Gateway
    Gateway --> Financial
    Gateway --> DroneBackend[Drone Backend]
    
``` 


### Technologies

* :simple-xamarin:{.grey} Xamarin
* :simple-flask:{.grey} Direct WiFi
* :simple-flask:{.grey} Flask
* :simple-react:{.grey} React
* :material-dot-net:{.grey} .net core
* :simple-django:{.grey} Django

### Sub Project

* Drone (Mobile-Frontend). Implement via `Xamarin`
* Drone server (Backend). Implement via `.net core`

### Database
* :simple-elastic:{.grey} ElasticSearch

### Diagram
``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
  Connection --> fork_state
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