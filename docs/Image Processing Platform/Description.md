### Description
This project is Web application which manage map tile and drawing operations for farming purpose.


### Technologies

* Django
* React

### Diagram

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
