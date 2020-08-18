# Local environment setup

## Prerequisites

- If you're on Mac, you'll need [homebrew](https://treehouse.github.io/installation-guides/mac/homebrew)

- Linux instructions assume that you're using an Ubuntu derivative with `apt`

Clone the repo using git. 
You should hopefully have an SSH key set up already.

## Required software

### Python

We'll be using python3.7 for this project.

Check if you have python3.7 by typing `python3.7` into your terminal.
If a python prompt appears, you're good.
Note that you can have multiple python versions at once - having python3.8 doesn't mean you're missing python3.7. Python3.8 would probably work too, but it's probably easier to have everyone on the same version just in case.

#### Installation

- On [Mac](https://docs.python-guide.org/starting/install3/osx/):
    - `brew install python`
- On [Linux (assuming Ubuntu or derivates)](https://docs.python-guide.org/starting/install3/linux/#install3-linux):
    - `sudo apt install python3.7`

## pip

Check if you have pip with `pip --version`.

- If you installed python via homebrew on Mac you should be fine

- On Linux, you may need to [install it separately](https://pip.pypa.io/en/stable/installing/)

### npm

- On [Mac](https://treehouse.github.io/installation-guides/mac/node-mac.html):
    - Basically just `brew update` then `brew install node`.
- On [Linux](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm):
    - `sudo apt install npm`
    - `sudo apt install nodejs`

Then verify that node and npm are both installed by running `node -v` and `npm -v`.

## Very Recommended software

### PyCharm

[PyCharm](https://www.jetbrains.com/pycharm/) is a highly recommended IDE for Python projects.
It takes care of a lot of things (e.g. installation of external libraries you're trying to import).
Pycharm will assist with formatting and alert you to syntax errors and other issues (much more than VS Code).
It should handle other files nicely too (e.g. Javascript).

Install the community (free) version.


#### Installation

- On [Mac](https://www.jetbrains.com/pycharm/download/#section=mac)
- On Linux, either:
    - Install using your distro's software centre (recommended)
    - Alternatively, download [here](https://www.jetbrains.com/pycharm/download/#section=linux)
    
### Git autocomplete

Linux (Ubuntu derivatives) should have a mechanism for git autocomplete (i.e. press tab to autocomplete branch names etc).
I don't think Mac does by default.
Definitely give it a try for quality of life.

[Mac - git bash completion](https://github.com/bobthecow/git-flow-completion/wiki/Install-Bash-git-completion).
Note that it's a bit more than just a `brew install`.

## Virtual environment setup

It's important to set up a Python virtual environment for this project.
A virtual environment helps to ensure that we all use the same libraries.
PyCharm conveniently provides an option for us with Virtualenv.

After cloning our GitHub repo (capstone-project-meal-friends), open PyCharm.

Click *File > New Project* (**NOT *File > Open***) and select the `api` directory in our project. 
On that same screen you'll now see stuff about a Project Interpreter.
Make sure that you're creating a New environment using Virtualenv.

The Base interpreter should be Python3.7. If it's not there by default, try the dropdown.
If it's not in the dropdown, run `which python3.7` in a terminal to get the required path.
Navigate to that in the Pycharm screen via the **...** button.
Sometimes this is fiddly.
Feel free to ask for help.

After clicking *Create* you'll be asked if you want to use existing sources.
Say yes.

Once PyCharm loads (give it a minute), find + click the *Terminal* button at the bottom of the screen.
The prompt should say `(venv)`.
This indicates excellent success.
If you open a Python document, you should then be prompted to install packages from the `requirements.txt` file.

The virtualenv for the project should activate automatically in PyCharm.
This is good.
In a regular terminal, you should navigate to the project root directory and run `source venv/bin/activate` to get the virtual environment running.
Type `deactivate` in that terminal to deactivate the virtual environment.

## Start the back end

### One-time setup
You'll need to set up a couple of **environment variables** so you can make calls to Spoonacular. 
Once you make your [Spoonacular account](https://spoonacular.com/food-api/console#Dashboard),
go to *My console > Profile* and copy the hidden API Key.

In order to email shopping lists to users, a valid Gmail account must be set up and these instructions must be followed
to configure the settings of that Gmail account:
https://www.dev2qa.com/how-do-i-enable-less-secure-apps-on-gmail/

Now make a file called `.env` in the project's `api` directory.
Edit the file and make it look like this:
```
SPOONACULAR_API = <paste your api key here>
SECRET_KEY = <just type like 15-20 random characters here>
ENVIRONMENT=dev
GMAIL_USERNAME=<your gmail username>@gmail.com
GMAIL_PASSWORD=<your gmail password>
```

For example:
```
SPOONACULAR_API = 120c01cmx102984sdfswe908wdf09i
SECRET_KEY = 32dg7cidfg0i34gy8U9
ENVIRONMENT=dev
GMAIL_USERNAME=mealfriends3900@gmail.com
GMAIL_PASSWORD=<see report for private password or set up your own account>
```

This file should be discovered when the Python/Flask server starts.

**Note**: Don't try to commit this file to git or share the contents.
Treat the contents like passwords.

### One-time Firebase setup

We are using Firebase Realtime Database for data persistence.
See here for information about storing data:

https://firebase.google.com/docs/database/admin/save-data

Expect a total delay of around 250-500ms for each request.

To access the team database you must do the following:
- create a Google/Gmail account if you don't have one.
- send your Google account's email address to the scrum master.
- sign up to firebase when you receive an invitation.
- on the firebase website:
  - make sure you see "meal-friends" somewhere on the page. For example:
    https://console.firebase.google.com/project/meal-friends/database/meal-friends/data
  - open the left sidebar.
  - click the cog -> project settings -> service accounts -> click "Generate new private key".
  - save that file inside the project's api/ folder with the filename "private-firebase-credentials.json". 
    This is another private file - don't share the contents. It should automatically be excluded from git.

### Running the back end

Once Flask is set up, you'll be able to start the back end server locally by executing the file `run.py` in either PyCharm or terminal (with virtualenv active).

Note: you'll probably need to `cd` into the `api` directory for imports to be found correctly.

## Start the front end

You can get `yarn` as an alternative to `npm` if `npm` doesn't work nicely. Do this with `npm install -g yarn`.

Run `npm install` (or `yarn`) to download the big folder of node_modules.

Then run `npm start` (or `yarn start`) from within the `frontend` directory.
This may take a minute the first time.
Stuff will download.
Your browser should then open up to what will become our project.
Check the developer console if you see/suspect errors.

Note: If you make a change to the front end while yarn is running, it should automatically take those changes into account and reload the page.
Pretty good.

# Git practices

This is a big project so be sure to do git properly.
COMP1531 is a great start, but we'll have a few other things too.

## Branching

Prepend your branch name with the Jira ticket identifier.
There might also be something to add for subtasks.
For example, if you're doing story `MEAL-41`, your branch might be `MEAL-41-admin-delete-recipes`.
Remember to use the handy 
```bash
git checkout -b <branch name>
``` 
for branch creation.

It might be better for backend people to get their subtasks done before frontend, so we don't have simultaneous work being done on a single thing.

## Committing

Again, prepend your Jira ticket ID to each commit.
So you might commit with 

```bash
git commit -am "MEAL-41 Database access set up and tested"
```

## Pushing

Push your branches often - just in case.

## Updating

If you're comfortable with rebasing, do that.
However, you might prefer to merging the master branch into your branch for now (after pulling from *master*).

## Merging to *master*

This is different from 1531.
We should be reviewing each others' code for quality before any merges to *master*.
This is to make sure people are familiar with each other's code and try to reduce bugs/code smells slipping in.

This is done via **[pull requests](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests)**.

Once you've finished a subtask, pull *master*, then switch back to your branch and rebase/merge *master* into yours.
Resolve conflicts and push the branch again to GitHub.
Then, open a pull request on GitHub to merge your branch into *master* on [this page](https://github.com/unsw-cse-capstone-project/capstone-project-meal-friends/compare).

Make sure *Base* has *master* selected.
*Compare* should be your branch.

Add everyone as reviewers.
This lets people look at your code, understand what's been done, make comments + queries etc.
Since we're a small team,  1 approval is probably enough, assuming you don't have any lingering questions/concerns. 
(Note: if you get approvals without having to fix anything, you're a pro programmer).

### Squashing

It's fantastic practice to make lots of commits as you work.
But if we ever get a bug (lol) it might be hard to find which commit it was introduced in.
You can compress a bunch of commits into 1 when you merge your pull request; use the "Merge and squash" option that should appear before confirming the merge on GitHub.

### More branches

Want to add a quick bug fix or edit to *master*? 
Still make a new branch so we can track stuff (except for non-code stuff like diaries). 

If it's related to a Jira task, include the ticket code in your new branch name.

If it's not related to an issue, call it something like `noissue-typo-fix`.

### Code reviews
Try to review other people's work regularly - at least as often as you make pull requests.
Read through the code. 
Also feel free to run it as well to check for bugs.

# Coding

## APIs

Flask provides endpoints for the frontend to access.

### JSON

This should be returned in JSON format to make frontenders' lives easier.
JSON can be thought of just like a Python dictionary.
It often has deeply nested structures.
Spoonacular responds in JSON format.
That's a good example to emulate.

More info:
- [JSON](https://www.json.org/json-en.html)
- [More accessible, maybe](https://www.w3schools.com/js/js_json_intro.asp)

### Add a descriptive comment

APIs are the *most* important thing for us to document in this assignment.

Make sure to put a comment on each Flask endpoint you create, describing what data it takes in (describing the format) and what it returns and how.
Mention any behaviour that might surprise someone.

APIs are basically a contract; changing the return value might break the front end.
Adding extra fields to the JSON is usually fine, though.

## Testing

We should test the backend in some capacity.
Flask makes manual verification fairly easy in your browser (but I've found automated testing of Flask itself to be difficult with pytest).
We can also write unit tests (pyunit or unittest) for our internal back end behaviour.
Nathan is probably the expert here.

## Abstraction

We'll work on this assignment for about 6 weeks. That's plenty of time for code to become complete spaghetti. We'll set up some layers of abstraction to help with this. For example, our Flask endpoints shouldn't be constructing SQL or HTTP queries - it'll be the work of a separate class.

## requirements.txt

After you install a library with pip or via Pycharm, run `pip freeze > requirements.txt` to make a record of the library name and version.
That makes it easy for everyone else to install the exact same thing.
This might not be absolutely necessary if everyone is using PyCharm, but it's still good practice.
