## Software Requirements

- [python 3.5+](https://www.python.org/)
- [Django 2.0+](https://www.djangoproject.com/download/)
- [Django Rest Framework 3.8+](http://www.django-rest-framework.org/#installation)
- [Coverage.py 4.3+](https://coverage.readthedocs.io/en/coverage-4.5.1a/install.html)

Although it is not necessary, it is highly recommended to use  [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/), since it isolates the project's environment, allowing the development of many different projects' versions with different dependencies' versions.


### Installing Dependencies

```bash
# After navigating to the project freightstore/src directory, install virtualenvwrapper
$ pip install virtualenvwrapper
# Additional steps (only for Linux users)
$ export WORKON_HOME=~/Envs
$ mkdir -p $WORKON_HOME
$ source /usr/local/bin/virtualenvwrapper.sh
# Create isolated enviroment (using "freightenv" as the name for the environment)
$ mkvirtualenv freightenv
# Use the freightenv environment created
$ workon freightenv
# Install the requirements
$ pip install -r requirements.txt
```


### Running the Project

```bash
# Use the freightenv environment
$ workon freightenv
# Execute migrations
$ python manage.py migrate
# After navigating to the project freightstore/src directory, start the server
$ python manage.py runserver

```


### Running simple test with sample data

It's possible to execute a test with the /api/v1/shortest-path/ endpoint by running the following steps:

```bash
# Use the freightenv environment
$ workon freightenv
# After navigating to the project freightstore/src directory, execute migrations
$ python manage.py migrate
# Load the sample data
$ python manage.py loaddata sample_data.json
# Start the server
$ python manage.py runserver
```

After these commands, just access the following URL using a web browser.

```
http://localhost:8000/api/v1/shortest-path/?map_name=Sao%20Paulo&origin_point=A&destination_point=D&fuel_litter_price=2.50&fuel_consumption=10
```

Expected result:

```
{
    "shortest_path": "['A', 'B', 'D']",
    "freight_rate": "6.25"
}
```


### Logging

Freightstore uses python built-in logging library to trace and analyze incoming requests. By default, the log is disabled. To enable information logging, the application expects a configuration file (logging.conf) and the "logs" folder in the same directory as manage.py.
There is a configuration file example (logging.conf_file) available in the project. Just rename this file to logging.conf, create the logs directory, restart the web server (python manage.py runserver), and a file will be created in the logs folder. The information level in this log depends on the configuration set in logging.conf.


### Running django unit tests

```bash
# After navigating to the project freightstore/src directory, execute tests
$ coverage run --source ./ ./manage.py test -v 2
```

- The command above uses coverage.py library to analyze how much code the tests executed can cover. If the tests were executed with no errors, then the command shell should show the following messages in the last lines shown in the terminal (the time period may have a different value on a different machine, and number of tests - "nn" in the following lines - may change depending on the application's version):

```bash
Ran nn tests in 0.455s

OK
Destroying test database for alias 'default'
```

- To analyse how much these tests cover each python script from this project, execute the following command:

```bash
# Show each python script of the project and how much code is covered with the tests
$ coverage report
```