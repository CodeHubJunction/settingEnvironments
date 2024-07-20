# Setting up Maven


## Steps 

1) Download Maven from the  [link](https://maven.apache.org/download.cgi)

2) Extract Maven
   Create the directory if it does not exist.
    ```sh
     sudo mkdir -p /opt/maven
    ```
     Extract Maven and moving it to opts

    ```sh
     sudo tar -xvzf apache-maven-3.9.8-bin.tar.gz -C /opt/maven
    ```
3) Adding it to bashrc
    Opening bashrc

   ```sh
     nano ~/.bashrc
    ```
   Adding environment variables

    ```sh
       # Maven environment variables
        export M2_HOME=/opt/maven/apache-maven-3.9.8
        export MAVEN_HOME=/opt/maven/apache-maven-3.9.8
        export PATH=$M2_HOME/bin:$PATH
    ```
4) To apply the changes without restarting your terminal
    ```sh
    source ~/.bashrc
    ```
6) To check maven installation
    ```sh
    mvn --version
    ```
