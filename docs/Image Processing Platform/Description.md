### Description
This project is Web application which manage map tile and drawing operations for farming purpose.

### Diagram


``` mermaid
flowchart TB
    
    Map --Rest--> Gateway
    Gateway --> Handler
    Handler --Rabbit MQ--> A[GEE Service]

    
``` 

### Technologies

* :simple-django:{.grey} Django
* :simple-react:{.grey} React



### User flow

```mermaid
    stateDiagram-v2

    HomePage(Admin) --> Auth,Login
    Auth,Login --> AdminDashboard
    AdminDashboard --> UsersSearchHistory

    HomePage(User) --> Register,Auth,Login
    Register,Auth,Login --> UserDashboard
    UserDashboard --> OwnUserSearchHistory
    UserDashboard --> DrawPolygon


```

### Team
* Ms. Sabahi
