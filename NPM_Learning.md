npm help--> To view Help

Using npm with "-h" on any specific command will provide the different ways in which a specific command can be used.
eg: npm -h search

The different ways to search for the package are as follows:
    1.Use the command "npm search" on your terminal.
    2.Go to npmjs.com and find package.
    3.Go to google.com and search for the package.

Installing a Package Locally
If a package is required just for a specific project, you can install the package locally using:
    npm install <package name>

Installing a Package with Dependencies
    Usually, packages contain references to a number of other packages. npm , by default, installs all the inner dependencies (packages) while installing a package.

Uninstalling Packages
    You can uninstall packages using the command "npm uninstall <package name>"

Installing Packages Globally
    npm , by default, installs packages and their dependencies locally. The functions of these packages can be directly referenced within the application.

    However, certain packages like grunt, bower, karma, jshint and so on, need to be installed in a global context so that they can be used in CLI function of node.js.

    Packages can be installed by using -g or --global commands.
        npm install <package name> -g
    NOTE: Packages that are installed globally can not be referred from within the application.

    What happens during global installation?
        When you install a package globally:

        It downloads the files into the global node_modules directory.

        It also creates the command in the bin directory and links it to the package.

    Now, run "npm config get prefix". This shows exactly where these node_modules and bin directories are.

    Permissions for Global Installation
        While installing packages globally, if the permissions are not set correctly, you might run into EACCES error.

        Easy way to fix the error is to use : 
        In Linux:
            sudo npm install <package name> -g
        In Windows:
            Go to the Environment Variables under Properties from My Computer.
            Find NODE_PATH under System Variables
            Set the folder path to the npm directory

                    or
            create a directory and run "mpm config set prefix directory" and
            add this directory path to user PATH variable
        
Semantic Versioning in npm
    npm follows Semantic Versioning (semver) for its packages.

    Semantic Versioning is a specification where a version is represented by three numbers that represent major/minor/patch version numbers.

    Consider a package "lodash 4.17.2". Here, 4 represents major version number, 17 represents minor version number and 2 represents patch version number

        Major Version number: Gets incremented when new features that are not backward compatible are introduced. 
            E.g.:         Angular 1, Angular 2

        Minor Version number: Gets incremented when a new feature is added and does not break any of the existing functionalities.

        Patch Version number: Gets incremented whenever a bug fix or other minor updates are done.

Installing the Right Version
    Sometimes you may want a specific version of a package and not the latest one. In such cases, you can use the   following approach.

    Install package with a specific major, minor version, and the latest patch version.
        npm install react@15.5 --save
    Install a specific major version and the latest minor and patch version.
        >npm install react@15 --save
    Install the latest version.
        >npm install react --save

Checking for Outdated Packages
    You should update the packages often so that new features that come with every release of the package are available for use in the project.

    For this, first you will need to check if there are any dependency packages that are not the latest.
        >npm outdated

Updating Packages
    Running "npm update" from the project directory will update all packages in the project to the latest version.

    However, it is possible that you may not want the latest version for all dependency packages. In such cases, you can update a specific package.

    //Update all dependencies and dev dependencies
    >npm update 
    //Update a specific package to latest version
    >npm update lodash --save
    //Update just the dev dependencies
    >npm update --dev --save-dev
    //Update all packages globally
    >npm update -g
    //Update npm to latest requires administrative privileges
    >npm install npm@latest -g

Understanding package.json
    Before you create a package, you should be familiar with package.json file.

    package.json is a file that holds package metadata and gives information to npm when you execute the command "npm view".

Creating package.json
    First, create a directory "chanu" 
        >mkdir chanu
        >cd chanu
    This is the directory where all project dependencies will be installed. Now, create a package.json file using:
        npm init
    You will need to answer a series of questions. By the end of this, you can see a package.json file created in   "chanu" folder.

    check for the bootstrap versions available and install the required version.
        //View the latest version
        >npm view bootstrap version 
        //View all available versions
        >npm view bootstrap versions
        //Install required version
        >npm install bootstrap@3.2.0 --save

        You can notice that an entry is made in the "dependencies": section of the package.json file.

        Note: --save ensures the application dependencies are added in package.json file.

    >npm install <package> --save-dev
        You will notice that <package> is registered as a dependency for development in package.json file under "devDependencies" section. when it moves to production it will not be included

    npm list
    This lists the entire tree of dependency packages installed. You can restrict the number of branches shown, using the command "--depth"
        >npm list --depth 0
        >npm list --depth 1

