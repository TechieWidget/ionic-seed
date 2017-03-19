Ionic v1 Seed
=====================

A rather opinionated starting project for all Ionic v1.x projects. Features:

- **Proper component based** application architecture
- ES6 / Babel
- Webpack
- ngAnnotate
- SCSS
- Unit testing harness setup Karma, Jasmine, and Sinon
- Production builds

## Why should you use this?

The default project architecture generated by the Ionic CLI is fine for hobby projects, but it quickly runs out of steam when your team and application need to scale. This project is setup [using Google's best practice guidelines for AngularJS projects](http://angularjs.blogspot.com/2014/02/an-angularjs-style-guide-and-best.html), and includes everything you need to get started with unit tests. 

If you're planning on upgrading to Angular 2 / Ionic 2 in the near future and need to start a new project **today**, using this project will ease the transition to the `@Component` architecture that Angular 2 brings to the table. Controllers in this seed are completely void of Angular specific syntax, which means they can be ported over to the new architecture quite easily when the time comes. 

## Using this project

```bash
$ git clone --depth 1 https://github.com/ModusCreateOrg/ionic-seed
$ npm install -g ionic
$ npm install
$ ionic serve

# add platforms
$ ionic platform add ios
$ ionic build ios
```

## Gotchas
The first time you run `ionic serve`, a browser will open and likely give you
an error, something like `Cannot find www/index.html`. This seems to be due
to the Ionic CLI not waiting until all gulp tasks are complete.

If you wait until Webpack is done, and all gulp tasks are complete, the app
will load. You shouldn't run into this error again.

## Structure
The seed is broken down into the following structure:
```
| app
| ─┬ components
|  └── ...
| ─┬ views
|  └───┬ about
|       └── ...
|           (module definition, controllers, tests, template, scss)
| ─┬ services
|  └── ...
| ─┬ assets
| ─┬ scss
```

In a typical mobile app environment, **views** are single representations of a screen. These would be the best representation of a true "angular module". Whether this be an "About" screen, Settings, etc. Think about breaking down your views into components that use `<ion-view view-title="...">`. These high level components will be the containers for your other re-usable components.

The root level **components** folder is a place to keep re-usable `.directives` or `.components` -- depending on your use case. This would typically be the place to put components that are **not view specific**. A good example would be the `userMenu` component -- something that could be used across multiple views. 

Another good example of a component would be a side menu. Taking the `<ion-side-menus>` code from `index.html` and extracting it into a re-usable component -- possibly with different states depending on authentication, device, etc. Perhaps you use a Modal dialog multiple times to confirm information. Display variations of a form. All of these are good examples of elements that should be broken down into components. 

## Testing
All test code resides with the component or view, ala `about.spec.js`. All test files should be named `*.spec.js` for the test harness to work properly. This seed is setup to use PhantomJS for test running, but can easily be adapted to use anything. Mocha provides a nice debug interface for running individual tests, as well as seeing test pass/fail status. 

When Karma is running, open `http://localhost:9876/debug.html` in your browser.

![chai](https://dl.dropboxusercontent.com/spa/pkr1d5uhq1t8wz1/4q69b1bw.png)

There are 2 gulp tasks available for running tests.

`$ gulp test`

Will start a Karma server, run tests, and then exit.

`$ gulp tdd` 

Starts a Karma server in watch mode.

### Testing References
- [SinonJ](http://sinonjs.org/docs/)
- [Chai](http://chaijs.com/guide/)
- [Mocha](https://mochajs.org/)


## Issues

- There is no indication when Webpack is done compiling unless you have your terminal open. Maybe look into something like https://www.npmjs.com/package/gulp-notify-growl to make this more clear.

## TODO
- examples of ngCordova integration
- examples of e2e testing?
