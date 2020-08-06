_Looking for the [Dwellingly App front end?](https://github.com/codeforpdx/dwellingly-app)_

## Dwellingly App Backend

Set up Dwelling Flask Testing Backend (for the first time)
NOTE: Database is SQLite3 via SQLAlchemy


- Github Repo: { https://github.com/codeforpdx/dwellinglybackend }
- Live Server: {https://dwellinglyapi.herokuapp.com/}


### To Start Server

1. Clone the repo (`git clone https://github.com/codeforpdx/dwellinglybackend.git`)
2. Install Python ( https://realpython.com/installing-python/ )
3. Install pipenv: `pip3 install --user pipenv`.
   - Python version 3.6 or higher is required
4. Database functions
   - Create & Seed: `python manage.py create`
   - Recreate:      `python manage.py recreate`
   - Drop:          `python manage.py drop`
   - If you get the error `ImportError: No module named flask` or similar, you may need to run `pipenv shell` to launch virtual environment.
5. Run `pipenv install`
   - If you get the error `ImportError: cannot import name 'Feature' from 'setuptools'`, your setuptools version might be at 46 or later. You may be able to get it to work using version 45 (e.g. `pip3 install setuptools==45`)
6. Start the server using the flask environment (required every time the project is re-opened):
   - Run: `pipenv run flask run`
   - Run + restart the server on changes: `pipenv run flask run --reload`

6. Test the server and view coverage reports. Use of coverage reporting is recommended to indicate test suite completeness and to locate defunct code in the code base.
    - Install the dev-packages: `pipenv install -d`
    - Run the tests: `pipenv run pytest --cov .`
      - View coverage for a particular directory: `pipenv run pytest --cov [directory]`
    - View detailed coverage reports, with listings for untested lines of code ...
      - As a web page: `python view_coverage.py`
      - In the console: `pipenv run view_coverage`

Queries can be made with the Postman Collection link ( https://www.getpostman.com/collections/a86a292798c7895425e2 )

### Note For Windows Users

Python does not come by default for Windows users. Sometimes the PATH variable in Windows will point to the wrong path and you will have trouble running the `python` and `pipenv` commands. If you don't have Python installed then follow these steps. If the steps listed above did not work for you, try the following.

1. Clone the repo (`git clone https://github.com/codeforpdx/dwellinglybackend.git`)
2. Hit the Windows key on your keyboard and type `Microsoft Store`. Click on Microsoft store and search for Python. Download Python from the official Microsoft store. When you are installing **make sure you tick the Add to PATH checkbox [ ]** If you don't do this, it could result in you being unable to run the python or pip / pipenv commands.
3. Once Python is installed, run `pip3 install --user pipenv` If this command doesn't work, try running `python -m pip install --user pipenv`
4. Follow instructions 4-6 from the previous instructions section.

#### Still having issues on Windows?

If you are still having issues or if your command prompt is throwing an error that says `python is not a command` or `pip is not a command`, it is most likely a pathing issue where the ENV variable is pointing to the wrong directory. To try to troubleshoot, I suggest following this guide: ( https://github.com/LambdaSchool/CS-Wiki/wiki/Installing-Python-3-and-pipenv ).

## Alternative Setup Instructions (for those who have never used Python/having path errors) - Mac OS

1. Clone the repo (`git clone https://github.com/codeforpdx/dwellinglybackend.git`)
2. Install Python ( https://realpython.com/installing-python/ )
3. Install pipenv: `pip3 install --user pipenv`
4. Shell into the environment configured by your Pipfile `pipenv shell`
  - This brings you into a partitioned environment set up to spec with your Pipfile. Often people who skip this step will have path and version errors.
5. Run: `python manage.py create`
6. Run: `pipenv run flask run`
7. Login using one of the accounts below and you should be good to go!

### Endpoints

How to contribute to this project.


1. Set your origin to https://github.com/codeforpdx/dwellinglybackend.git
2. The Main Branch is Development

```console
~$: git pull origin development
```

3. Branch from Development

```console
~$ git checkout -b <name of branch>
```
(Step #3 creates a new branch titled <name of branch> and navigates you to that branch)

#### ENDPOINT: USER Model

| method | route                | action                              |
| :----- | :------------------- | :---------------------------------- |
| POST   | `/register/`         | Creates a new user                  |
| GET    | `/users/`            | Gets all users (dev only)           |
| GET    | `/users/:uid`        | Gets a single user (admin only)     |
| PATCH  | `/users/:uid`        | Updates a single user               | not implemented yet |
| POST   | `/login`             | Login a single user                 |
| POST   | `/user/archive/:uid` | Archives a single user (admin only) |
| DELETE | `/users/:uid`        | Deletes a single user (admin only)  |

### This Backend Uses JWT for authorization

Authorization header format:

```javascript
Authorization Bearer < JWT access token >
```

### The database is seeded with 3 default users

```javascript
[
	{
		email: "user1@dwellingly.org",
		password: "1234",
		firstName: "user1",
		lastName: "tester",
		archived: "false",
		role: "admin",
	},
	{
		email: "user2@dwellingly.org",
		password: "1234",
		firstName: "user2",
		lastName: "tester",
		archived: "false",
		role: "admin",
	},
	{
		email: "user3@dwellingly.org",
		password: "1234",
		firstName: "user3",
		lastName: "tester",
		archived: "false",
		role: "admin",
	},
];
```

#### ENDPOINT: PROPERTIES


| method | route                     | action                                  |
| :----- | :------------------------ | :-------------------------------------- |
| POST   | `/properties/`            | Creates a new property (admin only)     |
| GET    | `/properties/`            | Gets all properties                     |
| GET    | `/properties/:id`         | Gets a single property (admin only)     |
| PATCH  | `/properties/:id`         | Updates a single property               | not implemented |
| PUT    | `/properties/:id`         | Updates a single property (admin only)  |
| DELETE | `/properties/:id`         | Deletes a single property (admin only)  |
| POST   | `/properties/archive/:id` | Archives a single property (admin only) |

```javascript
     {
    "id": "property1",
    "name": "Garden Blocks",
    "address": "1654 NE 18th Ave.",
    "zipCode": "97218",
    "city": "Portland",
    "state": "OR",
    "archived": False
  },
```

#### ENDPOINT: TENANTS

| method | route                        | action                                   |
| :----- | :--------------------------- | :--------------------------------------- |
| POST   | `/tenants/`                  | Creates a new tenant (admin only)        |
| GET    | `/tenants/`                  | Gets all tenants                         |
| GET    | `/tenants/:id`               | Gets a single tenant (admin only)      |
| PUT    | `/tenants/:id`               | Updates a single tenant (admin only)   |
| DELETE | `/tenants/:id`               | Deletes a single tenant (admin only)   |

```javascript
    {
        "id": 1,
        "firstName": "Renty",
        "lastName": "McRenter",
        "phone": "800-RENT-ALOT",
        "propertyID": 1,
        "staffIDs": [1, 2]
    },
```


#### ENDPOINT: EMERGENCY NUMBERS

| method | route                        | action                                              |
| :----- | :--------------------------- | :-------------------------------------------------- |
| POST   | `/emergencycontacts/`        | Creates a new emergency contact (admin only)        |
| GET    | `/emergencycontacts/`        | Gets all emergency contacts                         |
| GET    | `/emergencycontacts/:id`     | Gets a single emergency contact (admin only)        |
| PUT    | `/emergencycontacts/:id`     | Updates a single emergency contact (admin only)     | 
| DELETE | `/emergencycontacts/:id`     | Deletes a single emergency contact (admin only)     |

```javascript
    {
        "id": 1,
        "name": "Narcotics Anonymous",
        "description": "Addiction services")
        "contact_numbers": [
            {
                "number": "503-345-9839"
            },
            {
                "number": "503-291-9111",
                "numtype": "Phone",
                "extension": "x123"
            }
        ]
    }
```


#### ENDPOINT: EMAIL

| method | route           | action                 |
| :----- | :-------------- | :--------------------- |
| POST   | `/user/message` | Send Message to a user |

#### Example Request

```javascript
     {
    "userid": 1,
    "title": "Test email title",
    "body": "Dwellingly Test email body"
  },

```


#### ENDPOINT: TICKETS

| method | route              | action (all actions require user to be logged in)   |
| :----- | :----------------- | :-------------------------------------------------- |
| POST   | `/tickets/`        | Creates a new ticket                                |
| GET    | `/tickets/`        | Gets all tickets                                    |
| GET    | `/tickets/:id`     | Gets a single ticket                                |
| PUT    | `/tickets/:id`     | Updates a single ticket                             | 
| DELETE | `/tickets/:id`     | Deletes a single ticket                             |

```javascript
    id: 1,
    issue: 'Property Damage',
    tenant: 'Renty McRenter',
    senderID: 1,
    tenantID: 2,
    assignedUserID: 4,
    sender: "user1 tester",
    assigned: "Mr. Sir",
    status: "new",
    urgency: "Low",
    opened: "01-Jul-2020 (21:29)",
    updated: "01-Jul-2020 (22:20)",
    minsPastUpdate: 745,
    notes: [
        {
            id: 2,
            ticketid: 1,
            created: "01-Jul-2020 (21:29:10.086958)",
            text: "Tenant has over 40 cats.",
            user: "user2 tester"
        },
    ]
```
