### Deploy on Day Five


### Objective

Students are to deploy their projects to Heroku


### Overview

Deploying to a webservice is one of the final steps in your journey to become a developer. Much like your first day at Flatiron "Deploy on Day One" we will be working to get your MVP's on the internet. The process of "spinning up" services has for a long time been a very difficult process. However, with the advent of services such as Heroku this process gets easier.

### Why deploy projects to Heroku

This makes testing your applications easier. Production environments aren't as forgiving as development environments and will require extra setup. It also allows you to send it to friends/classmates to bug test. Often as developers we are too close to the project to objectively test.



## How to deploy


To deploy your application to heroku follow the steps below

Create an account on Heroku

Install the Heroku CLI toolbelt

`brew install heroku`

To use the toolbelt you will need to login to your heroku account.

`heroku login`

Once you are successfully logged in, navigate to your project. To deploy to Heroku you must use git. In the same way we push our code from our local environment to Github, we will be pushing our code to Heroku. Once Heroku receives our code it will then begin to build the remote environment and run our application. **NB** The remote environment is a server somewhere that requires its own setup.

When building your project, you will most likely have a React frontend and Rails backend. There are two ways of deploying this type of setup. Option 1 is the easiest and will require you to setup two separate remote environments. We will deploy your backend and frontend separately. Your Rails API and the React application will each have their own server (remote environment on Heroku). The other option involves having Rails serve up your React frontend, this will require a deep knowledge of the Rails Asset Pipeline and Webpack. We discourage this type of setup for final projects.

#### Deploying to Heroku

**Your frontend and backend should be tracked separately in git (They should live in separate repos). If this is not the case see an instructor**


#### Rails


Inside your rails folder, type the following in your terminal.

  `heroku create`

This will create a new Heroku application and will provide you with the url for your application.

In your Gemfile, it is advised that you specify the version of ruby you are working with. At the bottom of the Gemfile, add the line ruby '2.X.X' where X is the version you wish to work with. Once you have made that change make sure all your files are committed


`git add .`

`git commit -m "Some message"`

Before pushing verify that you have a Heroku remote add. You are most likely accustomed to using the command `git push origin master`. `origin` is the remote used to push to Github. If you type `git remote -v` You should see 4 entries: Two for Github (fetch & push) and two for Heroku (fetch & push). If this is not the case your project is not connected to your Heroku remote. **See instructor**


Once your files have been committed push your files to Heroku.

  `git push heroku master`

Be sure to read the messages that your console prints out. This will let you know if about any issues during the deployment. If you do make any changes to correct deployment issues **make sure to commit changes**.


Once this is done test your Heroku website by typing `heroku open`. This will open a new tab and open your url.

##### Testing your website

This may mean different things for different projects, generally speaking you will want to deploy your frontend (React) in order to test your application from a user's perspective. For some it may mean trying to login and seeing if you get back a JWT token for some it may mean navigating to some static page. Do what makes sense for your application. **Your development database is not your production database** This is important to note as students sometimes expect to see data that they used on their development machine (localhost) on their production site (Heroku). This is where running your migrations and seeding your database comes in.

In terminal run `heroku run rails db:migrate`. This will execute this command in the terminal on your production machine and will run your migrations. **Watch out for any errors**. Once your tables have been created you make run `heroku run rails db:seed` to run your seed file.

#### React

Navigate in to the folder with your frontend. **Your frontend should be tracked separately in git from your backend**

Be sure to commit your code before attempting to do anything further.

Create a new Heroku application by running `heroku create --buildpack https://github.com/mars/create-react-app-buildpack.git`

We are using a buildpack here which will tell Heroku how to configure our application to work with our create-react-app based application. To learn about buildpacks read more here [See more here ](https://devcenter.heroku.com/articles/buildpacks).

Once your Heroku application is created and you have committed your changes, you must push your application to Heroku.

In terminal type `git push heroku master`. Once your files are uploaded Heroku will build your application.

You may encounter some issues with a package-lock.json and a yarn.lock. The error messaging will tell you to remove one or the other. Type `git rm ****` to accomplish this. To complete this be sure to commit your code and push your code.

Once the build is successfully type `heroku open` to see your frontend. Be sure to update your frontend code so it is able to access your new backend website. You can either hardcode this value (**Not recommended**) or you may use [environment variables](https://devcenter.heroku.com/articles/config-vars)

### Resources

[Deploying Rails to Heroku](https://devcenter.heroku.com/articles/getting-started-with-rails5)
[Mars Create React App buildpack](https://github.com/mars/create-react-app-buildpack)
[Heroku Procfiles](https://devcenter.heroku.com/articles/procfile)
[Heroku Buildpacks](https://devcenter.heroku.com/articles/buildpacks)
