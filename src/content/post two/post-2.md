---
title: "MERN Stack + GraphQL"
date: "2019-11-03"
draft: false
path: "/blog/mern-graphql"
---

It's Saturday so why not build a GraphQL server using Express? Coffee's on so here we go!

## Setting up the project

###Create and initialize the directory

To get started we're going to create a new directory for the project and init Git and NPM.

```
mkdir mern-graphql && cd mern-graphql
git init
npm init --yes
```

This will init a Git repo and create a package.json file with default values.

The result is a package.json that should look something like this:

```javascript
{
  "name": "mern-graphql",
  "version": "0.1.0",
  "description": "GraphQL server with the MERN stack.",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Robin Leboe",
  "license": "ISC"
}
```

Note that I changed the version number to 0.1.0, to reflect a best practices starting point for semantic versioning, added a description, renamed the default index.js to app.js and added my name to the author field.

 If you're using VS Code and have run the [Shell command to add it to your PATH](https://code.visualstudio.com/docs/setup/mac) you can launch the editor from the command line using `code package.json`.

###Install packages

The next step is to install the Express and GraphQL packages.  The `express-graphql` package provides Express with GraphQL superpowers. The `graphql` packages  library will let us build a GraphQL schema and execute queries against it.

`npm install express express-graphql graphql --save`

Before getting down to business we'll need a file for our application and files for a couple of other things. Let's create them from the command line.

`touch app.js .gitignore README.md`

With the `.gitignore` file created we'll add the `node_modules` directory to it. This will make sure our Node modules don't end up in our repo. Let's launch VS Code again, add `node_modules/` to .gitignore and save the file.

`code README.md`

```node_modules/
```

The last file we'll modify before we do out first commit is a markdown file called `README.md` .

 `code README.md` 

For now let's just add something simple as a placeholder and save the file. I added the following HTML:

```html
<h1 align="center">
  MERN and GraphQL Server
</h1>
```

At this point `git status` should show us what we've created so far:

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        app.js
        package-lock.json
        package.json
```

To get our local repo up to date let's stage the files and make our first commit:

```
git add .
git commit -m 'initial commit'
```

The next step is to create a GitHub repo and push to it. This step assumes we have a valid [GitHub](https://github.com/) account. We can either create the repo bu visiting GitHub with a browser or we can get the job done on the command line by replacing USER and REPO with actual values.

```
curl -u 'USER' https://api.github.com/user/repos -d '{"name":"REPO"}'
 
git remote add origin git@github.com:USER/REPO.git
git push origin master
```

## Setting up the application

For our next trick, let's create our main application file `app.js` in the root directory and configure it so that Express can interact with the GraphQL schema.

First let's require the packages we installed earlier and add areference to a schema file we'll create in a minute:

```javascript
const express = require('express');
const graphqlHTTP = require('express-graphql');
const schema = require('./schema/schema');
```

Next we'll add the basic code for the Express server and do some minor configuration.

```js
...
const app = express();

// route used as an endpoint for Graphql, 
app.use('/graphql', graphqlHTTP({
    // use this schema for the graph 
    schema,
    // use graphiql when hitting '/graphql' from the browser
    graphiql:true
}));

app.listen(4000, () => {
    console.log('Listening on port 4000');
}); 
```

Here we added a route for all GraphQL queries and configured graphqlHTTP to reference the schema we're about to create. We also enabled the [GraphiQL](https://github.com/graphql/graphiql) in-browser editor for working with queries.

###Adding a schema

The `schema.js` file is where we'll define information about our graph including:

- Data types
- Object relations 
- Data operations

To create the schema directory, schema file and launch VS Code execute:

`mkdir schema && touch schema/schema.js && code schema/schema.js`

Here's what we're building. You can cut and paste the code below into the schema.js file and read through the comments for further explanation.

```js
// get the graphql package
const graphql = require('graphql');

// assign graphql types to consts using destructuring
const {
    GraphQLObjectType,
    GraphQLString,
    GraphQLID,
    GraphQLInt,
    GraphQLSchema,
    GraphQLList
} = graphql;

// hard-coded data
var guitars = [
    { name: "ES-339", year: 1998, id: 1, makerID: 2 },
    { name: "Stratocaster", year: 1963, id: 2, makerID: 1 },
    { name: "JEM777", year: 1987, id: 3, makerID: 3 },
    { name: "Telecaster", year: 1969, id: 4, makerID: 1 },
    { name: "Les Paul", year: 1957, id: 5, makerID: 2 }
]

var makers = [
    { name: 'Fender', country: "USA", id: 1 },
    { name: 'Gibson', country: "USA", id: 2 },
    { name: 'Ibanez', country: "Japan", id: 3 }
];

const GuitarType = new GraphQLObjectType({
    name: 'Guitar',
    // wrap fields in a function, we dont want to execute until init is complete
    fields: () => ({
        id: { type: GraphQLID },
        name: { type: GraphQLString },
        year: { type: GraphQLInt },
        maker: {
            type: MakerType,
            resolve(parent, args) {
                return makers.find((item) => { return item.id == parent.makerID });
            }
        }
    })
});

const MakerType = new GraphQLObjectType({
    name: 'Maker',
    fields: () => ({
        id: { type: GraphQLID },
        name: { type: GraphQLString },
        country: { type: GraphQLString },
        guitar: {
            type: new GraphQLList(GuitarType),
            resolve(parent, args) {
                return guitars.filter((item) => { return item.makerID == parent.id });
            }
        }
    })
})

// RootQuery describes how users can interact with the graph and data
const RootQuery = new GraphQLObjectType({
    name: 'RootQueryType',
    fields: {
        guitar: {
            type: GuitarType,
            // argument passed by user while making the query
            args: { id: { type: GraphQLID } },
            resolve(parent, args) {
                // return guitar with id passed in as argument by user
                return guitars.find((item) => { return item.id == args.id });
            }
        },
        guitars: {
            type: new GraphQLList(GuitarType),
            resolve(parent, args) {
                return guitars;
            }
        },
        maker: {
            type: MakerType,
            args: { id: { type: GraphQLID } },
            resolve(parent, args) {
                return makers.find((item) => { return item.id == args.id });
            }
        },
        makers: {
            type: new GraphQLList(MakerType),
            resolve(parent, args) {
                return makers;
            }
        }
    }
});

// create a new GraphQL Schema with above options 
module.exports = new GraphQLSchema({
    query: RootQuery
});
```

To test things out run the following on the command line:

```
node app.js
```

You should see `Listening on port 4000` and hitting http://localhost:4000/graphql in your browser should launch the GraphiQL in-browser editor.

Clicking the Docs link on the righthand side of the GraphiQL editor will let you view the various elements of the schema.  Clicking on the links and bread crumbs at the top will let you move up and down through the objects and field of the schema.

GraphQL is a powerful challenger to the traditional REST API and it's certainly something we should all be paying attention to. In an upcoming post we're going to take a look at some other apps and frameworks that have sprung up in the GraphQL ecosystem.

That's it for today! Until next time...