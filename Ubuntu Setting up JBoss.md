# Setting up JBoss EAP 8.0

## Steps to Set Up and Start JBoss EAP on a Local Machine

### 1. Download JBoss EAP
Download JBoss EAP from the official [Red Hat Developer Portal](https://developers.redhat.com/content-gateway/file/eap/8.0.0/jboss-eap-8.0.0.zip).

### 2. Extract JBoss EAP
Extract the downloaded ZIP file to your desired location.

### 3. Create Users
Navigate to the `bin` directory of your JBoss installation:
```sh
cd /home/raptor/Prashanth/Software/jboss-eap-8.0.0/jboss-eap-8.0/bin/
```
To create a user, execute:
```sh
./add-user.sh
```
You will be prompted to choose the type of user:
```sh
What type of user do you wish to add? 
a) Management User (mgmt-users.properties) 
b) Application User (application-users.properties)
```

Choose option 'a' for Management User.
```sh
User Details
    Username: prashanth
    Password: Test123#
    Realm: Management Realm
    Group: develop
    Confirm by typing yes.
```
Similarly, create an Application User:
```sh
User Details
    Username: prashanth
    Password: Test1234#
    Realm: Application Realm
    Group: user
    Confirm by typing yes.
```
### 4. Start JBoss EAP
To start the JBoss server, run:
```sh
./standalone.sh
```


