# Upload documentation  

This documentation provides information about upload center that its goal is to replace ArvanCloud bucket and serve as upload center, Meaning it can recieve files(Images, Videos, ...) and got access for download.  
PN: Right now there is no restrion on data types and file size.  

## **Technologies Used in Project**  
* **Node.js**
* **Express.js**
* **Mutler**
* **Cors**
* **Docker**

# **Getting Started**  
You can use `npm server.js` or `node server.js` commands(make sure you are in the same directory as server.js) to run the service in local mode and test, However, the docker image is avaiable and should be used for production mode.  

## **General WorkFLow of the Project**  
* There are three api references for uploading files, getting the list of uploaded files and downloading the file(Check API reference part).  

# **Project Structure and WorkFlow**  
Different folders in the project will be described here by the order that they receive and proccess the File:  
* **middleware**  
this part contains `upload.js` file that is responsible for configuring multer and saving the file in the fileserver  
* **controller**  
this part contains `file_upload_controller.js` file that is responsible for handling errors and functions that are responsible for serving the routes  
* **routes**  
this part contains `routes.js` file that is responsible for routes and mthods(POST, Get) and calls`file_upload_controller.js` methods on the URL  


## **General API Reference**  
**Last Update: 5/21/2023**  
Upload a file:  
[POST] `/upload`  
Get list of stored files with respective links:  
[GET] `/files`  
Download a file:  
[GET] `/files/:name`  