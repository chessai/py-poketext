# Poketext

An SMS/MMS Pokedex application, powered by Twilio and GitHub user phalt's PokeAPI v1

Here I will be re-writing the tutorial from https://www.twilio.com/blog/2014/11/build-your-own-pokedex-with-django-mms-and-pokeapi.html, without the explanations of the workings of everything and while updating the tutorial to python-3.5.1

What you NEED to get this working:

Python 3.5 (Python is the language used in this application)
Ruby (Necessary for Heroku Toolbelt)
Pip, the Python library installer, if you don't already have it (did not come with my Python installation)
Python's virtual environment library, virtualenv (http://docs.python-guide.org/en/latest/dev/virtualenvs/)
A free Twilio Account (https://twilio.com/try-twilio)
A free Heroku Account (https://id.heroku.com/signup)
The Heroku Toolbelt (https://devcenter.heroku.com/articles/getting-started-with-python#set-up)
Your Distribution's version of libpqxx (could be under a different name depending on the distribution. Necessary for one of the application's requirements to install)

After you have gotten all of the above,

Create a new directory called 'pokemon' (or something appropriately descriptive)

Navigate to that directory in a terminal:
$ cd path/to/pokemon

Use git to clone the updated Poketext project from this repository and navigate into the newly created directory
$ git clone https://github.com/wutang-bnp/poketext.git
$ cd poketext

Once you have checked out the start branch after cloning into your appropriately descriptive directory, we need to create a Python virtual environment and install all the relevant software for this project to run. 
$ virtualenv venv
New python executable in venv/bin/python
Installing setuptools, pip...done.

For Twilio to work with Django, we need to add our TWILIO_ACCOUNT_SID (username or email used to sign into Twilio) and TWILIO_AUTH_TOKEN (password) to our environment. Open venv/bin/activate with a text editor, go to the bottom and add these two lines:
export TWILIO_ACCOUNT_SID=YOUR_USERNAME_HERE
export TWILIO_AUTH_TOKEN=YOUR_PASSWORD_HERE

Be sure to replace the values with your own tokens. Save the file and activate the virutal environment:
$ source venv/bin/activate
(venv) $

Then use pip to install all the requirements (you may need sudo):
(venv) $ pip install -r requirements.txt
Downloading/unpacking [library_name_here] (from -r requirements.txt (line etc.

...
Successfully installed [horizontal_list_of_libraries_here]

Cleaning up...
(venv) $

With everything installed, make sure the server is working:
(venv) $ python manage.py runserver

If you see the following output then we are good to go (note that with some recent versions of Django, a warning message(s) may appear, but to my knowledge it can be disregarded):
[Date] - [Time]
Django version [version], using settings 'poketext.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.

Type CONTROL+C to stop the server.

With the Heroku Toolbelt installed, log into Heroku
(venv) $ heroku login
You will be prompted for your heroku credentials - then we can create a heroku app:
(venv) $ heroku create
Creating appNameHere... done, stack is cedar
https://appNameHere.herokuapp.com/ | git@heroku.com:appNameHere.git
Git remote heroku added

'appNameHere' will probably be of the format 'descriptor-natureThingy-number' - don't worry. You can change this. Refer to:
https://devcenter.heroku.com/articles/renaming-apps

To deploy the code to the new Heroku app use the following command:
(venv) $ git push heroku master
Initializing repository, done.
...

-----> Python app detected
-----> Installing runtime (python-3.5.1)
-----> Installing dependencies with pip
      [Downloading/unpacking here]

...
Compressing... done, 40somethingish MB
-----> Launching... done, v1
    https://nature-inspired-name-here-andThenANumber.herokuapp.com/ deployed to Heroku
To git@heroku.com:nature-inspired-name-here-andThenANumber.git
* [new branch]      master -> master

Now we need to add our Twilio tokens to Heroku using the following commands:
(venv) $ heroku config:set TWILIO_ACCOUNT_SID='YOUR_TWILIO_SID_HERE'
Setting config vars and restarting nature-inspired-name-here-andThenANumber... done, v1
TWILIO_ACCOUNT_SID: YOUR_TWILIO_SID_HERE
(venv) $ heroku config set TWILIO_AUTH_TOKEN='YOUR_TWILIO_PASSWORD_HERE'
Setting config vars and restarting nature-inspired-name-here-andThenANumber... done, v1
TWILIO_AUTH_TOKEN: YOUR_TWILIO_PASSWORD_HERE

If you don't have an MMS-enabled phone number, get a new phone number here: https://www.twilio.com/user/account/phone-numbers/search

Within the MMS enabled phone number settings, we want to change the Messaging URL to point to our heroku URL (https://appNameHere.herokuapp.com/incoming/message) and then click save.

Now text the name of a Pokemon to your Twilio phone number. 

Enjoy.
