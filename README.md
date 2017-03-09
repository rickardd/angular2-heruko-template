# Angular2Heroku

A template of a simple angular app deployed to heroku by following this guid. http://angularonrails.wpengine.com/deploy-angular-cli-webpack-project-heroku/

This project was created with angular cli...

- @angular/cli: 1.0.0-rc.1
- node: 7.4.0
- npm 4.0.5

This is the stages I did in order to deploy to Heroku.
Only javascript. The site will run on node on Heroku.


### Package.json

- Two extra scripts **preinstall** and **postinstall**
- Moved all dev-dependencies to normal dependensies.
- Changed **ng serve** to **http-server**

```
"scripts": {
  "ng": "ng",
  "start": "http-server",
  "build": "ng build",
  "test": "ng test",
  "lint": "ng lint",
  "e2e": "ng e2e",
  "preinstall": "npm install -g http-server",
  "postinstall": "ng build && mv dist/* ."
}
```
postinstall runs the build and then moves the outputted folder to the roo.

Created a new Heroku app.

```
$ heroku create <name>
```

committed all changes with git and then pushed them to Heroku


```
$ git push heroku master
```

I think the scripts preinstall and post install was meant to run automatically. They didn't so I tried

```
$ heroku run npm preinstall
$ heroku run npm postinstall
```
But that didn't work. I ended up run the scripts manually instead. Plus angular cli needed to be installed as well.

This worked.

```
$ heroku run npm install -g @angular/cli
$ heroku run npm install -g http-server
$ heroku run ng build && mv dist/* .
```