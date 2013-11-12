# MEAN (Mongo Express Angular Node) seed
*MongoDB, Express.js, AngularJS, Node.js + Yeoman (Grunt, Bower, Yo) + Jasmine, Karma, Protractor*

This is project is meant to be a starting point for full stack javascript (Angular + Node) HTML5 websites and mobile apps (cross platform, responsive, can optionally be wrapped with TriggerIO, Phonegap, etc.).
- It's meant to be:
	- more specific than barebones language specific seeds such as angular-seed so you can start out with core functionality such as user login, sign up, forgot password, etc. out of the box, BUT:
	- broad and modularized enough to be used for a wide variety of applications. Angular and Node are the core technologies and Express, Mongo (using mongodb-native) and Grunt are pretty heavily integrated but all other technologies can be swapped as needed with a little bit of work.

- mongodb-native is used (rather than mongoose) as the npm plugin for the node-mongoDB interface.
- Other key technologies used:
	- Yo - scaffolding tool.
	- Grunt.js - build tool.
	- Bower - frontend dependency management.
	- Jasmine - testing framework - used for both frontend (with Karma) and backend (with jasmine-node) testing. Can switch in other testing frameworks in place of Jasmine if you want.
	- Protractor - frontend E2E tests
	- LESS - CSS pre-processor. Twitter Bootstrap CSS framework is currently NOT used but can be easily integrated. SASS/SCSS/Compass can be switched in instead of LESS pretty easily as well. The main reasons for going with LESS by default are because it seems to compile a bit faster and because Angular UI and Twitter Bootstrap use LESS so it makes it easier to develop/augment those.
- For a full list of dependencies / technologies see below, though many of the non-core ones can be switched out as necessary.
	- frontend: `bower.json` and `app/src/lib`
	- backend: `package.json`
- NO jQuery depdendency! (AngularJS is meant to be used with its included jqLite)
	
Feel free to add Yeoman builds and submit pull requests for other 'cores' (i.e. Mongoose instead of mongo-db-native, SASS instead of LESS, Mocha instead of Jasmine for backend tests, etc.).

Any suggestions for improvement are welcome!

### NOTE: if you are NOT using Facebook login, REMOVE the `facebook.all.js` file that's included in `buildfilesModules.json` since it's a HUGE (170kb minified!) file and thus a huge waste if you're not using it!


## Code standards and expectations

All code should be:

1. Linted
2. Tested
3. Well-documented, clear, and understandable
4. Maintainable, easy to change and update. Modular.
5. Performant
6. Well designed, with good UI, UX, and aesthetics (for frontend code)



## Limitations / Compatibility
- Built to be cross browser and cross platform (mobile, desktop, Windows, Mac, etc.) compatibile so it should work most everywhere
	- Exceptions - it will NOT work:
		- Internet Explorer <=9. Works on Internet Explorer 10+ (10 is the first version to support flexbox. It can work on IE9 without flexbox use but IE8 and below is iffy..)
	- Tested / should work on:
		- Chrome, Firefox, Safari, Internet Explorer 10+
		- Android 2.3+
		- iOS
		- should work elsewhere too but not rigorously tested outside the ones listed above
	- In total, should be about 85% coverage (IE 9, 8, 7, 6 make up about 15% market share as of 2013.07.21 - this number will go down with time as more people switch to IE10). See current statistics below; note they vary as these are all (very large) samples from different sites.
		- http://www.impressivewebs.com/browser-usage-stats/
			- http://gs.statcounter.com/
			- http://www.w3counter.com/globalstats.php


## Documentation

### API (rpc) documentation and interactive usage

Go to [server]/api/help - for example, `http://localhost:3000/api/help`.
There are subpages for each "group" of calls. These should be documented on the main help page, but in general each namespace has its own page. For example, the `Auth` module's calls may be found at `http://localhost:3000/api/auth/help`.

NOTE: for security/authorization, all backend calls should be checked (to ensure a user is logged in and has privileges to complete the request specified). To simulate this for the api/help, type your authority keys into the URL and they'll be read at GET params. For example, either using the interative help login call OR the site itself, login. A `user_id` and `sess_id` are return; set these in the URL as GET params (i.e. `?user_id=38asdlfk3&sess_id=alkjefe3dk`) and they'll be passed back on all calls to authenticate. Note - this still will NOT give you access to ALL calls UNLESS you're a super admin. Super admins fields on the user object must be manually set in the database (to prevent other people from making themselves a super admin).

### YUIDoc auto documentation, generated by grunt

- Frontend docs are in `yuidocs/frontend`. View them by opening `yuidocs/frontend/index.html` with a browser.
- Backend docs are in `yuidocs/backend`. View them by opening `yuidocs/backend/index.html` with a browser.


## Testing, Continuous Integration
- see `testing.md` and `continous-integration.md` files


## Grunt / build process

All files should be linted, tested, and well-documented - YUIDoc is used to auto-generate documentation for the both frontend and backend. Frontend files should additionally be concatenated and minified. Grunt is used for this purpose.

### Command-Line Usage

