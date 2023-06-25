# Chatbot documentation  

This documentation provides information about Chatbot project that its goal is to provide human like conversation and suggestion with users. right now it is using GPT but its not limited to. 

## **Technologies Used in Project**  
* **FastAPI**
* **ElasticSearch**
* **openai**

# **Getting Started**  
In order to run the service in local mode use `uvicorn main:app --reload` command. the project has docker file that uses gunicorn with uvicorn worker

## **General WorkFLow of the Project**  
* There are one api references that can be used to ask question(ask question with json and get response as json)   

# **Project Structure and WorkFlow**  
first we talk about Util and Models folders and then about files in root directory of the project:  
* **Util**  
This folder contains `elastic_connection.py` file with has the credentials of elastic
* **Models**  
This part contains `chat_model.py` and `elastic_crud.py` files:  
* ***chat_model.py***  
this module defines a ChatInfo Pydantic model with two fields, user_id and prompt. It also defines a Chat_Model class with an initializer that takes in three arguments: user_id, prompt, and date_time.  

The document method of the Chat_Model class returns a dictionary containing the values of the user_id, prompt, and date_time attributes.  

this code creates a data structure to represent chats in chat application. The ChatInfo model is used to validate input data before creating a new chat instance using the Chat_Model class. The document method is used for serializing the chat object into a dictionary that can be stored in elastic and also can be transmitted over a network.    
* ***elastic_crud.py***  
This code defines an ElasticManager class that provides methods to interact with Elasticsearch. The initializer establishes a connection to Elasticsearch and prints a message to indicate successful connection.  

The `insert` method takes in user_id, prompt, and date_time parameters and creates a new document using the Chat_Model class. The document method of the Chat_Model class is called to serialize the chat object into a dictionary that can be passed to the index method of the Elasticsearch client to store the document in an index. The index name can be overridden by passing the index parameter to the method. The method returns the result of the indexing operation.  

The `search` method takes in a query parameter as a dictionary and performs a search operation on the specified index using the search method of the Elasticsearch client. The index name can also be overridden by passing the index parameter to the method. The method returns the search results as a dictionary.  
this code is trying to create an interface to interact with Elasticsearch for storing and searching chats represented by instances of the Chat_Model class. The ElasticManager class allows for easy integration with Elasticsearch, abstracting away some of the complexities of the Elasticsearch API and making it easier to work with.  

* Now its time for root files
* **main.py**  
This script is a Python code that uses OpenAI's GPT-3.5 to generate a response for a given prompt. The conversation history of each user is stored in an Elasticsearch instance using the ElasticManager class from the Models.elastic_crud module.  

The script first loads the API key for OpenAI from an environment variable and sets it as the default API key for the openai package. It also initializes the conversation_history dictionary.  

The generate_response() function takes a prompt, user_id, and other optional parameters as input. It then searches for any previous messages by calling the get_user_all_questions() function, retrieves the user's conversation history and appends the new prompt to the context. A request is then sent to OpenAI to generate a response using the context and returns the generated text.  

The get_user_all_questions() function retrieves all previous questions asked by a user from Elasticsearch and stores them in a list. The list is then returned to the calling function after updating the global conversation_history dictionary.  

Finally, the add_question_to_user_history() function appends the new prompt to the user's conversation history in Elasticsearch along with the current timestamp. The updated conversation_history dictionary is then returned to the calling function.  

Overall, this code provides the functionality to generate responses from OpenAI's GPT-3.5 model while keeping track of a user's conversation history using Elasticsearch.  
* **server.py**  
This code provides a simple FastAPI server that exposes an endpoint at /ask-gpt. When this endpoint is called with a valid JSON payload containing a user_id and a question, it generates a response to the question using OpenAI's GPT-3.5 model by calling the generate_response() function from the main module.  

The health_check() function provides a simple GET endpoint at / for checking if the service is running. This function returns a dictionary with a "message" key indicating that the logging service is running.  

The ask_gpt() function listens for POST requests at /ask-gpt. It takes in a Request object containing a JSON payload via the info parameter. The JSON payload should contain a user_id and a question. If these parameters are present, the function retrieves them and passes them as arguments to the generate_response() function. A prompt is constructed from the user's question, and OpenAI's API is called to generate a response.  

If the response is successfully generated, it is returned as a JSON object containing a "response" key. If there is an error generating the response, a dictionary is returned with a "message" key containing the error message.  

Overall, this code provides a simple way to integrate OpenAI's GPT-3.5 model into a FastAPI application for generating responses to user queries.  


## **General API Reference**  
**Last Update: 5/21/2023**  
Health Check:  
[get] `/`  
Ask Question from GPT:   
[POST] `/ask-gpt`