# Blog post model

For our test application, we're going to create a blog. Let's start off by using a generator to create a model for the blogPost.

```console
$ ember generate model blog-post
installing model
  create app/models/blog-post.js
installing model-test
  create tests/unit/models/blog-post-test.js
```

OK, Ember-CLI has just created for us both a model file in `app/models` and a test file in `tests/unit/models`.  Let's take a look at the model and see what it contains:

```js
import DS from 'ember-data';    
                                
export default DS.Model.extend({
                                
});                             
```

What is the funky `import` and `export` syntax?  Welcome to the world of tomorrow! Those `import` and `export` statements use ECMAScript 6 module syntax. Thanks to the magic of transpilers, we can use future syntax today even though browsers don't yet support the standard. This should look familiar if you have used Node.js or AMD modules. We're importing a module from 'ember-data'.  Then we're extending the `Model` class and using that as our module export.

Now each model should specify the fields that each object of that type contains. In our case, we want a
blog to include a `title` and a `body`. These are both `string` fields but maybe
we should keep track of when a blog post was published. We'll call that
`publishedDate`. Perhaps it's no surprise, but that field is of type `date`.

Inside of the `DS.Model.extend({})` object, we can add the necessary lines for these fields:

```js
  title: DS.attr('string'),
  body: DS.attr('string'),
  publishedDate: DS.attr('date')
```

Your file should now look like the following.

```js
import DS from 'ember-data';    

export default DS.Model.extend({
  title: DS.attr('string'),
  body: DS.attr('string'),
  publishedDate: DS.attr('date')
});
```

## Test our blog post model

Testing can seem daunting if you put it off for too long so lets get right to it and write a test for that model we just created. Ember-CLI has us covered. When we generated our blog post model Ember-CLI also generated a test module for our model:

```console
$ ls tests/unit/models
blog-post-test.js
```

Pretty cool, huh? Let's open up `tests/unit/models/blog-post-test.js` and see what Ember-CLI generated for us:

```js
import { moduleForModel, test } from 'ember-qunit';

moduleForModel('blog-post', 'Unit | Model | blog post', {
  // Specify the other units that are required for this test.
  needs: []
});

test('it exists', function(assert) {
  let model = this.subject();
  // let store = this.store();
  assert.ok(!!model);
});

```

That looks like a lot! First is the `import` statement. This imports the `moduleForModel` and `test` helpers we will need from `ember-qunit` for writing our test.

The first section you see, `moduleForModel`, is where any necessary loading for the model testing will be done. Each unit test is self-contained, so any dependencies (for example if one model depends on another) must be defined here. We don't need to worry about this for our simple blog post model _yet_.

The next section, `test`, shows how we define an individual test. One test can have many assertions but should test only one thing. The generator created a default test which asserts that our model exists.

Since we have about as much as we can test in here already for our small model, let's make sure the tests pass by visiting [http://localhost:4200/tests](http://localhost:4200/tests) in your browser.

# Adding blog posts to the homepage

## Create an index route

If we want to see blog posts on our website, we need to render them into our HTML.  Ember's view layer places routes and their associated URLs front and center.  The way to show something is to create a route and associated template.

Let's start once again from a generator, this time for our index page route:

```console
$ ember generate route index
installing route
  create app/routes/index.js
  create app/templates/index.hbs
installing route-test
  create tests/unit/routes/index-test.js
```

**ProTip** If you ever need to know what generators are available, just type `ember help generate` and enjoy a deliciously long list of generating goodness.

This creates a few files for our index route and template file.

Looking at `app/routes/index.js` we see:

```js
import Ember from 'ember';

export default Ember.Route.extend({
});
```

## Update an index template

Let's take a look at the template file that was generated for us in `app/templates/index.hbs`:

```handlebars
{{outlet}}
```

All we see is something called `{{outlet}}`. Ember.js uses handlebars for templating, and the `outlet` variable is a special variable that Ember uses to say "insert any child templates here". This is similar to `yield` if you've worked with Ruby on Rails before. We're not adding any child templates to our `index` template, so let's remove the `{{outlet}}` and add a sample post:

