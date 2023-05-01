---
subtitle: This part will Describe how to run the load test and see the results
---
# Load Test Documentation  

This documentation provides information about how to run load tests and save them database and also see the results  


## **Technologies Used in Project**  
* **K6.io**
* **Grafana**
* **InfluxDb**
* **Docker**

# **Getting Started**  
In order to see the test results in dashboard you need to run InfluxDb and Grafana(they are dockerized and ready to use, just need to build and run them) beforehand, However, for running the tests they are not necessary and you can check the results in terminal that you run the the tests(actually the terminal result is more detailed).  
Tests are written in scenario based structure and in order to findout how they work and modifing them check the official document [here](https://k6.io/)

## **General WorkFLow of the Project**  
After running inial commands in terminal(described in detail later in this this page), you device will increase the load on the target service and at the end of test you can see the result in the terminal and in Grafana dashboard(IF YOU ENABLED IT!)  


## **Command Reference**  
**Last Update: 4/24/2023**  
JUST MAKE SURE YOU ARE IN THE SAME DIRECTORY AS THE LOAD TEST FILE IS!  
To run the test locally(Not sending results to database):  
`k6 run Load-Test.js` (Change the Load-Test.js to name of the loadtest file you want!)  
To the test and send the result to database for dashboard  
`k6 run --out influxdb=Grafana-server-address Load-Test.js`(Change the Load-Test.js to name of the loadtest file you want!)  
## **Running InfluxDb and Grafana dashboar services**  
**For running InfluxDb and Grafana dashboard**  
IF THE DASHBOARD IS RUNNING JUST NAVIGATE TO YOUR GRAFANA HOME PAGE AND GO TO THE DASHBOARD SECTION!  
`SERVER-ADDRESS:3000/`  
IF YOU WANT TO SETUP THE DASHBOARD FOLLOW THE INSTRUCTION.  
You can access the latest configs from `git clone https://github.com/grafana/k6 && cd k6`. It Contains all the files and examples, However the file you need is the docker compose that is described Here:  

``` yaml
version: '3.4'

networks:
  k6:
  grafana:

services:
  influxdb:
    image: influxdb:1.8
    networks:
      - k6
      - grafana
    ports:
      - "8086:8086"
    environment:
      - INFLUXDB_DB=k6

  grafana:
    image: grafana/grafana:latest
    networks:
      - grafana
    ports:
      - "3000:3000"
    environment:
      - GF_AUTH_ANONYMOUS_ORG_ROLE=Admin
      - GF_AUTH_ANONYMOUS_ENABLED=true
      - GF_AUTH_BASIC_ENABLED=false
    volumes:
      - ./grafana:/etc/grafana/provisioning/
```
Now, we will use the above docker-compose.yml to set up influxdb and Grafana in our instance using docker-compose, as seen in the YAML file we are using influxdb version 1.8 and have mapped container port 8086 with the host port for influxdb and our database name is k6. Similarly, for Grafana we will be running on port 3000.  
Run the below command which will pull in all the applicable docker images and set up our containers using docker-compose.  
`docker-compose up -d influxdb grafana`(-d is for detach mode, to see the output without -d!)  

**Access the Grafana dashboard from the browser**  
Now its time to connect to the server that is runnig Grafana service from browser(Find the IP Address):  
`SERVER-ADDRESS:3000/login`  
???+ Default-User-And-Pass

    Username: admin  
    Password: admin

Navigate to the URL: `SERVER-ADDRESS:3000/datasources`  
When you open the data source you can view the details, here You can verify the URL and database name which was configured in the YAML file.  
Post running this k6 run command, You set of results will be pushed to the influxdb database called k6, now in order to visualize Your run results we can configure a Grafana dashboard using the below steps:  
1. Navigate to your Grafana home page and go to the Dashboard section
2. Under New, select the import option
3. In the Import page, we will use ID: 2587 which is a pre-configured dashboard available for k6 load tests in Grafana. For more information, you can refer to this [Link](https://grafana.com/grafana/dashboards/2587-k6-load-testing-results/)
4. In next page, we can add 2587 in the textbox and click Load button.
5. Finally, select the source as “myinfluxdb (Default)” option and click on the Import button which will load up our dashboard.  


**Results**  

???+ 5-1-2023

    GateWay:  
      Signup:  
        390 Concurrent User  
      SignIn(In 90 Seconds Duration):  
        100  
      Resources:  
        PostgreSQL:  
          CPU: 1Core  
          RAM: 2GB  
        GateWay:  
          CPU: 1Core  
          RAM: 1GB  
      
    Drone:  
    80 is OK  
    Resources:  
      Financial:  
        CPU: 1Core  
        RAM: 1GB  

      
    WebSocket:  
      Both socket server and Socket publisher had 1GB of Ram and 1Core CPU
      Because of async nature of node.js and FastAPI didn’t break even at 1 million requests!
      Publish rate (with API call and not rabbit) was between 100-150.
      Publish rate With RabbitMQ More than 2000.

