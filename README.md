# <ins>A Guide to making new view functions </ins>
This a guide on Django Workflow for the SSE Project, it contains a basic Django workflow for this project.



##  <ins>Where should View Functions be made?<ins/>

### Generally, you will be making a new view function in these 3 files:

<img width="398" alt="Screenshot 2025-04-07 at 10 48 56 AM" src="https://github.com/user-attachments/assets/2b2618f3-5601-4120-811c-f3197321bfa0" />

####  <ins>user_services: <ins/>
##### All functions in this file are related to user services, such as:
- Creating new user accounts
- Emailing Users (notifications pushed to users about monitoring)
- Deleting a User (Optional)
- Editing a User's details (Optional)


####  <ins>monitoring_services: <ins/>
##### All functions in this file are related to monitoring services, such as:
- The endpoint Daemon activation
- Data collection from the daemon
- Endpoint monitoring
- Editing an Endpoint
- Deleting an Endpoint


####  <ins>web_services: <ins>
##### All functions in this file are related to web services, such as:
- Displaying Monitoring Data to the frontend website (Frontend -> Get Request to Backend)
- sending a list of all VMs being monitored by a user (Frontend -> Get Request to Backend)



##  <ins>Making a View Function<ins/>

####  The General Layout for a View function for a RESTful API Backend is as follows:


```python
#These are generally the imports you will be using
from django.http import HttpResponse
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
import requests
import json

from components.classes import Endpoint_Data, User_Data
from components.models import User, Endpoint

@csrf_exempt
def DummyFunction(request:requests):
      try:
          #Checking to ensure that the request is the one required for the method to function
          if request.method == #"GET", "POST", "DELETE"

                  #If it is a POST request, this is needed to unload the POST data
                  request_body = json.loads(request.body)
                  request_body["Name_of_Var_in_POST_Data_Response"]
                  response = JsonResponse({"message":"Successful POST Request}, status = 200)

                  #If it is a GET, gather the data and then send it back as a response
                  Enpoint_ID = int(request.GET.get("endpoint_id"))
                  Endpoint_ObJ = Endpoint(user_id=User.objects.get(user_id = 12345)
                  response = JsonResponse(Endpoint_OBJ.json(), status = 200)

                  #DELETE is the same as get, but you delete an object in the DB and then send a 200 if successful
	       
      except:
      return JsonResponse({"message":"Failed Post for New Endpoint"}, status = 405)
```

#### All functions which are callable by the frontend should similar the the examples, all of them should include:
- having @csrf_exempt before the function
- a try catch statement to ensure the backend doesn't error out and stop runtime stuff
- a request variable in the parameter of the function to gather the request data from the front ennd
- a response to the request made by the front end



##  <ins>Linking a View Function to a URL<ins/>


#### Now that you have a function ready to be called by the frontend, we need to map that function to a URL.

##### To do that, we need to navigate to the admin directory:

<img width="400" alt="Screenshot 2025-04-09 at 12 36 17 PM" src="https://github.com/user-attachments/assets/92a5fb57-b3e0-4422-86e0-1a96e95886b5"/>


##### Once inside the admin directory, open the urls.py file:

<img width="400" alt="Screenshot 2025-04-09 at 12 36 22 PM" src="https://github.com/user-attachments/assets/1c4dc701-0d49-4d60-a2b2-d47220beea85"/>

##### In the urls.py file, you will see a list of URLS and functions:

<img width="836" alt="Screenshot 2025-04-09 at 12 37 43 PM" src="https://github.com/user-attachments/assets/9b36db34-6cf9-4358-999b-784e8182c1e4" />

##### To map a function to a URL, add a URL using the following syntax:

```python 
path('v2/api/Name-of-Endpoint/', Name_of_Service_File.Name_of_Function),
```

##Testing the new URL / Function:

##### To test the new function, we're gonna locally start up a server of the Django application.
##### To do this, we're gonna open a new terminal tab in our compiler:

<img width="606" alt="Screenshot 2025-04-09 at 12 47 46 PM" src="https://github.com/user-attachments/assets/4b216dc9-544d-4c0b-9f27-de519fde39f3" />


##### Ensure that you are in the correct directory (should be the base dir for the project).

##### After which, type in `python manage.py runserver` in the terminal and run it!

##### Assuming you have no errors, the terminal output should be as follows:

<img width="722" alt="Screenshot 2025-04-09 at 12 50 52 PM" src="https://github.com/user-attachments/assets/120d817a-abcc-4b9f-bf86-3010445f6c4d" />

##### Once it is running, go to http://127.0.0.1:8000/ to visit the local site

##### To test the newly created URL, you will need to use a program like Postman if it is a POST request you are trying to test.

## And that is the general Django workflow for creating new view functions and mapping them to URLS.
