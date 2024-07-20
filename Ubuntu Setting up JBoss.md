# Setting up JBoss


## Steps 

1) Download JBoss from the  [link](https://developers.redhat.com/content-gateway/file/eap/8.0.0/jboss-eap-8.0.0.zip)

2) Extract JBoss 
3) Create User
    Go to this bin folder of JBoss 
    ```sh
     cd /home/raptor/Prashanth/Software/jboss-eap-8.0.0/jboss-eap-8.0/bin/
    ```
   To Create User, there are two types Management and Application
   
    ```sh
     ./add-user.sh
    ```
    It gives two options 
    
    ```sh
     What type of user do you wish to add? 
     a) Management User (mgmt-users.properties) 
     b) Application User (application-users.properties)

     Choose a for Management
     (a): a
    ```
    it prompts for `userName` and input it as `prashanth` and the password as `Test123#` as the management realm as `develop` and it asks for verification just give it as `yes`.
    Now the password is

    ```sh   
    `management  realm develop -> prashanth/Test123#`
    ```
    On the similar lines create Application user  and it should  have 

    ```sh    
    application realm user    -> prashanth/Test1234#
    ```
5) To start the JBoss
    ```sh
     ./standalone.sh
    ```
    It starts on 8080
