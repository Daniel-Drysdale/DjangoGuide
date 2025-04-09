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
from django.http import HttpResponse
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
import requests
import json

@csrf_exempt
def DummyFunction(request:requests):
      try:
          #Checking to ensure that the request is the one required for the method to function
          if request.method == #"GET", "POST", "DELETE"
          request_body = json.loads(request.body)	 
      except:
      return JsonResponse({"message":"Failed Post for New Endpoint"}, status = 405)
```







