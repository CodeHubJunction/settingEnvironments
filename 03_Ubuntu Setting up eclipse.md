# Setting up eclipse


## Steps 

1) Download eclipse from the  [link](https://www.eclipse.org/downloads/)

2) Extract eclipse
    ```sh
     tar -xvzf eclipse-jee-2024-06-R-linux-gtk-x86_64.tar.gz
    ```
3) Moving it to opt go to the last part of eclipse folder where we get configuration, dropins etc..
    ```sh
     sudo mv ./eclipse/ /opt/
    ```
4) Creating a Symbolic link 
    ```sh
    sudo ln -s /opt/eclipse/eclipse /usr/local/bin/eclipse
    ```
5) To create icon 
    ```sh
    nano ~/.local/share/applications/eclipse.desktop 
    ```
6) To add the 
    ```sh
    [Desktop Entry]
    [Desktop Entry]
    Encoding=UTF-8
    Version=1.0
    Type=Application
    Name=Eclipse
    Icon=/opt/eclipse/icon.xpm
    Exec=/opt/eclipse/eclipse
    Terminal=false
    Comment=Integrated Development Environment
    Categories=Development;IDE;
    ```
7) To Run eclipse from terminal
    ```sh
    eclipse
    ```
8) The Eclipse icon may not appear in the application menu immediately. Please restart the operating system to facilitate the update.  
    
