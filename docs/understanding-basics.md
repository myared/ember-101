# Project Organization

In the [Pre-event setup instructions][pre-event] section you generated a new ember project called `workshop`. Let's step inside and start exploring:

```console
$ cd workshop
$ ls -1
README.md
app
bower.json
bower_components
config
ember-cli-build.js
node_modules
package.json
public
testem.js
tests
vendor
```

## Node Modules

The first file and directory to inspect are those provided by [npm][npm]:

* `package.json`
* `/node_modules/`

`package.json` contains a list of the versioned npm modules necessary for this app. Included are broccoli and Ember CLI. We won't need to edit this file because we're using Ember CLI to manage it. 

The `node_modules` folder is where npm modules are installed. As a result, any package specified in `package.json` will live in the `node_modules` directory.

## Bower Components

The next thing to look at is the file `bower.json` and the `bower_components` directory. These are like `package.json` and `node_modules`. 

Bower has become the standard for frontend package management. Our Ember CLI application will use bower to manage some of our dependencies. Open `bower.json` to see that our app comes with Ember, Ember Data (for data persistence), and QUnit (for testing).

## Tests

Ember CLI comes out-of-the box with a testing framework and provides some helpers to make testing easier. You can test models, routes, components, and user stories.

**Unit tests** allow us to focus on specific functionality of a module and do not require the entire Ember app to be running. 

**Integration tests** are for testing components in isolation. 

**Acceptance tests** are for testing high level stories. They emulate user interactions throughout your app and you can make assertions about the expected functionality.

## Public and Vendor

You may be wondering where images, fonts and other miscellaneous asset files should go. The answer is the `public` directory. These will be served at the root of your application.

Similarly, you may have JavaScript or CSS dependencies that are not in bower. These can be stored in the `vendor` directory. Loading vendor files is not something we will cover in this workshop.

## App

The `app` directory is where we're going to put all of our own application code.  It is carefully structured with an appropriate place for each type of module:

```console
$ ls -1
app.js
components
controllers
helpers
index.html
models
resolver.js
router.js
routes
styles
templates
```

Some of these may sound familiar to you, while others may be brand new.  Don't worry yet if you don't know what all of these different pieces are.  We'll get to them one-by-one.

[pre-event]: index.md#pre-event-setup-instructions
[npm]: https://www.npmjs.com/