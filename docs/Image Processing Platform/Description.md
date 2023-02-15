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

### Detailed Design

* `Handler`

:   First State : The requested data(black polygon) places completely in one of the available data(white polygon).

    <figure markdown>
        ![image info](./first_state.PNG){ width="200" }
    <figcaption>First State</figcaption>
    </figure>


:   Second State : The requested data(black polygon) intersects with one of the available data(white polygon).

    <figure markdown>
        ![image info](./second_state.PNG){ width="200" }
    <figcaption>Second State</figcaption>
    </figure>

:   Third State : The requested data(black polygon) surrounds one of the available data(white polygon).

    <figure markdown>
        ![image info](./third_state.PNG){ width="200" }
    <figcaption>Third State</figcaption>
    </figure>

:   Forth State : The requested data(black polygon) surrounds multiple available data(white polygon).

    <figure markdown>
        ![image info](./forth_state.PNG){ width="200" }
    <figcaption>Forth State</figcaption>
    </figure>

:   Fifth State : The requested data(black polygon) surrounds and intersects with multiple available data(white polygon).

    <figure markdown>
        ![image info](./fifth_state.PNG){ width="200" }
    <figcaption>Fifth State</figcaption>
    </figure>

:   Sixth State : The requested data(black polygon) intersects with multiple available data(white polygon) -> It's like the.

    <figure markdown>
        ![image info](./sixth_state.PNG){ width="200" }
    <figcaption>Sixth State</figcaption>
    </figure>




### Technologies

* :simple-django:{.grey} Django
* :simple-react:{.grey} React



### User flow

```mermaid
    flowchart TB

    E[HomePage-Admin] --> Auth,Login
    Auth,Login --> AdminDashboard
    AdminDashboard --> H[Users Search History]
    AdminDashboard --> ImageManagement

    F[HomePage-User] --> Register,Auth,Login
    Register,Auth,Login --> UserDashboard
    UserDashboard --> G[Own User Search History]
    UserDashboard --> I[Draw Polygon]
    I --> D[Receive Services and Related Images]

```

### Team
* Ms. Sabahi
