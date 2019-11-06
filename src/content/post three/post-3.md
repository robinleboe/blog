# Basic tools setup with macOS Mojave

I recently started tooling up a new dev environment on a MacBook Pro running Mojave. There are lots of things to configure and a few gotchas so I thought I'd document the process in case it saves someone time and and helps keep the frustration level to a minimum. 

### Grab a Brew

Hailed as 'The missing package manager for macOS', [Homebrew](https://brew.sh/) is one of the most popular package managers for macOS. To see if it's installed already you can check using

```
brew --version
```

If you discover it is already installed you should probably run 

```
brew update
```

followed by

```
brew doctor
```

to  make sure everything is up to date and working correctly. If you don't have Homebrew installed installation is easy, just paste this line into macOS Terminal and hit enter. Note the backslash character at the end of line one that  continues the Bash script on the line below:

```
`/usr/bin/ruby -e "$(curl -fsSL \ https://raw.githubusercontent.com/Homebrew/install/master/install)"`
```

For this and each of the following installations it is advisable to re-check the version post install just to make sure that everything is ok and that you're getting the correct version.

### Xcode Command Line Tools

To check and see if the Xcode Command Line Tools are installed or not you can run the following code from the Terminal command line:

```
/Applications/Xcode.app/Contents/Developer/usr/bin/xcodebuild -version
```

If the tools are installed fter a few seconds you should see something like the following:

```
Xcode 11.2
Build version 11B52
```

If you don't you can run the following to install them:

```
xcode-select --install
```

If you are installing or updating the Xcode you MUST accept the license when prompted. If you don't get the prompt there are various solutions to the issue [on the web](https://www.google.com/search?rlz=1C5CHFA_enCA720CA720&biw=1440&bih=798&ei=dBbCXZ2fDcmm0wT8jYqACQ&q=xcode+command+line+tools+accept+license&oq=accept+license+xcode+command+line+tools&gs_l=psy-ab.1.0.0i8i30.2619.8201..9351...1.3..0.325.3654.0j3j11j1......0....1..gws-wiz.......0i71j0i8i7i30.3Ya40cJi6aM).

### Node Version Manager

Like the name suggests, Node Version Manager is a handy tool for selecting different versions of Node.js. To see if it's installed check the version:

```
nvm --version
```

If you don't have it you can install it from the command line. Note the backslash character at the end of line one that  continues the Bash script on the line below:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | \
bash (https://github.com/nvm-sh/nvm#installation-and-update)
```

### Node and Node Package Manager (NPM)

Once again you can check for an installation by using:

```
node --version
```

and 

```
npm --version
```

If you need to install these the easiest route is to use Homebrew:

```
brew install node
```

### Git

Lather, rinse... check for a Git version!

```
git --version
```

If it's not installed you can either:

````
brew install git
````

or

```
https://www.atlassian.com/git/tutorials/install-git#mac-os-x
```

should you get a warning:

```
Warning: /usr/local/bin is not in your PATH
```

you will need to add the following to your .bash_profile to prepend the newly installed version of Git:

```
export PATH="/usr/local/bin:${PATH}"
```

This prepends the Git installation directory to your existing PATH variable.

### Just an opinion

The installations above are pretty standard and not very controversial. The next steps in my setup process take us into the weeds of subjectivity, especially in the choice of IDE. I am using VS Code and I am finding it light weight, very well supported and easy to use. In a future post I'll go over the installation and explain some of the choices I made in terms of plugins and other configuration decisions.

Happy Brewing!