Run this from the root directory, where the `Gruntfile.js` is located.

```bash
grunt
```

This will auto-run tests, which will require 1 additional action on your part. Instructions should be detailed in command line Grunt prompts, but here's a summary of what to do:

1. Backend jasmine-node tests run on a **test** configuration with a **test** database, as determined by the `app/configs/config.test.json` configuration file. The tests make HTTP requests to the the corresponding test node server, so it must be running for these to work. Open a NEW command prompt (i.e. Terminal, Git Bash, Cygwin), then run node as usual with the following command line arugment: `config=test`.
```bash
cd /path/to/project
node run.js config=test
```


### Command-Line Usage, for production.

This will cause minified files to be referenced in the app's `index.html` file, among other things.

```bash
grunt q --type=prod
```

### Other Command-Line Grunt Tasks
There may be more than the ones listed below, but these are the most important. See `Gruntfile.js` for the full list.

```bash
# Run a subset of grunt build tasks, for quicker execution. This skips the tests, among other things. This will likely be your most common command as it needs to be run each time a .less or .html file changes.
grunt q

# Build YUI docs
grunt yui
```

### Versioning
The manual setup tasks (such as copying and updating `configs` or running `npm install`, `bower install`) need to be periodically updated. To ensure each server is up to date, grunt will not run unless the versions match accordingly.
- If you change `package.json` or a `configs` file, increment the `versions` key accordingly in `app/configs/config.json` and also update the `curVersions` object in `Gruntfile.js` to match. This will then prevent grunt from running until the local environment is brought up to date by re-syncing config.json or running npm install.
- After pulling code: Follow the console instructions upon running `grunt` if it says your files are out of date.


## Conventions / Style guide

TODO: Add final set of compiled and merged conventions.

In general, we try to follow "standards" with regard to javascript coding conventions. NOTE: see the below conventions as they OVERWRITE anything listed in the below links.
- http://javascript.crockford.com/code.html
- https://github.com/rwldrn/idiomatic.js/ (from http://addyosmani.com/blog/javascript-style-guides-and-beautifiers/ )
- https://npmjs.org/doc/coding-style.html

Additionally, all code is linted by grunt and thus must pass linting tests. The most important thing, however, is that all code be CONSISTENT and follow the same conventions. Here are some specifics:
- TAB characters should be used to indent, not spaces. (We use 4 spaces per tab.)
- Use YUIDoc-style documentation for all files: a general description at the top plus a table of contents (@toc) that summarizes the main functions and parts of the file. Each function should have its inputs and outputs (@param) detailed, together with example usage.
- Test files should be named with a `.spec.js` suffix as per the Jasmine specification.


## Frameworks, MVC (Model View Controller) and Flow
The app (both backend and frontend) follow MVC but the file structure is modularized (so the view, controller and model are typically in the same folder) as opposed to all the controllers in one folder, all the models in one folder and all the views in one folder as may be more common. The module approach allows for easier adding, editing, and removing of components since everything the module needs is right there in the same folder. Managing dependencies and connecting modules together is easier since things are more separated.

For the backend (node), `express` is used as the (lightweight) framework with MongoDB as the database. There is NO VIEW (just controller and models) as all view code is on the frontend exclusively. The backend is slim in that the vast majority of the time it only deals with interacting with the database. The 'controllers' are just the route management and the 'models' are just the functions that do the work of CRUD (create, read, update, delete) on the database. The steps are:
1. incoming request --> controller: the controller (router) receive a request (HTTP, AJAX from frontend)
2. controller --> model: the controller calls the appropriate model function to do the actual processing (CRUD)
3. model: the model does the work and returns the result
4. model --> controller: the controller takes the result from the model (typically via a promise or other asynchronous method)
5. controller --> outgoing response: the controller sends the result back as a response
All of the above is handled in 2 files - both in the `modules/controllers` folder.


	
## File Structure
- see `file-structure.md`


## Common actions
- see `common-actions.md`


## Git Workflow
** Make sure to run grunt and ensure all code is LINTED, TESTED and DOCUMENTED before submitting ANY code!! **

- GIT:
	- Make some changes (locally on your own computer).
	- Add them with `git add -A`.
	- Commit them with `git commit -m '[descriptive message here]'`.
	- Use `git pull <remote> <branch>` to sync your code with changes other coders may have made (i.e. `git pull origin master`).
	- Use `git push <remote> <branch>` to push your changes to re-sync the central repo (i.e. `git pull origin master`).
- Building (grunt)
	- Everytime you pull code, run `grunt` from the command line. Do this from the root folder of the site (the folder that has `Gruntfile.js` in it).
	- If `package.json` changed, first run `npm install` (again run from root folder) THEN run `grunt`.
	
- Best practices with GIT
	- commit, pull, and push often. At least once a day, often more. Each time you make changes and have a stable, bug free, complete version of the code, push/sync it. This will reduce frequeny of manual merge conflicts.
	


## Project Files

### Configuration
- see the `app/configs` folder for all the config.json files and examples. You can create as many configurations as you like and tell grunt which one to use when building your app.