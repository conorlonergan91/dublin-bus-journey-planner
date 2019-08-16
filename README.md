
# Instructions for Deployment - Team 4

The website is fully deployed and operational at the url:
 
 https://dublinbus.city
 
 This is the final production release, and the code present on this deployment has been provided as part of the code submission. This is the preferred method for viewing the final submission. Should you wish to view our GitHup repository where the development of the project took place collaboratively, please send an email to robert.young2@ucdconnect.ie including the email linked to your GitHub account and you will be given access to the private repository.

There are a number of useful documents within our repository used during the development process.

* README.md - Coding practices for the team.
* Django.md - how to run Django locally while accessing the database on the UCD server.
* DataAnalyticsConnect.md - Connecting and using Jupyter notebook and accessing the data stored on the server, without removing it from the server.

### Local Deployment of the Code
Should you wish to deploy the code locally, there are several steps required to enable this. 

First you will need to build a virtual environment with the provided *requirements.txt* file. In the root of your working directory (but not in the Django directory) create a virtual environment. This may be done by running the command:

``` virtualenv venv_django```

Activate the newly created venv with the following command:

```source venv_django/venv/bin/activate```

Now, to install the dependencies, make sure your working directory is where the *requirements.txt* file is and run this command:

```pip install -r requirements.txt```

Due to the nature and complexity of the project, there is an additional step required to ensure the pymysql package can correctly communicate with the MySql database located on the server. 

Enter the folder where your virtual environment is sotred and navigate through the tree to this location:

```/lib/python3.7/site-packages/django/db/backends/mysql ```

Open the file ```base.py``` and find this statement:

```version = Database.version_info```

Update the code so it looks like this:

```if version < (1, 3, 13):
   pass
   '''
   raise ImproperlyConfigured(
       'mysqlclient 1.3.13 or newer is required; you have %s.'
       % Database.__version__
   )
   ''' 
   ```

Save this and open ```operations.py```. Go to the line:
```query = query.decode(errors='replace')``` 

and update it to:

```query = query.encode(errors='replace')```

### Django runserver
To run Django locally, the easiest solution is to use the inbuilt Django runserver (only for use in development, not to be used in deployment)

Before starting the server, ensure a pipe to the server has been made using steps contained in the Django.md markdown document.

Navigate to the directory where manage.py is located. Run the command 'python manage.py runserver'. The server should now be running on the local host of your machine.

A number of Djangos settings are currently set for *server deployment*. To allow the project to run locally, rather than on the
server you will need to make several changes to the settings.py file.

* Lines 27-32 should be commented out. These are security settings used for deployment only.
* If desired, line 35, DEBUG can be set to True.
* ALLOWED_HOSTS on line 37 will need to be updated to include your local server IP 'http://127.0.0.1'.

Again, this can be quite an involved task, and the best advice for testing of the code and it's deployment would 
be to visit our hosted webpage at: https://dublinbus.city

