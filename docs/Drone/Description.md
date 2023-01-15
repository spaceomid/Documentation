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

### Team
* Mr Yaghini