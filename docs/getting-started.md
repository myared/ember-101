# Ready to code!

Now that we have reviewed the contents Ember CLI sets us up with for development, we are ready to get coding. One of the many commands Ember CLI provides us is `serve` which will launch the server with live-reload. Any time we make changes to the application we should see this instantly reflected in any of the browser we have open to the server.

0. `ember serve`
0. Visit [http://localhost:4200](http://localhost:4200) in your browser and you should see a message that says "Congratulations, you made it!" with a friendly Tomster wearing a construction hat. 

# Add our own Template

Let's get rid of the default construction Tomster by adding our own template with the following command:

```console
ember generate template application
```

Now let's add edit our new application template (located in `app/templates/application.hbs`) and add the following HTML inside:

```console
<h1>My Blog</h1>
```

Once you save, visit [http://localhost:4200/](http://localhost:4200/), and you should now see a header that shows "My Blog" at the top. Great work!

# Install Bootstrap

Let's use Bootstrap to make our website look a little better. This step isn't strictly necessary, but it will make our application look nice. 

```console
ember install ember-bootstrap
```

**ProTip** As we mentioned, Ember CLI uses live reloading to show the latest changes to your browser without needing to reload the browser. As long as `http://localhost:4200/` is open, you'll see changes immediately. Neat! However, if you edit install addons like we just did, you will need to **stop** and **start** `ember serve` again. You can stop your ember application by pressing `CTRL-C`. After restarting ember with `ember serve`, visit `http://localhost:4200/`, and you will see your changes.

You should now see that the font for "Welcome to Ember" has changed. Note: `ember-bootstrap` uses extra components that you may not want to add to your application. If you want to stay as minimal as possible, ask an instructor what other options exist.

Now let's add a big header introducing our blog.  Let's update our `app/templates/application.hbs` file to add a jumbotron header and wrap our page content in a Bootstrap `container`.

```
<div class="jumbotron">
  <div class="container">
    <h1>My Blog</h1>
  </div>
</div>

<div class="container">
  {{outlet}}
</div>
```

Our site should have refreshed in our web browser now, revealing a big header for our blog.

# Checkout our completed version

At the end of every section, you can compare your code to our code. It's hosted at the following repository: [ember-101-app repository][ember-101-app]. If you wanted to see the code at the end of this step, check out the `step1` [branch][step1-branch] using the following command: `git checkout step1`.

[ember-101-app]: https://github.com/myared/ember-101-app/tree/master
[step1-branch]: https://github.com/myared/ember-101-app/tree/step1