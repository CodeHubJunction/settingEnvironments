# Setting up P


## Steps 

1) Update System
    ```sh
    sudo apt update
    sudo apt upgrade -y
    ```
2) Check if Python 3 is already installed
    ```sh
     python3 --version
    ```
3) Check if pip3 is already installed
    ```sh
    pip3 --version
    ```
4) Install virtualenv Virtual environment
    ```sh
    sudo apt install python3-venv -y
    ```
5) Create a Python Virtual Environmental (Optional)
    ```sh
    mkdir myproject
    cd myproject
    python3 -m venv venv
    source venv/bin/activate
    ```
7) To deactivate the virtual environment, simply run
    ```sh
    deactivate
    ```
