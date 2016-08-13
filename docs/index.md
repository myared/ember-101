Welcome to **Free Ember Workshop** hosted by [Ember.js Louisville](emberlou).

# Pre-event setup instructions

[![Ember Setup Instructions](images/video-title.png)](https://vimeo.com/174148994)

0. Install **nvm** by pasting the following command into your terminal window: 
	* `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash`
	* Once installed, you need to either close your terminal window and open a new one or source your new changes as shown in the video above.
0. Install **node** with nvm by pasting the following command into your terminal window:
	* `nvm install node`
0. Install **Ember** by pasting the following command into your terminal window: 
	* `npm install -g ember-cli`
0. You're ready to create a new project named **workshop** by pasting the following command into your terminal window: 
	* `ember new workshop`
0. Move into the **workshop** directory, and you're ready to get started!
	* `cd workshop`

# Reduce the glue

Web application development can involve a lot of repetition.  Attempts to reduce this repetition gave rise to a variety of scaffolding tools and best practices. These scaffolding tools are trying to reduce the amount of work necessary to get started by providing a set of best practices that are enabled default.  

Choices that are oftentimes left to developers include:

* Setting up an application's directory structure
* Creating generators for common scenarios
* Determining which build system to use
* Compiling and minifying assets
* Chooing a testing framework

# Ember CLI

[Ember CLI][ember-cli] is a command line interface (CLI) that helps manage and enforce conventions of the Ember framework. We'll dive into these choices in more detail later, but at a high level Ember-CLI builds in:

* A broccoli-powered asset pipeline
* A strong conventional project structure
* A powerful addon system for extending Ember
* The QUnit testing framework
* Dependency Management
* Runtime configuration options

# Modules

Modules allow you to divide logical portions of code into smaller, functional pieces and include them as needed. As your application grows, smaller pieces of functional code become easier to manage, support, maintain and test. To learn more about JS Modules, check out [jsmodules.io][jsmodules]

# Naming best practices

0. Code
    0. `TitleCase` naming of classes
    0. `camelCase` naming of attributes
    0. use modules, avoid globals
    0. reusable code → components, mixins, add-ons
0. Files
    0. `kebab-case-naming.js`
    0. children in subdirectory → `routes/invoices/edit.js` & `routes/invoices/new.js`

[bower]: http://bower.io/
[ember-cli]: http://ember-cli.com
[emberlou]: https://www.meetup.com/Ember-js-Louisville/
[npm-g-without-sudo]: https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md
[node-install]: https://nodejs.org/download/
[git-scm]: http://git-scm.com/downloads
[npm-no-sudo-script]: https://github.com/glenpike/npm-g_nosudo
[jsmodules]: http://jsmodules.io
[ember-cli]: http://ember-cli.com