```html
<article>
  <header class="page-header">
    <h2>My Blog Post</h2>
  </header>
  <p>This is a test post.</p>
</article>
```

Go look at the website in your browser again. Our 'My Blog Post' header should appear nicely beneath our big site header.

## Putting our posts on the page

So far we have only put some HTML on our page. Let's use the API to show our actual blog posts.

First let's add a `model` to our route in `app/routes/index.js`. One of the jobs of routes is to provide a model to their template. Our model should be a list of blog posts retrieved from our API.

We could manually provide list of blog posts as our model:

```js
import Ember from 'ember';

export default Ember.Route.extend({
  model() {
    return [{
      title: "First post",
      body: "This is the post body."
    }];
  }
});
```

Instead, let's use the data store to retrieve all of our blog posts:

```js
import Ember from 'ember';

export default Ember.Route.extend({
  model() {
    return this.store.findAll('blog-post');
  }
});
```

Now we should update our index template to loop over each of our blog posts and render it:

```handlebars
{{#each model as |post|}}
  <article>
    <header class="page-header">
      <h2>{{post.title}}</h2>
    </header>
    <p>{{post.body}}</p>
  </article>
{{/each}}
```

The handlebars `each` helper allows us to enumerate over a list of items. `each` is considered a block helper due to the use of `{{#each}}` and `{{/each}}`. The `as |post|` syntax sets `post` as a local variable for the duration of the block. 

After making this change, let's check out our homepage in our browser. You should now see two blog posts!

# Additional Blog post route(s)

What if we want to share a link to one of our blog posts?  To do that, we would need a page for each blog post.  Let's make those!

## Create the route

Let's start by using a generator to make the new files we'll need:

```console
$ ember generate route blog-post
installing route
  create app/routes/blog-post.js
  create app/templates/blog-post.hbs
updating router
  add route blog-post
installing route-test
  create tests/unit/routes/blog-post-test.js
```

This creates a few files, and also adds some stuff to your  `app/router.js`:

```js
import Ember from 'ember';                  
import config from './config/environment';  
                                            
const Router = Ember.Router.extend({        
  location: config.locationType,            
  rootURL: config.rootURL                   
});                                         
                                            
Router.map(function() {                     
  this.route('blog-post');
});                                         
                                            
export default Router;                      
```

Ember generated a route definition for us. This type of route would be useful for a static page, like `about` or an index of Blog Posts. We need to make a small modification to give us the URL we want (`/posts/1`) as well as give us a way to determine the post id from the URL. The `path` option to a route definition allows us to just that:

```js
Router.map(function() {                     
  this.route('blog-post', {
    path: '/post/:blog_post_id'
  });
});                                         
```

This tells the Ember Router how to construct the URL, including a dynamic segment of `:blog_post_id`. This dynamic segment will be extracted from the URL and passed into the `model` hook on the `blog-post` route. We can then use this parameter to look up that exact `blog-post` in the data store. So let's open up `app/routes/blog-post.js` that was generated for us and do just that.

_Note: you can also pass `--path=/post/:blog_post_id` when generating a Route to do this step automatically._

```js
import Ember from 'ember';

export default Ember.Route.extend({
  model(params) {
    return this.store.findRecord('blog-post', params.blog_post_id);
  }
});
```
## Update the template

In order to make sure this is working, let's add some markup to `app/templates/blog-post.hbs` that will display a post. This file doesn't exist yet, so be sure to add it.

```handlebars
<article>
  <header class="page-header">
    <h1>{{model.title}}</h1>
  </header>
  <p>{{model.body}}</p>
</article>
```

Since we happen to know there is a blog post with `id: 1` on our API server, we can manually visit `http://localhost:4200/post/1` in our browser to test with an example blog post.

# The magic of Ember-Data

Ember-Data gives us conventions that map ORM methods like save and delete to API URLs and HTTP Verbs. As long as our API follows these conventions, we have to write little code to fetch and save data. Our API is following the [JSON API specification][jsonapi]. So, we can take full advantage of Ember Data's defaults. If you need to work with an API that doesn't conform to Ember Data's built in conventions, don't worry. One of the great things about Ember Data is that it is flexible enough to adapt to any backend.
Here is the default mapping Ember Data Methods to API URLs and HTTP Verbs:

