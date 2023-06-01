# log documentation  

This documentation provides information about log service which is designed to store error logs from different services in elastic that later can be retrieved.  

## **Technologies Used in Project**  
* **FastAPI**
* **Elasticsearch**

# **Getting Started**  
In order to run the service in local mode use `uvicorn main:app --reload` command. the project has docker file that uses gunicorn with uvicorn worker

## **General WorkFLow of the Project**  
* There are three API reference that can be used for working with elastic, one can be used to create new index(right now it is using default index name that is specified in the code and is not adviced to change it!) the other two can be used to save errors in the elatic on the default index(one would get id to store in elastic and the other let elastic auto id generate PN:latter API is suggested!) 

# **Project Structure and WorkFlow** 
The `main.py` contains all the routes and functions that use below files   
* **util**  
Contains elastic connection information
* **models**  
It has two main file:  
1. `async_elastic.py`: This file containt elastic functions that will be used in the project to interact with elastic  
1. `error_model.py`: This file contains model that specifies the error model  




## **General API Reference**  
**Last Update: 5/21/2023**  
Check if the service is Runnig:  
[GET] `/`  
to create new index(get index name as json):  
[POST] `/create-index`  
to insert new document with specified id:  
[POST] `/inser-doc-with-id`  
to insert new document(Use this!):  
[POST] `/inser-doc`  