# Deploy Machine Learning Model into AWS Cloud Servers

- Now we will build a spam detector using machine learning & launch it as a serverless API using AWS Elastic Beanstalk technology. We will accomplish it in by completing each task in the project:

## Task 1: Create a Flask application

- Create a flask application file and name it as "application.py"
```
from flask import Flask, request
app= Flask(__name__)

@app.route('/')
def hello_world():
    return "Hello world"

@app.route('/spamorharm', methods=['GET', 'POST'])
def spamorham():
    message = request.args.get("message")
    return message

if __name__ == '__main__':
    app.run()
```
- Do not forget to install flask:
```
- " pip3 install flask"
```
- Than create a virtual environment and activate it:
```
 pip3 install virtualenv
# to activate  use this command below
 source venv/bin/activate
```
- Run the command to run application.py
  ```
  python3 application.py
```
- Check the local host for the running app with Postman app.
- Click the postman, use your local IP to make Get and Post request.
  
## Task 2: Create a RESTful API - GET/POST Method
- Update your code: 

```
from flask import Flask, request
app= Flask(__name__)

@app.route('/')
def hello_world():
    return "Hello world"

@app.route('/spamorharm', methods=['GET', 'POST'])
def spamorham():
    message = request.args.get("message")
    return message

if __name__ == '__main__':
    app.run()

```

## Task 3: Build a spam detector ML model
- We will use our "SpamDetector.ipynb" file in the project file. 
- Run the code and tune the "LogisticRegression" model.
- Install sklearn library
```
pip3 install sklearn
```
- use the "pickle" operation to create a connection with jupyter 

## Task 4: Build a spam detector API
- Update your code with "vectorizer.pkl" and "spam_ham_model.pkl" files.

```
from flask import Flask, request
import joblib 

app = Flask(__name__)

vectorizer = joblib.load("vectorizer.pkl")
spamorham_model = joblib.load("spam_ham_model.pkl")


@app.route('/')
def hello_world():
    return "Hello world"


@app.route('/spamorham', methods=['GET', 'POST'])
def spamorham():
    message = request.args.get("message")
    vect_message = vectorizer.transform([message])
    result = spamorham_model.predict(vect_message)[0]
    return result


if __name__ == '__main__':
    app.run()
```

## Task 5: Launch an AWS EC2 instance(Virtual Server) using AWS Elastic Beanstalk.
 -- Connect to your AWS Account and create a Beanstalk Instance

## Task 6: Deploy your ML model(API) into AWS virtual servers.

-Save your environtment requirements with this command
```
pip3 freeze > requirements.txt
```
- Copy "vectorizer.pkl" and "spam_ham_model.pkl" files to myflask folder and zip the  "vectorizer.pkl", "spam_ham_model.pkl", "requirements.txt" and "application.py" files. 
- Upload the zip file to AWS Elastic Beanstalk
- Use the Postman application to be sure that your SpamDetector is working

## Task 7: Perform additional AWS Elastic Beanstalk actions: Application versioning, Server logs, Server performance monitoring & Terminate the server.
