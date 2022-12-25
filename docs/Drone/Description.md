### Description
This project is mobile application for spraying farm landing via drone device.


### Technologies
* Xamarin
* Direct WiFi
* Flask

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