## publishing package 
    Naming your Package
        The first step towards publishing is to name your package.

        It is recommended to keep the package name simple, easy to remember and relevant to its functionality. A few popular npm packages are:
            express
            request
            async
        Note: Package names should be unique. To check if a package name has been taken, plug the package name to the following URL: https://www.npmjs.com/package/packagename.\

    Creating a User
        To publish a package, you need to have access to the npm Registry.

        Create a User directly from the CLI. Enter the username, password and e-mail address, when prompted.
            npm adduser
        Check if user details have been stored locally:
            npm config ls
        To check if the user is created on the registry, go to https://www.npmjs.com/~username

    Publishing the Package
        Once you create the user, execute npm publish command from the package folder. This will upload the package into the npm registry.

        Unless ignored by a local .gitignore or .npmignore file, everything in the directory will be included
        
        The package will not be published if there is an existing package with the same name.

        To check if the package is published, go to [https://www.npmjs.com/package/packagename].
    
    Updating the Package
        You can update the package using npm version <update_type>

        Here, update_type is one of the semantic versioning release types- patch/minor/major.

        This command updates the version number in package.json.

        Once the version number is updated, use npm publish to update the package.

        To check if the updated package is published, go to https://www.npmjs.com/package/packagename.

        Note: The README displayed on the site will not be updated unless a new version of a package is published. So you need to run npm version patch and npm publish to have a documentation fix displayed on the site.

    Package Documentation
        Every package should have a README.md file, where you will explain what the package is for and give instructions on how to use it.

        This is useful for others to get a quick understanding of the package and to decide on which package to use.

        Also, the content in the README.md needs to be in Markdown for better readability.

## NPM with github
    Step 1: Create a directory for your new package.
        mkdir <packagename>  
        cd <packagename> 
    Step 2: Log on to Github and create a new repository for the package. Initialize the git repository from npm and connect it to your GitHub Repo.
        git init  
        git remote add origin https://github.com/{github username}/<repositoryname>.git  
    Step 3: Create package.json file.
        >npm init
        npm will automatically detect the git repository you've configured in Step 2. 
    Step 4: Create index.js file. This will be the entry point to the package and will be run first when you execute "npm install <packagename>". Add a simple code in the index.js file. 
        Example:
            function isNullOrEmpty(input) {
               // Returns true if the input is either undefined, null, or empty, false otherwise
                return (input === undefined || input === null || input === '');
            }
            // Export to make the function available to other packages
            module.exports = isNullOrEmpty;
    Step 5: Github creates README.md by default while creating the repository. Pull this file into npm package.
        >git pull origin master
    Step 6: Update README.me with details of the package.
        # <packagename>
        <Description of what the package does>
        ## Usage
        Install the package using npm :
         npm install is-null-or-empty --save
        Then, require the package and use it:
         [Comment: To check if this usage is proper]
         var isNullOrEmpty = require('is-null-or-empty');
         console.log(isNullOrEmpty("")); // true
         console.log(isNullOrEmpty("Hello World")); // false
    Step 7: Commit all new files to git repository.
        >git add index.js package.json example.js README.md
        >git config --global user.email "your git email add"
        >git config --global user.name "your git user name"
        >git commit -m "Initial commit"
        >git push origin master
    Step 8: Finally,
        Login: If you are a registered user of npm registry, log in to npm registry using "npm login". Else, create a new user using "npm adduser" from your npm terminal.

        Go ahead and publish the package!
            >npm publish
        Now, you must be able to view your new package in https://www.npmjs.com/~yourusername
        You can remove these test packages anytime from the registry using,
            >npm unpublish --force

## NPM Scoped Packages
    Scope is like a namespace for a package. A user or an organization can opt to have all their packages published under one scope.

    Scope folder is referred as "@" followed by the name of the scope like username/an organization.
        @scopename/packagename

    With over 500,000 packages already registered in the npm registry, scoped packages will allow users to worry less about a package name being already taken.

    Note: Scoped modules, require a version of npm greater than 2.7.0.

    Using a Scoped Package
        Installing a scoped package:
            npm install @scopename/packagename –save
        Configuring package.json:
            {
              "dependencies": {
              "@scopename/packagename": "^1.0.0"
              }
            }
        Using in a require:
            var mypackage = require("@scopename/packagename")
    Initializing a Scoped package
        While creating a scoped package using npm init, add the created scope as an option to that command.

        npm init --scope=scopename
        In the package.json file, refer the package name as:
            {
              "name": "@scopename/packagename"
            }
    Publishing a Scoped Package
        By default, the scoped packages are private. Publishing and downloading private modules requires a paid subscription to npm registry.
    
        However, public scoped modules don't require a paid subscription. They are free. To publish a public scoped module,set the access option while publishing it.
            npm publish --access=public

    Private Packages in npm
        All scoped packages in npm are published as private by default. These packages are in private scope with access restricted to few users, who can collaborate to build/use the package.

        To publish a package as private:

            >npm publish 
            //OR
            >npm publish --access restricted
        These packages can be used along with the public packages in the same project without any issues.

        To change a package from a public to private scope:

        >npm access restricted <package_name>
        This will ensure that the package is removed from listings on the site.
    
## NPM useful commands
    npm prune
        npm prune is a way to clean up your package. During development, you might end up installing packages to try something and later against using it.

        Prune is a way to removes all those packages that are not listed as dependencies in the package.json file.

        To list all packages that are used by the project as well as the ones installed and not in use,
            >npm list --depth 0
        Run the prune command to remove/unbuild all packages that were identified as extraneous.
            >npm prune
    
    npm Search
        npm search command searches the registry and package metadata and returns packages matching the search terms.
        Syntax: npm search [-l|--long] [--json] [--parseable] [--no-description] [search terms ...]
        Options used to filter and format search results:
            --no-description: Omits search on package description.
            --json: Returns results as a JSON array.
            --parseable: Returns results as rows with tab-separated columns.
            --long: Displays entire package details across multiple lines. When disabled, results are neatly fit into a single line.
            searchexclude: Displays options separated by space and filters the search results.
            Ending a search term with ~ (eg: rea~) Returns all packages starting with "rea".

    npm Dedupe
        npm installs the entire dependency package tree by default. However, when you install multiple packages for a project, there is a high possibility of same package being installed multiple times, owing to it being an inner dependency for multiple packages.
        This behavior slows down the project installation.

        This is where Npm dedupe comes to rescue.

        "Npm dedupe" searches the local package tree and reduces duplicates by moving dependencies further up the tree.     

    npm Shrinkwrap
        npm shrinkwrap locks down the version numbers of installed packages and their descendant packages.

        It helps you to use same package versions on all environments (development, staging, production) and also improve download and installation speeds.

        You can execute npm shrinkwrap after installing packages using npm install. This will create a new npm-shrinkwrap.json file with information like package version and the descendant packages being used.

    npm run
        While npm is a great package manager, it has the capability to run tasks in a packages lifecycle, making it a great tool for build scripts. It can very well do all that the build tools like grunt and gulp can do, with less maintenance overhead.
        >npm run <args>
            Arguments in the npm run refer to property in the scripts object configured in package.json file. This will execute the value of the property as a command in the operating system's default shell.

        Consider scripts module in package.json file:
            "scripts": {
                "patch-release": "npm version patch && npm publish && git push --follow-tags"
              }
            Running "npm patch-release" will update the version in package.json, commit the change, publish the changed package to npm and push the changes to GitHub. Note: "npm run" can be used not only on the globally available commands, but also on the modules installed as dependencies.

        Here is another example that depicts the usefulness of the npm run command.

            "scripts": {
                "build": "...",
                "git-commit": "git add -A . && git commit -a -m 'gh-pages update'",
                "git-push": "git push origin gh-pages --force && git checkout master",
                "deploy": "npm run build && npm run git-commit && npm run git-push"
              },
            With this script, deploying your project is as easy as running "npm run deploy".
