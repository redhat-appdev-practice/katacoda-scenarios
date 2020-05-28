### Project Base
We'll be using the Todo project that we created at the beginning of the series to test with. If you need a new copy
of the project follow these steps:
1. Clone the project: `git clone https://github.com/redhat-appdev-practice/schemathesis-lab.git`{{execute}}
2. Navigate to project directory `cd schemathesis-lab`{{execute}}
3. Generate the sources and make sure that the application runs without issue: `mvn spring-boot:run`{{execute}}

### Install Schemathesis
1. The first thing we're going to do is set up a virtual environment for our python packages:
`pip install --user virtualenv`{{execute}}
2. Create a new virtual environment in your project folder: `python -m venv myvenv`{{execute}}
3. Activate your new virtual environment: `source myvenv/bin/activate`{{execute}}
4. Install Schemathesis: `pip install schemathesis`{{execute}}