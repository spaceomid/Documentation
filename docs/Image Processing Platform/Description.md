### Description
This project is Web application which manage map tile and drawing operations for farming purpose.

### Diagram


``` mermaid
flowchart TB
    
    Login --Rest--> Gateway
    C[Map-Token] --Rest--> Gateway
    Gateway --Rest--> Handler
    Handler --Rabbit MQ--> A[GEE Service]
    Handler --Rabbit MQ--> B[SOE Service]

    
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
    AdminDashboard --> ImageManagement

    HomePage(User) --> Register,Auth,Login
    Register,Auth,Login --> UserDashboard
    UserDashboard --> OwnUserSearchHistory
    UserDashboard --> DrawPolygon
    DrawPolygon --> ReceiveServicesAndRelatedImages

```

### Team
* Ms. Sabahi
