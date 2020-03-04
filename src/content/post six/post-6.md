---
title: "Building a Blog with React-Static and Strapi CMS - Part One"
date: "2020-03-03"
draft: false
path: "/blog/building-blog-with-react-static-strapi-cms-part-one"
---

I have several clients asking me for an alternative to the growing crop of website builders out there that offer speedy website creation with little or no coding involved. While they are certainly helpful creating a basic site quickly and economically, I often find these tools frustrating when clients request customization that's even a little outside of the box. 

After looking around at various options for a stack to develop SMB sites that kept the costs to an absolute minimum but also allowed the freedom to modify the site without few constraints I settled on [React Static](https://github.com/react-static/react-static) and [Strapi CMS](https://github.com/strapi/strapi/). For the database we will use MongoDB and for hosting we will use [Netlify](https://www.netlify.com/).

#### React Static

In their own words, "React-Static is a fast, lightweight, and powerful progressive static site generator based on React and its ecosystem. It resembles the simplicity and developer experience you're used to in tools like Create React App and has been carefully designed for performance, flexibility, and user/developer experience."

#### Strapi CMS

Strapi bills itself as, "...a free and open source headless CMS delivering your content anywhere you need.

- **Keep control over your data**. With Strapi, you know where your data is stored, and you keep full control at all times.
- **Self hosted**. You can host and scale Strapi projects the way you want. You can choose any hosting platform you want: AWS, Netlify, Heroku, a VPS, or a dedicated server. You can scale as you grow, 100% independent.
- **Database agnostic**. You can choose the database you prefer. Strapi works with SQL & NoSQL databases: MongoDB, PostgreSQL, MySQL, MariaDB, and SQLite.
- **Customizable**. You can quickly build your logic by fully customizing APIs, routes, or plugins to fit your needs perfectly."

#### Netlify

According to their website "Netlify is an all-in-one platform for automating modern web projects. Replace your hosting infrastructure, continuous integration, and deployment pipeline with a single workflow. Integrate dynamic functionality like serverless functions, user authentication, and form handling as your projects grow."

Thay also have a free tier which makes them a great choice for projects like this.

### Overview

As we've learned, this project will feature a Strapi backend connected to the React Static frontend using a GraphQL API and it will be hosted on Netlify. 

The local project directory will have two directories, one for the backend and one for the frontend. Scripts will allow you to start both local servers simultaneously or individually while building out the project.

The end result of this tutorial will be a blog site with a fully featured admin section and a clean, albeit simple, UI and UX  for visitors to the site.

### Installing CLI Tools

To install the React Static CLI tool with Yarn:

```
yarn global add react-static
```

Strapi gets installed during project creation so there's nothing to install for Strapi at this point.

###Setting up Directories

#### The Project Directory

The first step is to create a parent directory to hold both the frontend and the backend folders for our project and then `cd` into it:

```
~/my-dev-folder mkdir my-react-strapi-project && cd my-react-strapi-project
```

#### The Frontend Directory

Now we can run `react-static create` inside the project directory. This will create a new `frontend` directory and build the newly created React Static app inside. You will be prompted for a project name (frontend) and a template (blank) as shown below:

```
react-static create
? What should we name this project? frontend
? Select a template below... blank
Creating new react-static project...
```

Once the install is complete you will see something like the following:

```
[✓] Project "frontend" created (195.6s)

  To get started:

    cd "frontend" 

    yarn start - Start the development server
    yarn build - Build for production
    yarn serve - Test a production build locally
```

To make sure everything is installed correctly you can `cd frontend` and run `yarn start` from the command line. If all is well you can view the app by visiting http://localhost:3000 in your browser. 

For now let's shutdown the development server using Ctrl+C to stop it.

#### The Backend Directory

To install Strapi and create the backend directory for our project `cd ../` to return to the project directory and run:

```
yarn create strapi-app backend
```

 If you are referencing the Strapi docs on the GitHub you will notice that we are not using the `--quickstart` option, which installs an SQLite database. We are going to use Mongo so we'll need to select a few options during install. 

***Note: You will need to have MongoDB installed on your local machine to succesfully complete the following Strapi installation.***

Aside from selecting a custom install and Mongo you can just hit enter to accept the defaults, including leaving the username and password and authentication database blank:

```
success Installed "create-strapi-app@3.0.0-beta.18.8" with binaries:
      - create-strapi-app
Creating a new Strapi application at ~/dev/my-react-strapi-project/backend.

? Choose your installation type Custom (manual settings)
? Choose your default database client mongo
? Database name: backend
? Host: 127.0.0.1
? +srv connection: false
? Port (It will be ignored if you enable +srv): 27017
? Username: 
? Password: 
? Authentication database (Maybe "admin" or blank): 
? Enable SSL connection: No
```

Once installed you will see the following in your terminal:

```
Creating files.
Dependencies installed successfully.

Your application was created at ~/dev/my-react-strapi-project/backend.

Available commands in your project:

  yarn develop
  Start Strapi in watch mode.

  yarn start
  Start Strapi without watch mode.

  yarn build
  Build Strapi admin panel.

  yarn strapi
  Display all available commands.

You can start by doing:

  cd ~/dev/my-react-strapi-project/backend
  yarn develop

```

Following the instructions above, run `yarn develop` from the command line. Strapi will commence building your admin UI and once completed it will start the Strapi dev server and launch the app:

```
Building your admin UI with development configuration ...

✔ Webpack
  Compiled successfully in 22.28s

[2020-03-04T00:14:54.102Z] info File created: ~/dev/my-react-strapi-project/backend/extensions/users-permissions/config/jwt.json

 Project information                                                          

┌────────────────────┬──────────────────────────────────────────────────┐
│ Time               │ Tue Mar 03 2020 16:14:54 GMT-0800 (Pacific Stan… │
│ Launched in        │ 12618 ms                                         │
│ Environment        │ development                                      │
│ Process PID        │ 55633                                            │
│ Version            │ 3.0.0-beta.18.8 (node v13.4.0)                   │
└────────────────────┴──────────────────────────────────────────────────┘

 Actions available                                                            

Welcome!
To manage your project 🚀, go to the administration panel at:
http://localhost:1337/admin

To access the server ⚡️, go to:
http://localhost:1337
```

The first time you visit the admin route in your browser you will be prompted to enter a username and password for the admin user. Once you are logged in successfully you will be greeted by the welcome screen:

![image-20200303162319643](/Users/robinleboe/VS Code/robin-leboe-gatsby-blog/src/content/post six/image-20200303162319643.png)

For the time being let's quit Strapi using Ctrl+C and do a little housekeeping in our project directory.

### GraphQL

To use graphQL we need to add the Strapi GraphQL plugin from the command line. Make sure you are in the `backend` directory and then run:

```
yarn strapi install graphql
```

NOTE: you can also launch Strapi and install the plugin from the admin UI.

### Scripts

To make it easier to manage the backend and frontend development servers let's add some scripts:

```
cd ~/dev/my-react-strapi-project
touch package.json
```

Then using your favorite code editor add the following:

```
{
    "scripts": {
      "develop:yarn": "yarn && npm-run-all -p develop:yarn:*",
      "develop:yarn:backend": "cd backend && yarn develop",
      "develop:yarn:frontend": "cd frontend && yarn start"
    },
    "devDependencies": {
      "npm-run-all": "^4.1.5"
    }
}
```

This script uses `npm-run-all`, a CLI tool that can run scripts sequentially or in parallel. In this case the `-p` option is used to run both the backend and frontend develop:yarn scripts at the same time so that running `yarn develop:yarn` from the main project directory will simultaneously start the Strapi and React Static dev servers. Nice!

Of course you can run either `develop:yarn:backend` or ``develop:yarn:frontend` individually if you need to.

### Next Time

In the next installment we will build on the basic installation we have created and start setting up the Strapi backend, which will give us the shape of our GraphQL API.