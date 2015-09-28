---
layout: docs
---

# The Free Code Camp Boilerplate

## About

Clementine.js is a lightweight boilerplate for fullstack JavaScript development which utilizes MongoDB, Express and Node.js. The boilerplate errs on the side of transparency and simplicity, making it an ideal starting point for beginner and seasoned developers alike. 

The [Free Code Camp](http://www.freecodecamp.com) version of Clementine.js is meant for use when completing projects as part of the FCC curriculum. This version includes GitHub authentication using [Passport](http://passportjs.org/).

### MongoDB

MongoDB is a document-store (NoSQL) database. Queries are written in JavaScript, and that is the primary reason for its inclusion in the MEAN stack.

For more information on MongoDB, please [have a look at their stellar documentation](http://docs.mongodb.org/manual/). In addition, once you have practiced your Node skills, I highly recommend taking [this free 7-week online course](https://university.mongodb.com/courses/M101JS/about) that MongoDB offers.

### Express

Express is an unopinionated framework for Node.js that creates additional functionality for the creation of web applications. 

For more information on express, check out their [website and documentation](http://expressjs.com/).

### Node.js

Node.js is a platform built on Google's V8 JavaScript run-time, allowing server-side code to be written in JavaScript. 

For more information on Node, [try their site](https://nodejs.org/documentation/). I also recommend having a look at [NodeSchool](http://nodeschool.io/).

### Passport

[Passport](http://passportjs.org/) is middleware for Node.js / Express that enables easy integration of authentication and authorization. It includes extensions for the popular oAuth options, and is used for GitHub authentication in this version of the boilerplate.

[Back to top.](#top)

## Installation

Prerequisites for Clementine.js:

- [Node.js](https://nodejs.org/)
- [NPM](https://nodejs.org/)
- [MongoDB](http://www.mongodb.org/)
- [Git](https://git-scm.com/)

[Back to top.](#top)

### Install Node.js and NPM

_Note:_ The Node insallation installs both Node & NPM.

**MAC OSX & Windows**

Head to the [Node.js install page](https://nodejs.org/download/). Download the appropriate file follow the installation instructions.

**Linux**

_Option 1_ - Install via PPA

```bash
$ sudo add-apt-repository ppa:chris-lea/node.js
$ sudo apt-get update
$ sudo apt-get install nodejs
```

_Option 2_ - Install via LinuxBrew

First, ensure [LinuxBrew](http://brew.sh/linuxbrew/) is installed. Then, enter the below into the Linux terminal:

```bash
$ brew install node
```

[Back to top.](#top)

### Install MongoDB

MongoDB has great installation instructutions for MAC OSX, Windows and Linux. [See this page.](http://docs.mongodb.org/manual/installation/)

[Back to top.](#top)

### Install Git

Follow the [directions here to install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for the appropriate environment.

[Back to top.](#top)

### Install Clementine.js

Clementine.js is easy to setup in the project directory of your choice! In the terminal:

```bash
$ git clone https://github.com/johnstonbl01/clementinejs-fcc.git your-project
```

It's that easy!

[Back to top.](#top)

### Setup GitHub Authentication

Please follow [this guide](/clementinejs/tutorials/tutorial-passport.html#github-app-setup) to register the application with GitHub and get API keys / secrets. This API information will also need to be added to the `app/config/auth.js` file.

[Back to top.](#top)

### Starting the App

To start the app, make sure you're in the project directory and type `node server.js` into the terminal. This will start the Node server and connect to MongoDB.

You should the following messages within the terminal window:

```
Node.js listening on port 8080...
```

Next, open your browser and enter `http://localhost:8080/`. Congrats, you're up and running!

## Architecture

Clementine.js employs a very simple application architecture to promote transparency and simplicity. The application consists of:

- Three views
- Two client-side controllers
- One server-side controller
- Passport Configuration
- Common AJAX Functions
- Node.js server file
- Route file
- CSS file

When installed, Clementine.js offers a very simple application demonstrating full stack JavaScript. This application follow the [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) design pattern. 

### Folder Structure

```
+--	Project Folder
	+-- app
	|	\-- common
	|	\-- config
	|	\-- controllers
	|	\-- models
	|	\-- routes
	|
	+-- public
	|	\-- css
	|	\-- img
```

**Project / Root Folder** - The project directory. This directory contains:

- _.gitignore_ - A file specifying which directories git should ignore when pushing to the master
- _LICENSE.md_ - Text file containing license information
- _README.md_ - Readme file for GitHub
- _package.json_ - A file specifying which packages should be installed by NPM, in addition general application information (name, version, license, etc).
- _server.js_ - The primary Node file used to start the server and initialize necessary services / frameworks for the application (i.e. connecting to the Mongo database, intializing Express, etc).

**app** - The directory containing the "behind-the-scenes" (i.e. controllers) and server-side JavaScript files (i.e. routes).

- **common** - This directory contains any files with functionality that is used across all controllers
	- _ajax-functions.js_ - This file holds AJAX functions which are used across both client-side controllers
- **config** - The directory containing configuration files for Passport's GitHub Authentication
	- _auth.js_ - File that contains the API key information. These are encrypted "tokens (passwords)" issued by GitHub and used to authenticate with GitHub's servers.
	- _passport.js_ - JavaScript file containing all setup information for Passport.
- **controllers** - Directory for client and server-side controller files. Controllers are used to either manipulate / modify the view or the model (i.e. the database).
	- _clickController.client.js_ - Client-side controller which creates event listeners for the button clicks and asynchronous data requests to the clicks API.
	- _clickHandler.server.js_ - This is a server-side controller that tells Mongo what to do when a particular HTTP request is made (i.e. GET, POST, etc).
	- _userController.client.js_ - This is another client-side controller that retrieves user information from the API and updates the DOM elements with a successful API call.
- **models** - Directory for database models. In this case, this is where the Mongoose schemas will be defined. These models are definitions of desired data structure that will be inserted into the database.
	- _users.js_ - The Mongoose model for "users."
- **routes** - This folder contains route files. Routes give directions on what to do when a particular URL or HTTP request is made from the client (i.e. browser) to the server.
	- _index.js_ - contains route code for the application

**public** - This directory contains information used to render the view (i.e. css & images).

- **css** - Contains the style sheet for the application
- **img** - Contains any images used in the view (i.e. the Clementine.js logo)
- _index.html_ - This file contains all HTML code to render the view for this single-page application.

[Back to top.](#top)

### Ports and MongoDB Collection

Clementine.js uses port 3000 for the application and the default MongoDB port of 27017. These can both be changed within the `server.js` file.

MongoDB will use the database `clementinejs` and the `users` collection. These can be amended in the `server.js` and `/app/models/users.js` files respectively.

### User Model

The User model is located within the `/app/models/users.js` file, and follows common Mongoose conventions for model / schema creation.

```js
{
	github: {
		id: String,
		displayName: String,
		username: String,
      publicRepos: Number
	},
   nbrClicks: {
      clicks: Number
   }
}
```

- `github`: An object containing GitHub user information
	- `id`: The numeric ID associated with the GitHub account
	- `displayName`: The combined first and last name of the GitHub user
	- `username`: GitHub username
	- `publicRepos`: The number of public repositories owned by the GitHub account
- `nbrclicks`: An object containing information for the click part of the application
	- `clicks`: The number of times the button has been clicked. This value will be set to `0` when the user is first created.

[Back to top.](#top)

### Clicks API

The clicks API is located at `/api/:id/clicks`, and has the following functionality:

- An HTTP GET request will query the database and return a JSON object mirroring the current document within the Mongo collection
- An HTTP POST request will increment the value of the `clicks` property in the database by one and return a JSON object with the updated value
- An HTTP DELETE request will update the current value of the `clicks` property, setting it equal to `0`.

[Back to top.](#top)

### Passport Configuration

The application must be registered with GitHub to work properly. GitHub API information is stored within `/app/config/auth.js`:

```js
'githubAuth': {
	'clientID': 'your-id-here',
	'clientSecret': 'your-secret-here',
	'callbackURL': 'http://localhost:3000/auth/github/callback'
}
```

Refer to [this section](#setup-github-authentication) for instructions on how to register your app with GitHub.

[Back to top.](#top)