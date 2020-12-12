# 2.6. Prepare demonstration
### 1. Setting Up The Environment 
i. Turn LabPartner and Hospital VMs on. Hospital VM will ask for a username and password:

``` 
username:root
password:osboxes.org
```

ii. Start **LabPartner** by going to */home/seed/Desktop/Arquivo* directory, open a terminal and run the following command:

```
java -cp gson-2.6.2.jar:fontbox-2.0.21.jar:pdfbox-2.0.21.jar:apache-commons-logging.jar: SecureLabPartnerTCP 8001 keys/bob.privkey keys/bob.pubkey keys/alice.pubkey keys/secret.key
```
Now LabPartner is running on port 8001. Note that machine's IP was previously  configured to 192.168.0.100. 

iii. To start Apache HTTP Server on **Hospital VM** open a terminal and run the following command:

```
sudo /opt/lampp/lampp restart
```
iv. Now open Firefox browser and access to *https://localhost/apiSIRS/* to visualize the application. The code for the application can be found  in */opt/lampp/htdocs/apiSIRS/* folder.

### 2. Running The Application 
i. To sign in as a doctor first insert the credentials bellow and then click login:
``` 
username:doctor
password:password
```
A list with patitents assigned to **doctor** will show up.

ii. To ask for a test for a specific patient, click on _Get Test_ button. When this action is performed, the user, in this case enrolled as a doctor, will be redirected to a page containing all the patient tests. To ask for a new test click on _Ask for a test button_. This action will send an encrypted message to Lab Partner's server with the patient's name and id. 

iii. When Lab Partner receives the Hospital's request will create a new test for the respective patient and send it to Hospital. This communication is implemented using the custom protocol described in project report.

### 3. Test User Authorization Policies
##### 3.1 - Normal Mode
i. Sign Up as doctor again as explained above and try to access, for instance, in receptionist's page by placing _https://localhost/apiSIRS/receptionist.html_ in the address bar in the browser. The application will not allow this action because a doctor is not authorized to access receptionist page. The same message will appear when accessing to the nurse's page _https://localhost/apiSIRS/searchNurse.html_. Note that this will also happen when doctor, nurses or receptionists try to access to non authorized information. 


##### 3.2 - Pandemic Mode
i. While in pandemic mode, all users are authorized to access all users pages. For instance, a doctor is authorized to visualize nurse's assigned patients and receptionist page as well, having permission to register a new patient, which was not possible in normal mode.
To test pandemic mode proceed to follow the steps bellow:
```
cd /opt/lampp/htdocs/apiSIRS/php/XACML/
sudo gedit mode.txt
```
Change "Normal" to "Pandemic" and save the file.