| Ember Data Method | API HTTP Verb | API URL |
| --- | --- | ---|
| findRecord('blog-post', 1) | GET | /blog-posts/1 |
| findAll('blog-post') | GET | /blog-posts |
| post.save() _(assuming post with an id)_ | PUT | /blog-posts/:blog_post_id |
| store.createRecord('blog-post') or post.save() _(post without id)_ | POST | /blog-posts |
| post.deleteRecord() + post.save() or post.destroyRecord() | DELETE | /blog-posts/:blog_post_id |

**ProTip** The store action determines the model name based on the defined dynamic segment. In our example `:blog_post_id` contains the proper snake-case name for our model with the suffix `_id` appended.

To confirm that this works, **delete the `app/routes/blog-post.js` file** and verify that our blog post page (http://localhost:4200/post/1) still works properly after reload.

Ember-CLI created a route test file automatically as well. To make sure your tests continue to pass, if you delete `app/routes/blog-post.js` you should also delete `tests/unit/routes/blog-post-test.js`

# Handlebars link-to helper

Now that we have unique URLs for each blog post, we can link to these URLs from our index route.

To add these links open up the `app/templates/index.hbs` file and add a `link-to` Handlebars helper around our blog title:

```handlebars
{{#each model as |post|}}
  <article>
    <header class="page-header">
      <h2>
        {{#link-to 'blog-post' post}} {{post.title}} {{/link-to}}
      </h2>
    </header>
    <p>{{post.body}}</p>
  </article>
{{/each}}
```

Now take a look at [http://localhost:4200](http://localhost:4200) and title links should appear. **Click it!** And now you're at the page for our blog post.

# Acceptance testing

With some user interaction added to our application we can now create an acceptance test. The user flow for this test will be:

0. Visit `/`
0. Click the first blog link
0. Verify that the URL now matches `/post/:blog_post_id`

First we will have to generate our acceptance test.

```console
$ ember generate acceptance-test blog-post-show
installing acceptance-test
  create tests/acceptance/blog-post-show-test.js
```

Open the created file `tests/acceptance/blog-post-show-test.js` and see what is there:

```js
import { test } from 'qunit';
import moduleForAcceptance from 'workshop/tests/helpers/module-for-acceptance';

moduleForAcceptance('Acceptance | blog post show');

test('visiting /blog-post-show', function(assert) {
  visit('/blog-post-show');

  andThen(function() {
    assert.equal(currentURL(), '/blog-post-show');
  });
});
```

Let's first rename this test to something more applicable and remove the stuff inside.

```js
test('visit blog post from index', function(assert) {

});
```

There are a few helpers available to us that we will use **a lot** when writing acceptance tests.

* `visit(route)`: Visits the given route
* `click(selector or element)`: Clicks the element and triggers any actions triggered by that element's click event
* `andThen(callback)`: Waits for any preceding promises to continue

Since `visit` and `click` are both asynchronous helpers we need to wrap subsequent logic in `andThen` to make sure actions complete before continuing onto the next step.

The really cool thing about asynchronous test helpers is that they run in a queue, automatically waiting for any previous asynchronous test helpers to finish running.

We will now code the steps listed above to test that we can link to a blog post from index.

```js
test('visit blog post from index', function(assert) {
  let blogSelector = 'article:first-of-type a';

  visit('/');
  click(blogSelector);
  
  andThen(function() {
    assert.equal(currentURL(), '/post/1');
  });
});
```
Verify the tests are passing by visiting [http://localhost:4200/tests](http://localhost:4200/tests) in the browser.

# Recap

We now:

* have blog posts
* are able to retrieve them from an API and list them
* can view individual posts
* have an acceptance test that ensures the functionality to visit an individual post works

If you wanted to see the code at the end of this step, check out the `step3` branch using the following command: `git checkout step3`.

[jsonapi]: http://jsonapi.org
