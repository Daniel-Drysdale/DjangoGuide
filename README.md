# Guide to making new views, linking them to URLS, and working on models (DB)
Guide on Django Workflow for the SSE Project



# Making a new view function

### Generally, you will be making a new view function in these 3 files

<img width="398" alt="Screenshot 2025-04-07 at 10 48 56 AM" src="https://github.com/user-attachments/assets/2b2618f3-5601-4120-811c-f3197321bfa0" />

#### user_services:
##### All functions in this file are related to user services, such as:
- Creating new user accounts
- Emailing Users (notifications pushed to users about monitoring)
- Deleting a User (Optional)
- Editing a User's details (Optional)


#### _monitoring_services:_
##### All functions in this file are related to monitoring services, such as:
- The endpoint Daemon activation
- Data collection from the daemon
- Endpoint monitoring
- Editing an Endpoint
- Deleting an Endpoint


#### web_services:
##### All functions in this file are related to web services, such as:
- Displaying Monitoring Data to the frontend website (Frontend -> Get Request to Backend)
- Displaying List of all VM's being monitored
