# my-angular-seed

My-angular-seed is a project, derived from the [Yeoman angular project build](https://github.com/yeoman/generator-angular).  This seed is "good to go," for my TDD/bdd development and set up for easy Heroku deployment.  It 

* has 1.2.x AngularJS build; 
* has a specially configured grunt server for use with single page applications;
* Assumes you are building the application from scratch, there is application scaffold apart from a very thin `index.html` and a trivial `app.js`.
* has karma installed and configured to use ngRoute, and angular-test-scaffold.

## Installation

Assuming you have installed node, and globally installed generator-angular, you can start cooking with:

```bash
git clone wizardwerdna/my-angular-seed foo
cd foo
npm install && bower install
```

Proceed at your own pace and style.  I tend to fire up tmux, run 'grunt server', and in a new page begin editing an integration test, usually
named something like `test/spec/integrations/integration.js` or the like.  I will blog on my style for developing angularjs apps shortly.

## Single Page Application Development Server

The default server configured with generator-angular fires up a browser, runs the application, and monitors the app directory for changes, with liveupdates upon change.
However, when your SPA application attempts to reload an internal route, such as //foo/first/second/third, the server does not recognize this as a static file, and
returns a 404.  Thus, when you are testing an internal page and the browser liveupdates, you end up getting a 404, and must restart your app from scratch.  The server
configured with my-angular-seed passes the 404 to the SPA, so that it can route and respond as you see fit.

## Heroku Deployment

A basic node webserver and procfile are provided to facilitate deployment of the app to heroku.  You might find deployment straightforward with the following strategy:

1.  Install the heroku toolkit, if you haven't already done so.
1.  Create and initialize your new application on Heroku.

```bash
heroku create <your-app-name>
```

1.  Each time you are ready to deploy:

```bash
grunt build
git add -A
git commit -m "<your message identifying the new build>"
git push heroku master
```

1.  After deployment, run the application wth

```bash
heroku ps:scale web=1
heroku open
```

Enjoy. 
