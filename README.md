# Tutorial: Deploying a basic Ruby on Rails app on Jekyo

Demo app [here](https://rails-demo.jekyo.app/)

### Prerequisites

Make sure you have [NodeJS](https://nodejs.org/en/download/), [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) and [git](https://github.com/git-guides/install-git) installed.

If it's your first time using **Jekyo**, you can **install** it by running the following command in your terminal:

`npm install -g jekyo`

### Sign in to Jekyo

You can sign in to Jekyo by running `jekyo user:signin`

```
➜  ~ jekyo user:signin 
Your email?: **************
Your password?: **********
You have successfully signed in!
```
If you don't have a Jekyo account, you can create one in the terminal by running `jekyo user:signup`. 

## 1. Create a basic Ruby on Rails app

You can start your Ruby on Rails project by using `jekyo create`

Using the **arrows** on your keyboard, select **rails** and press **enter**.  
```
? Select template
  None Creates only the application
  expressjs A basic app skeleton using [Express](https://expressjs.com/)     
  nuxt-js A boilerplate SSR application using [Nuxt.js](https://nuxtjs.org/) 
❯ rails A basic starter app using [Ruby on Rails](https://rubyonrails.org/)
```
When prompted, enter the desired name for your Ruby on Rails app. 

`Application name?: rails-tutorial`

This will create a basic Ruby on Rails app in the current directory by cloning this [Ruby on Rails starter app](https://github.com/jekyo/rails-getting-started) repository.

```
Cloning source code... OK
Application created!
```

### Deploy the Ruby on Rails app on Jekyo

To deploy the app, first navigate to the newly created directory:

`cd rails-tutorial`

Now you can deploy this app to Jekyo by running: 

`jekyo deploy`

After a while, you should see something like this:

```
➜  Fetching source code ... OK
➜  Building application, this might take a while ... OK
➜  Publishing application, this might take a while  ... OK
➜  Deploying application ... OK        
➜  Waiting for application to start ... OK
➜  Visit your app on: https://rails-tutorial.jekyo.app ... OK
```

You can now browse to your Ruby on Rails app on https://rails-tutorial.jekyo.app (replace 'rails-tutorial' with your app name)

## 2. Deploying an existing Ruby on Rails app

### Make sure to use PostgreSQL

When creating a rails app, pass the PostgreSQL database flag:

```
rails new blog --database=postgresql
```

We won't use SQLite because the containers are stateless. 

### Generate a controller

If you haven't done so already, generate a controller:

```
rails generate controller hello
```

### Index file

Make sure you have an index file, in our case in **views/hello** `index.html.erb`: 

```
<html>
    <h1>Hello, world!</h1>
</html>
```

### Edit routes.rb

Edit the `routes.rb` file found in **blog/config** and add a root line:

```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  root 'hello#index'
end
```


### Install webpacker
```
bundle exec rails webpacker:install
```


### Commit changes

Initialize a git repository if you haven't already done so by running `git init`. 

```
git add .
git commit -m "initial commit"
```

### Create an empty Jekyo app:

`jekyo create` 

Select 'none' using the **arrows** on your keyboard and press **enter**. This will create an app using your current directory. 

```
? Select template (Use arrow keys)
❯ None Creates an application from your current directory
```

Name your app: 

`Application name?: blog`

Run `jekyo link` to link your local app to the remote Jekyo app. Select 'blog' using the **arrows** on your keyboard and press **enter**.

```
? Select application (Use arrow keys)
❯ blog
```
### Now you can deploy this app to Jekyo by running: 

`jekyo deploy`

After a while, you should see something like this:

```
➜  Fetching source code ... OK
➜  Building application, this might take a while ... OK
➜  Publishing application, this might take a while  ... OK
➜  Deploying application ... OK        
➜  Waiting for application to start ... OK
➜  Visit your app on: https://blog.jekyo.app ... OK
```

You can now browse to your Ruby on Rails app on https://blog.jekyo.app (replace 'blog' with your app name)

## Pushing local changes to Jekyo 

Add the newly modified file(s) to the git index by using [git add](https://www.atlassian.com/git/tutorials/saving-changes)

`git add filename`

Create a [git commit](https://github.com/git-guides/git-commit)

`git commit -m "your commit message"`

Now, simply deploy your app again:

`jekyo deploy`

You will see your changes on your live app after a short while. 