# Ready to code!

Now that we have reviewed the contents Ember CLI sets us up with for development, we are ready to get coding. One of the many commands Ember CLI provides us is `serve` which will launch the server with live-reload. Any time we make changes to the application we should see this instantly reflected in any of the browser we have open to the server.

0. `ember serve`
0. Visit [http://localhost:4200](http://localhost:4200) in your browser and you should see a message that says "Congratulations, you made it!" with a friendly Tomster wearing a construction hat. 

# Install Bootstrap

Let's use Bootstrap to make our website look nice. This step isn't strictly necessary, but it will make our application look nice.

```console
ember install ember-bootstrap
```

**ProTip™** As we mentioned, Ember CLI uses live reloading to show the latest changes to your browser without needing to reload the browser. As long as `http://localhost:4200/` is open, you'll see changes immediately. Neat! However, if you edit install addons like we just did, you will need to **stop** and **start** `ember serve` again. Then refresh `http://localhost:4200/` and you will see your changes.

You should now see that the font for "Welcome to Ember" has changed! 

Now let's add a big header introducing our blog.  Let's update our `application.hbs` file to add a jumbotron header and wrap our page content in a Bootstrap `container`. Edit `/app/templates/application.hbs` to match:

```
<div class="jumbotron">
  <div class="container">
    <h1>Bernice's Blog</h1>
  </div>
</div>

<div class="container">
  {{outlet}}
</div>
```

Our site should have refreshed in our web browser now, revealing a big header for our blog.

# Checkout our completed version

Throughout the workshop if you need to compare your app at a point in time to the steps in this workshop, head on over to the [ember-101-app repository][ember-101-app] where each step has been tagged to match this walk-through.

If you wanted to checkout the code at the end of this step, check out the `getting-started` [tag][getting-started-tag].

[ember-101-app]: https://github.com/sandiego-ember/ember-101-app/tree/master
[getting-started-tag]: https://github.com/sandiego-ember/ember-101-app/tree/getting-started