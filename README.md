# Overview  
This project was part of the subject "Cloud-based web applications" of the Master of Data Science degree from La Trobe University.
This project aims to create a simple web application that consists of frontend and backend (API and DB) to keep and maintain all of your contacts. The architecture of the application is shown below.
![image](https://github.com/user-attachments/assets/eb039d67-f530-4926-9ebb-3818ce51d478)
The application has the following functionalities:  
•	Add new a contact name  
•	Add new phone numbers  
•	List all contact names and phone numbers  
•	Remove a phone number from a contact  
•	Remove a contact name and all of the phone numbers  
•	Display the statistics of the data  
The application is created in a docker container with microservices configuration. The example of fully working application is shown below.  
![image](https://github.com/user-attachments/assets/5f3ec617-b353-475e-a4ab-134b9b1b4cc1)
To add a new contact, you could put your name in the name component and click “Create Contact”
![image](https://github.com/user-attachments/assets/32be4293-17d3-42e3-b87c-5d61db453d19)
To add a new contact phone number, you could click the name and provide the contact type and the phone number.  
![image](https://github.com/user-attachments/assets/02342129-1eec-4a8a-905f-0889969cabf4)
To delete a phone number, click the “Delete” button on a phone number row.  
![image](https://github.com/user-attachments/assets/37c1c469-c21f-440d-a561-aef1f5471296)
To delete a contact name, click the “Delete” button on a name block.  
![image](https://github.com/user-attachments/assets/4642f1e4-090d-42a8-acc9-49749d30e396)
To show the statistic, click the “Show Stats” link. Click Refresh to recalculate the number of data in the database.  
![image](https://github.com/user-attachments/assets/420fef48-864f-4b23-bb7d-ad0f000e56c1)
# Steps
## Provide the connections among all of the microservices
The project has several microservices that are connected to each other. These microservices are NGINX, Frontend, Backend and Database. The microservices architecture of the application is shown below:  
![image](https://github.com/user-attachments/assets/bee7d442-1a29-46b9-b97d-b69a7511e301)
•	Update the docker-compose.yml to provide the connections as shown in the microservice architecture  
## Backend API
Create the backend database and REST API for the Contactor application. The backend contain the API and Sequelize scripts to handle the request.  
The database shall have two tables, one for contacts called Contacts and one for phone numbers called Phones. You can test these endpoints using HTTPie  
•	Records from the Contactor table shall contain the fields id (number, Primary Key), name (string)  
•	Records from the Phones table shall contain the fields id (number, Primary Key), name (string), number (string), and contactId (number, Foreign Key)  
•	Foreign keys shall follow the camel-case naming convention (eg a foreign key to the Contacts table would be called contactId). Specify the foreign key name explicitly in associations, as in Lab 07 (there we did foreignKey: 'postId').  
•	Each phone number shall belong to one contact, but a single contact can have many phone numbers.  
•	Two Sequelize models shall be defined – Contact and Phone. These models shall have the correct associations.  
•	The backend shall expose the following REST API:  
![image](https://github.com/user-attachments/assets/747d528a-3eac-46ee-bffc-f6e35d0a9fa7)
## Frontend interface
### Task 1: Create a read-only web interface for the Contactor application which displays contacts and phone numbers. 
SPECIFICATIONS  
•	There shall be a view which lists the names of all the contacts.  
•	Clicking on a contact shall display a list of all of the phone numbers within that contact.  
### Task 2: Allow users to create and delete phone numbers and contacts via the web interface.  
SPECIFICATIONS  
•	Users shall be able to create and delete phone numbers and contacts.  
•	Modifications to contacts and phone numbers shall be persisted in the backend database via the REST API. Therefore changes should survive a page refresh.  
•	You do not need to implement the ability to edit contacts or phone numbers, only to create and delete them  
### Task 3: Summary statistics
#### Task 3.1
Create a new REST API endpoint at GET /stats. This endpoint will serve to show statistics about the application. It should meet the following requirements:  
•	The new /stats API endpoint shall be made available at http://localhost/api/stats  
•	The stats controller code shall be placed in a new controller file  
•	The /stats endpoint shall respond to GET requests with a JSON object containing the following information:  
o	The number of contacts in the database  
o	The number of phone numbers in the database  
o	The time of the most recently created contact  
o	The oldest contact creation time  
#### Task 3.1
Modify the frontend to display summary statistics on the Contactor home page. The statistics themselves shall be retrieved using the /stats API endpoint implemented in Task 3.1. It should meet the following requirements:  
•	A new “Statistics” React component shall be created which is connected to the application store and displays summary statistics  
•	The Statistics component shall be displayed on the Contactor home page  
#### Task 3.2
Add a refresh button which updates the displayed statistics when clicked.
For example, if the statistics show a count of 3 contacts, and then you add another one, clicking the refresh button should update the displayed statistics to indicate that there are now 4 contacts. This means that:  
•	A refresh button shall be visible in the statistics component  
•	Clicking the refresh button shall update the stats by accessing the /stats API endpoint  

