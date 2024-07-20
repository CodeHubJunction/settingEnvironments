# Setting up JDK


## Steps 

1) Download Eclipse from the  [link]([https://www.postman.com/downloads/](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)) download Linux x64 Compressed Archive. 

2) It's a common practice to install Java Development Kits (JDKs) in the /usr/lib/jvm directory on Linux systems. So we create this directory if it doesn’t exist.
   ```sh
    sudo mkdir -p /usr/lib/jvm
    ```
3) Extract the JDK
   ```sh
    sudo tar -xvzf jdk-17.0.11_linux-x64_bin.tar.gz  -C /usr/lib/jvm/
    ```
4) Setting Up Environment Variables

   edit `.bashrc`

   ```sh
   nano ~/.bashrc
    ```
   edit these to bashrc and add java_home and path
   
   ```sh
    alias jdk17="export JAVA_HOME='/usr/lib/jvm/jdk-17.0.11'; export PATH=\$JAVA_HOME/bin:\$PATH; java -version"

    echo 'We have multiple versions of SDKs available, the available ones are: '
    echo 'jdk17       -> jdk 17'
    ```
6) Apply the changes by sourcing the `.bashrc`:
    ```sh
     source ~/.bashrc
    ```
7) Select the jdk 
    ```sh
    jdk17
    ```
