# Accessing our API with ember-data

Ember is a client side framework, so we need an API (backend) when we have data that we want to persist. We will use our API to serve blog posts and to allow users to view and submit comments.

We could use fixtures or a mock API to do this, but some friendly developers have already made a working API for us. The API is setup at [https://emberlou-workshop.herokuapp.com](https://emberlou-workshop.herokuapp.com) supporting the following endpoints

| Verb | path | Description |
| --- | --- | --- |
| GET | /blog-posts | List of blog posts |
| GET | /blog-posts/:id | Retrieve a blog post |
| PUT | /blog-posts/:id | Update a blog post |
| DELETE | /blog-posts/:id | Delete a blog post |
| GET | /comments | List of comments |
| POST | /comments | Add a comment |
| GET | /comments | Retrieve a comment |
| PUT | /comments/:id | Update a comment |
| DELETE | /comments/:id | Delete a comment |

Our API uses `snake_case` in the JSON it sends, the convention for Ruby on Rails APIs. Ember expects everything to be `camelCase`. 

So how can we connect these two nicely? Let's create an Ember Data adapter to consume our API and adapt the API responses to what Ember expects.

## Application Adapter

We could create adapters at a model level, but let's create one for the entire application since we'll be using the same API for all our models. Type the following line into terminal: `ember generate adapter application`

```console
$ ember generate adapter application
  installing
    create app/adapters/application.js
  installing
    create tests/unit/adapters/application-test.js
```

Let's open up that adapter and see what is there:

```js
import DS from 'ember-data';

export default DS.JSONAPIAdapter.extend({
});
```

We're using an Ember Data built-in adapter called the JSONAPIAdapter. Building a custom adapter isn't too hard, but we don't need to because we're going to use the default.

The last step we need to take is to point our Ember app to the API we want to use. Hit `CTRL-C` to stop Ember from running and restart Ember using the `ember serve` command with the `--proxy ` flag to point to our API. 

0. Close ember by pressing `CTRL-C`
0. Type `ember serve --proxy https://emberlou-workshop.herokuapp.com` in your terminal window.

```console
$ ember serve --proxy https://emberlou-workshop.herokuapp.com
Proxying to https://emberlou-workshop.herokuapp.com
Livereload server on http://localhost:49152
Serving on http://localhost:4200/
```
If you wanted to see the code at the end of this step, check out the `step2` branch using the following command: `git checkout step2`.