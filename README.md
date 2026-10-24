# Python Flask Multi-Stage CI/CD Pipeline Using Jenkins



## Project Overview



This project demonstrates a multi-stage CI/CD pipeline using Jenkins to build, test, and deploy a simple Python Flask application. The pipeline automatically checks out the source code from GitHub, installs dependencies, executes unit tests, copies application files to a deployment directory, and verifies the application's response.



## Technologies Used



\- \*\*Python\*\* â€“ Application development

\- \*\*Flask\*\* â€“ Web application framework

\- \*\*Jenkins\*\* â€“ CI/CD automation

\- \*\*Git and GitHub\*\* â€“ Source code management

\- \*\*unittest\*\* â€“ Unit testing



## Project Structure



```text

python-flask-pipeline/

â”œâ”€â”€ app.py

â”œâ”€â”€ test\_app.py

â”œâ”€â”€ requirements.txt

â”œâ”€â”€ Jenkinsfile

â””â”€â”€ README.md

```



## Application Details



The Flask application exposes a home route (`/`) that returns:



```text

Hello, Jenkins Multi-Stage Pipeline!

```



## Jenkins Pipeline Stages



### 1. Build



\- Creates a Python virtual environment.

\- Upgrades pip.

\- Installs the dependencies specified in `requirements.txt`.



### 2. Test



\- Executes unit tests using Python's `unittest` framework.

\- Verifies that the Flask application behaves as expected.



### 3. Deploy



\- Creates a `python-app-deploy` directory in the Jenkins workspace.

\- Copies `app.py` and `requirements.txt` into the directory.



### 4. Test Application



\- Uses Flask's test client to send a request to the home route.

\- Verifies that the HTTP status code is `200`.

\- Checks that the response matches the expected message.



## Configuration



The Jenkins job uses \*\*Pipeline script from SCM\*\* to retrieve the pipeline definition from GitHub.



\- \*\*Repository:\*\* https://github.com/ishitaxgupta07/python-flask-pipeline

\- \*\*Branch:\*\* `main`

\- \*\*Script Path:\*\* `Jenkinsfile`



## Execution Results



The pipeline completed successfully with all four stages passing:



\- Build: Successful

\- Unit Tests: Successful

\- Deploy: Successful

\- Application Test: Successful



Expected application test output:



```text

HTTP status: 200

Response: Hello, Jenkins Multi-Stage Pipeline!

Application test passed!

```



## How to Run



1\. Push the project files to the GitHub repository.

2\. Configure a Jenkins Pipeline job using \*\*Pipeline script from SCM\*\*.

3\. Enter the repository URL, select the `main` branch, and set the script path to `Jenkinsfile`.

4\. Click \*\*Build Now\*\*.

5\. Open the build's \*\*Console Output\*\* to inspect the execution results.



## Note



The deployment stage currently performs a mock deployment by copying files into the Jenkins workspace. It does not deploy the application to a production server or expose a live application endpoint.



## Learning Outcomes



\- Configuring Jenkins pipelines using a `Jenkinsfile`.

\- Automating Python dependency installation.

\- Running unit tests as part of CI.

\- Organizing multi-stage CI/CD workflows.

\- Validating application behavior within a pipeline.




