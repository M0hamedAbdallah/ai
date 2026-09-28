---

::page{title="Practice with Flask Part 1"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/IDSN-logo.png" width="200/">

##

**Estimated time needed:** 20 minutes

##

Welcome to the first lab of the Capstone course. You will practice working with Flask in this lab. You should know all the concepts you need for this lab from the previous set of videos. Feel free to pause the lab and review the module if you are unclear on how to perform a task or need more information.

## Learning Objectives

After completing this lab, you will be able to:

- Create and run a Flask server in development mode
- Return JSON from an endpoint
- Understand the request object

---

::page{title="About Skills Network Cloud IDE"}

Skills Network Cloud IDE (based on Theia and Docker) provides an environment for hands on labs for course and project related labs. Theia is an open source IDE (Integrated Development Environment) that can run on desktop or the cloud. To complete this lab, you will be using the Cloud IDE based on Theia and MongoDB running in a Docker container.

## Important Notice about this lab environment

Please be aware that sessions do not persist for this lab environment. Every time you connect to this lab, a new environment is created for you. Any data you save in earlier sessions will be lost. Plan to complete these labs in a single session, to avoid losing your data.

---

::page{title="Set Up the Lab Environment"}

There are some prerequisite preparations required before you start the lab.

## Open a Terminal

Open a terminal window using the menu in the editor: **Terminal** > **New Terminal**.

![New Terminal](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/new-terminal.png "New Terminal")

In the terminal, if you are not in the `/home/project` folder, change to your project folder now.

```bash
cd /home/project
```

## Create the lab directory

You can now create a directory for your server file.

```bash
mkdir lab
```

Change into the `lab` directory:

```bash
cd lab
```
## Check Python version and install Flask

Use the `python3 --version` command to check the version of python3 in the lab enviornment. You should see an output as follows:

```
theia@theiadocker-captainfedo1:/home/project/lab$ python3 --version
Python 3.10.12
```

Next, install Flask using the following command:

```bash
pip3 install flask
```

If Flask is present on the system, you will see the following message:

```
Requirement already satisfied: flask in /home/theia/.local/lib/python3.10/site-packages (3.1.2)
Requirement already satisfied:
...
```

You are now ready to start the lab.

### Optional

If working in the terminal becomes difficult because the command prompt is long, you can shorten the prompt using the following command:

```bash
export PS1="[\[\033[01;32m\]\u\[\033[00m\]: \[\033[01;34m\]\W\[\033[00m\]]\$ "
```

---

::page{title="Step 1: Create the Hello World server"}

### Your Tasks

1. Create server.py file.

	First, create an empty file called `server.py` in the terminal or use the file editor menu.

<details>
	<summary>Click here for a hint.</summary>

> The following command will create the empty file in the right directory.

```bash	
	touch /home/project/lab/server.py
```
</details>

  Open `server.py` in the editor

  ::openFile{path="/home/project/lab/server.py"}

If a new tab called `P&#8203;ython - Get Started` displays after opening this file, you can close it to return to the python file.

2. Import Flask module.

	Next, import the Flask module in this file so you can start coding the server.

<details>
	<summary>Click here for a hint.</summary>

> Import the Flask class in this file by changing the module name.

```python
from flask import <module_name>
```
</details>

3. Create the Flask app

	After importing the Flask module, create your Flask application by initializing the Flask class.

<details>
  <summary>Click here for a hint.</summary>

> Initiate a new application from the Flask class.

```python
from flask import <module_name>
app = <module_name>(__name__)
```
</details>

4. Create the main route and define its method.
   Import Flask, then use the app you created in the previous task to create your first route for the root URL and define its handler method.

<details>
	<summary>Click here for a hint.</summary>

> Use the app decorator to create the root URL `"/"`, then define the method that handles requests to it.

```python
# Import the Flask class from the flask module
from flask import Flask
# Create an instance of the Flask class, passing in the name of the current module
app = Flask(__name__)
# Define a route for the root URL ("/")
@app.route("/")
def hello_world():
    # Function that handles requests to the root URL
    return "Hello, World!"
```
</details>

5. Return the "Hello World" message to the client.

	Return the string "Hello World" to the client.

<details>
	<summary>Click here for a hint.</summary>

```python
# Import the Flask class from the flask module
from flask import Flask

# Create an instance of the Flask class, passing in the name of the current module
app = Flask(__name__)

# Define a route for the root URL ("/")
@app.route("/")
def hello_world():
    # Function that handles requests to the root URL
    return "Hello, World!"

```
</details>

You are all set to run the server. Use the following command to run the server from the terminal:
```bash
flask --app server --debug run
```

![Run Flask server in debug mode](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/m1-flask-run-app.png "Run Flask server in debug mode")

You should now be able to use the CURL command on `localhost:5000/`. Note that the terminal is already running the server, you can use the `Split Terminal` button to split the terminal and run the following command in the second tab.

**Note:** Kindly verify the presence of the `Server.py` file in the /home/project/lab directory to prevent encountering a connection refusal error.
```bash
curl -X GET -i -w '\n' localhost:5000
```
The `-X` argument specifies the `GET` command, and the `-i` argument displays the header from the response.

![Curl command](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/m1-flask-curl-get.png "Curl command")

You should see `Hello World` returned as the output of the CURL command. Note the return status of `HTTP 200 OK` and the `Content-type` of `text/html`. You are asked to return a custom status with JSON instead of plain text in the next part of this lab.

### Solution
Double-check that your work matches the solution below.
<details>
	<summary>Click here for the answer.</summary>

```python
# Import the Flask class from the flask module
from flask import Flask

# Create an instance of the Flask class, passing in the name of the current module
app = Flask(__name__)

# Define a route for the root URL ("/")
@app.route("/")
def hello_world():
    # Function that handles requests to the root URL
    return "Hello, World!"

```
</details>

---

Here's the updated instruction with `jsonify` removed from the hint's import:

---

::page{title="Step 2: Return JSON"}

### Your Task
Congratulations on creating your first route handler in the Flask server. You can return a number of different content types from the `@app.route()` methods. For the purpose of this project, let's return the following JSON instead of the **Hello World** string.
```json
"message": "Hello World"
```
Recall from the videos that there are two ways to return a JSON object from the method:
1. Return a Python dictionary
2. Use the **jsonify()** method on a string

You are being asked to use the first method in this lab.
### Hint
You can edit the existing **index** method to return the desired JSON message.
<details>
	<summary>Click here for a hint.</summary>

> Return a dictionary with the `Hello World` message in the index method.
```python
# Import the Flask class from the flask module
from flask import Flask
# Create an instance of the Flask class, passing in the name of the current module
app = Flask(__name__)
# Define a route for the root URL ("/")
@app.route("/")
def index():
    return <dictionary>
```
</details>

### Solution
Double-check that your work matches the following solution.
<details>
	<summary>Click here for the answer.</summary>

```python
# Import the Flask class from the flask module
from flask import Flask
# Create an instance of the Flask class, passing in the name of the current module
app = Flask(__name__)
# Define a route for the root URL ("/")
@app.route("/")
def index():
    # Function that handles requests to the root URL
    # Create a dictionary to return as a response
    return {"message": "Hello World"}
```
</details>

If you have the server running, you are good to go. If not, you can run the server with the following command again:
```bash
flask --app server --debug run
```
You should now be able to use the CURL command with `localhost:5000/`. Note that the terminal is running the server, you can use the `Split Terminal` button to split the terminal and run the following command in the second tab.
```bash
curl -X GET -i -w '\n' localhost:5000
```
![Flask returns JSON response](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/m1-flask-json-run.png "Flask returns JSON response")

You should see `{"message": "Hello World"}` JSON returned as the output of the CURL command. Note the return status of `HTTP 200 OK` and the `Content-type` of `application/json` this time.

## Author(s)
CF

<!---## Change Log
| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2023-02-01 | 0.5 | SH  | QA pass  |
| 2023-01-22 | 0.4 | CF  | Initial Lab |
| 2025-11-12 | 0.6 | Rajashree Patil  | Updated the flask installation command |
| 2026-04-02 | 0.7 | Rajashree Patil  |Fixed misleading `jsonify` import in Step 2 hint, merged duplicate Step 1 tasks 4–5 into one, and standardized function names across all hints to use a consistent naming convention.|
-->
## <h3 align="center"> &#169; IBM Corporation 2023. All rights reserved. <h3/>
