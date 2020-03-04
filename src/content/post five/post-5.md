---
title: "Full Stack Dev Environment with Express and React"
date: "2019-11-26"
draft: false
path: "/blog/full-stack-express-react-setup"
---

Since I am working on several full stack JS projects at the moment launching and running both Express and the dev server for the client at the same time seemed like an idea whose time has come.

### Overview

The structure uses a common directory with sub-directories for the React client and Express server apps. A `package.json` file in the common folder holds an `npm start` script that launches both Express and the React development server simultaneously. Handy.

This run through uses `create-react-app` to spin up a boilerplate React app with all the trimmings so if you don't have that installed you can run `npm install -g create-react-app` in your terminal to install it globally. 

###Setting up React things

With `create-react-app` installed the next thing to do is to create a parent directory to hold both the client and the server folders and `cd` into it:

```
~/my-dev-folder mkdir my-full-stack && cd my-full-stack
```

Now we can run `create-react-app` inside the parent directory. This will create a new `client` directory and build the newly created React app inside:

```
create-react-app client && cd client
```

Since `create-react-app` takes care of installing everything we can initialize the application by running:

```
npm start
```

If all is well you can view the running React app by visiting http://localhost:3000 in your browser. 



You can now shutdown the development server using Ctrl+C.

### Why?

VS Code has macOS, Linux and Windows covered for one. It's also a performant, tightly integrated development environment that features a snappy source code editor with multi-language support. VS Code also sports syntax highlighting, bracket-matching, auto-indentation, box-selection, snippets, and a whole lot more. Other features include  IntelliSense code completion, effective code refactoring options and an integrated Terminal view that supports multiple sessions.

Debugging is also front and centre with Visual Studio Code. The interactive debugger let you step through code, inspect variables, view call stacks, and execute commands right from the console. Git support is also baked in so you can commit your work without leaving the app. 

### Extensions Galore

One of the many benefits of VS Code is the sheer number of handy extensions available. Here is a short list of must-have plugins (as of this writing!):

#### ES Lint

This is one of the most downloaded extensions for VS Code. [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) integrates automatic formatting and linting with your editor. It is highly recommended.

![](./es-lint.png)

#### Prettier

[Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) formats your code __consistently __ so you don’t have to sweat it. It does a great job and is very popular with over 7 million downloads.

![](./prettier.png)

#### Bracket Pair Colorizer

Identifying matching brackets in deeply nested code is a real pain. The [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) extension correlates  brackets by identfying them with matching colors. Do yourself a favour and grab this one.

![](./bracket-pair-colourizer.png)

#### Debugger for Chrome

While console.log is handy for debugging the official [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) extension takes things to a whole new level, allowing you to use Chrome's debugger directly in VS Code.

![](./chrome-debugger.png)

####Live Server

The [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension provides an easy to use development server with live reload for both static and dynamic pages. It's quick and easy to spin up a server when you need one directly from within VS Code.

![](./live-server.png)

####Path Intellisense

[Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense) helps you automatically complete filenames while editing. Looking up path names for files or directories can be a real pain. This extension provides file and directory name intellisense completion which can save a lot of time and reduce the number of errors created by incorrect paths in your code.

![](./path-intellisense.png)

### Themes Aplenty

Another benefit of VS Code's popularity is the abundance of themes available. The default installation comes with a fair number of themes available from Code > Preferences > Color Theme. You can also install other themes from VS Code's built-in Marketplace. My favorite theme of late is [Monokai++](https://marketplace.visualstudio.com/items?itemName=dcasella.monokai-plusplus). It's a dark but highly readable theme that works really well for me.

![](./monokai.png)

### Make it Your Own 

As previously mentioned there are loads of extensions and themes available for download on the VS Code Marketplace. Beyond that though there is a whole other realm of customization available to you by tweaking the parameters found in Code > Preferences > Settings. This includes all kinds of tweaks that are well beyond the scope of this post. There is also a comprehensive and customizable list of keyboard shortcuts which are especially welcome if you're coming from another editor and can't live with out the muscle memory :)

### In Conclusion 

VS Code's popularity, extensions and community support make it a worthwhile investment. The learning curve was minimal for me coming from Sublime Text and the added power of the extensions I use daily have made it a central part of my work flow.