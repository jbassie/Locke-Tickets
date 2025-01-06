# Locke Tickets Rest API built with NodeJs, Express and MySql



### :memo: Documentation

The documentation was generated using Postman and is divided into collections at the following URLs:

- Auth - https://documenter.getpostman.com/view/13348269/TzRa6443
- Movies - https://documenter.getpostman.com/view/13348269/TzRa63yg
- Roles - https://documenter.getpostman.com/view/13348269/TzRa63yh
- Genres - https://documenter.getpostman.com/view/13348269/TzRa63yf
- Shows - https://documenter.getpostman.com/view/13348269/TzRa643z
- Theaters - https://documenter.getpostman.com/view/13348269/TzRa6441
- Bookings - https://documenter.getpostman.com/view/13348269/TzRa63ye
- Payments - https://documenter.getpostman.com/view/13348269/TzRa63yi

### :rocket: Deployement

- The database for this API is hosted using AWS RDS (Make sure to update the .env.prod file with your own Database Hosting Url, otherwise the production environment will be running on the local database as well)
- The Production API is deployed using Heroku

**IMPORTANT:** The URLs for both of these deployments is kept private due to security reasons. You can use any services out there for your own hosting requirements. 

The release branch contains workflow to deploy to my own Heroku Service and won't work on your fork. If you want to use heroku as well, see their instructions and update your github secrets with your own credentials to make the release branch CI work for you as well.

### :dvd: Installation
#### 1. Getting Started

``` sh
# Clone this repo to your local machine using
git clone https://github.com/jbassie/Locke_tickets

# Get into the directory
cd Locke_tickets
# Make it your own
rm -rf .git && git init
```

### 2. Setting Up ENV Variables
```sh
# Copy example.env and create your own .env file in envs folder
cp .env.example envs/.env

# Move into the envs dir
cd envs

# Edit .env file and add your mysql username, password and db name, host,
# port, jwt_secret, sendgrid api key and sender email
vscode .env

# Create different .env.{NODE_ENV} file for each environment and override only your
# required variables. The missing ones will be loaded from .env by default.
# For example if you want dev and production environments:
cp .env .env.dev
cp .env.dev .env.production

# When the NODE_ENV variable is set while running, the correct .env loads automatically.
# e.g. Setting NODE_ENV=production is going to load the .env.production file

# Add a gitignore to ignore node_modules and your .env file
echo -e 'node_modules \n envs \n' >> .gitignore
```

#### 3. Setup MySQL database

Import the Locke_ticket.sql using your sql workbench to create the database.

#### 4. Setting up node js

``` sh
# Install dependencies
npm install

# Run the server locally with default .env file
npm start

# Run the server in dev mode with nodemon with .env.dev file
npm run dev

# While deploying to production with .env.production file
npm run production
```

### :arrows_counterclockwise: Setup CI (Github Actions)

If you want to run the github testing and PR labelling workflows in the CI then:

Create the following repository secrets:
  * CONFIG_VARS: value should be the following .env file variables
   ```
   DB_HOST= db_localhost
   DB_USER= db_username
   DB_PASS= db_password
   DB_DATABASE= db_name
   ```
  * SENDGRID_API_KEY: value should be your .env file variable => sendgrid_api_key
  * SENDGRID_SENDER: value should be all your .env file variable => from_email
  * SECRET_JWT: value should be all your .env file variables => your_secret

### :man_astronaut: (Optional) Setup Postman API

If you want to quickly setup the endpoints for testing:

* Go to Postman to import backup
* Upload the schema_backup or unzip postman_collections_backup.zip and upload the folder

### :closed_book: Important Notes

- There are two types of users possible (admin, api_user)
- Most of the POST/PATCH/DELETE endpoints are forbidden to the `api_user` and only `admin` can use them. So make sure you use the `token` from an **admin account login** for `admin` access.
- Only some POST/PATCH endpoints are open to the `api_user` like updating his profile or creating a booking/payment.
- The `healthcheck` endpoint is to ensure the status of the API from the CI so we can be sure we are deploying a working API only.
- You need to make an account on Twillio and integrate Sendgrid to get your own `SENDGRID_API_KEY` and `SENDER_EMAIL`
- If you add/remove/change the names of any folders/file extensions make sure to update the [labeler.yml](.github/labeler.yml)

**Enjoy :)**

### :wrench: Tech

This example uses a number of open source projects to work properly:

* [node.js]
* [Express]
* [@sendgrid/mail]
* [bcryptjs]
* [cors]
* [cross-env]
* [deep-email-validator]
* [dotenv-flow]
* [express-validator]
* [jsonwebtoken]
* [mysql2]
* [otp-generator]
* [babel-eslint]
* [mocha]
* [eslint-config-strongloop]
