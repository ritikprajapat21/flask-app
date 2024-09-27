# Part-1
# Install Python3 & Set Up Programming Environment in Ubuntu(18.04)
### 1. Setting Up Python 3
```sh
sudo apt update
sudo apt -y upgrade
```
#### 2. check the version of Python 3
```sh
python3 -V
```
  #### output: 
  Python 3.6.9
#### 3. software packages for Python
```sh
sudo apt install -y python3-pip
pip3 install Django
pip3 install numpy
sudo apt install build-essential libssl-dev libffi-dev python3-dev
sudo apt install -y python3-venv
mkdir environments
cd environments
python3.6 -m venv env
```
#### 4. Installing Flask
```sh
source env/bin/activate
pip install flask
vi app.py
```
#### Write the following code inside the app.py file:
```sh
from flask import Flask

app = Flask(__name__)


@app.route('/')
def hello():
    return '<h1>Hello, World!</h1>'
```
#### 5. Running the Application
```sh
export FLASK_APP=app
export FLASK_ENV=development
flask run --host=0.0.0.0 --port=5000
```
#### Once the application is running, the output will be like this:
 * Serving Flask app 'app' (lazy loading)
 * Environment: development
 * Debug mode: on
 * Running on all addresses.
   WARNING: This is a development server. Do not use it in a production deployment.
 * Running on http://172.31.43.210:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
---------------------------------------------------------------------------------------------------------------------------------------
  - Once the application is ready copy the public ip address of the VM and ping with 5000 port
  - In my case http://13.235.45.60:5000
  - you will get an output as "Hello World"
  - After this is succesfull Create and configure a Public GitHub repository.
  - Protect the master/main branch. 
  - Once it is done push the code to the repository

# Part-2
# Create a CD pipeline
#### For Continuous Deployment I have opted to use Jenkins. You can do this in CODE-DEPLOY also in AWS. 
#### For this 
#### Install and configure jenkins in Ubuntu 18.04
#### 1. Update the server
```sh
sudo apt update
```
#### 2. Install java
```sh
sudo apt install openjdk-8-jdk -y
```
#### 3. Add the Jenkins Debian repository
```sh
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
```
#### 4. Add the Jenkins repository to the server
```sh
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```
#### 5. Install Jenkins
```sh
sudo apt update
sudo apt install jenkins -y
```
#### 6. Configure Jenkins
###### After installing the jenkins ping your public ip address with 8080
###### It will prompt for admin password, check the path mentioned in UI 
###### Input the password and install the suggested plugins
###### Skip and continue as admin (if you want, you can create a admin user that's upto you)
###### Now click on New Item, provide a proper name to it and select Freestyle Project & click Ok
###### Now Provide the description with proper work flow
###### select Source Code Management as Git
###### In the Build triggers configure pollscm logic in this manner for periodic builds to happen
        MINUTE HOUR DOM MONTH DOW
       * MINUTE	Minutes within the hour (0–59)
       * HOUR	The hour of the day (0–23)
       * DOM	The day of the month (1–31)
       * MONTH	The month (1–12)
       * DOW	The day of the week (0–7) where 0 and 7 are Sunday.
#### By this your GitHub will get clonned to jenkins & will be stored in /var/lib/jenkins/workspace
#### Now in the Build step scroll to Execute shell and do the "scp" funtion to copy the code to the Flask app for the final deployment
#### This will automatically deploy the code when there is a new push to the main/master branch



    
