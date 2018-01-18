# Angular App for [Acadview](https://acadview.com)

The app is built to consume a RESTful API.

In this app we are introducing a new frontend framework made using:

1. Angular JS a.k.a The view layer
2. Redux a.k.a. The single data store for proper data management
3. Redux Observable a.k.a The async tasks lib for doing async calls in redux
4. Angular Material a.k.a The framework for styling angular apps

# Table of Contents
1. [On Boarding](#on-boarding)
2. [Setting Up & Running on Local](#setting-up-and-running-on-local)
3. [Code Formatting](#code-formatting)
4. [General UI/UX guidelines](#uiux-guidelines)
5. [Resources](#resources)
6. [Code Architecture](#example)
    1. [Action performed by views are declarative](#action-performed-by-views-are-declarative)
    2. [Naming Pattern for Constants](#naming-pattern-for-constants)
    4. [Naming Pattern for Actions](#naming-pattern-for-actions)
    5. [Making the actions available in the view](#making-the-actions-available-in-the-view)
    6. [The two most common used reducer patterns!](#the-two-most-common-used-reducer-patterns)
    7. [What are Epics?](#what-are-epics)
    8. [What the hell is a Miner?](#what-the-hell-is-a-miner)
    9. [The container component pattern](#the-container-component-pattern)
    10. [Making the data and actions available to child components](#making-the-data-and-actions-available-to-child-components)
    11. [The graph-component pattern](Coming Soon!)
    12. [Leveraging Directives to manage UI](#leveraging-directives-to-manage-ui)
    13. [Writing Styles](#writing-styles)
    14. [Wrapping up a module](#wrapping-up-a-module)
    15. [Handling Mixpanel tracking calls](#handling-mixpanel-tracking-calls)
    16. [Handling internal tracking](#handling-internal-tracking)
    17. [The mysterious shared directory!](#example)
    18. [The Api service with endpoints](#example)
    19. [Stuff you might be wondering by now](#example) => `ngInject`
7. [Testing Architecture](#example)
    1. [Where are all the tests?](#example)
    2. [Testing reducers](#example)
    3. [Testing Epics](#example)
    4. [Testing Child Components](#example)
    5. [Testing Parent Components](#example)
    6. [Advanced Details around tests](#example) => `mocks,jest config`
    7. [Running Tests](#example)
8. [Directory Structure](#directory-structure)
9. [Why do I need to run `gulp watch`?](#example2)
10. [Tools Used](#tools-used)
11. [Deployment](#third-example)
12. [Get in touch?](#get-in-touch)


## On Boarding
This section is especially for contributors.
It contains the pre-requisites and resources to gain them.

It also contains what minimum portion should **beginners**
read from this *long* :stuck_out_tongue_winking_eye: manual.

#### Pre-requisites
1. Ability to convert Design => HTML + CSS.
<br> Resources: [Thinking in layouts] (Coming Soon!)
2. Basic knowledge of FlexBox
<br> Resources: [TODO]
3. Making responsive web with Angular Material using `layout` and `flex`
<br><br> Resources:
<br>[Angular Material Docs](#https://material.angularjs.org/latest/layout/introduction)
<br>[Layout Containers](#https://material.angularjs.org/latest/layout/container)
<br>[Layout Children](#https://material.angularjs.org/latest/layout/children)
<br>[Child Alignment](#https://material.angularjs.org/latest/layout/alignment)
<br>[Reponsiveness](#https://material.angularjs.org/latest/layout/options)<br><br>
4. Making reusable and nested css with scss
<br> Resources: [Sass Docs](#http://sass-lang.com/guide)
5. **In depth** knowledge of JS **(ES6)**.
<br> Resources: [You Don't know JS](#https://github.com/getify/You-Dont-Know-JS)
6. Basics of AngularJs
<br> Resources: [TODO (AV-notes)]
7. AngularJS components
<br> Resources: [Official Docs](#https://docs.angularjs.org/guide/component)
8. Basics of Redux
<br> Resources: [Redux by Dan Abramov](#https://egghead.io/courses/getting-started-with-redux)

#### What to Read?
If this is the first time you are contributing to this repo, do read
the following topics from this readme:

1. [On Boarding](#on-boarding)
2. [Setting Up & Running on Local](#setting-up-and-running-on-local)
3. [Code Formatting](#code-formatting)
4. [General UI/UX guidlines](#uiux-guidelines)

For advanced contributors, wanting to get deeper :smirk:, read up on:

1. [Code Architecture]
2. [Testing Architecture]
3. [Directory Structure](#directory-structure)
4. [Running Tests]


# Setting Up and Running on Local


Get ready to see this app in action on your machine :sunglasses:.

If you don't have node:
<br>`sudo apt-get install nodejs`

If you don't have npm:
<br>`sudo apt-get install npm`

*Make sure your versions pass the min criteria of
node@7.7 <br>
npm@4.4.
<br> Check using `node -v` and `npm -v`*

#### Follow the steps tp setup:

1. Clone the repo: (I hope you got this part)
2. `cd` your way into the `ngacad` directory.
3. Run `npm install -g gulp`.
4. Run `npm install -g jest`.
5. Run `npm install`.

#### Follow the steps to run

Both these commands are never ending, so make sure you run
then in diff terminals.

\[student, admin, support, instructor] => choose the app you want to run.

1. Run `gulp templates --appName=[student, admin, support, instructor]`
2. Run `npm run dev:[student, admin, support, instructor]`
3. Open you browser
4. Go to [localhost:8080]


**NOTE: These steps are only tested and trusted on Ubuntu 16+.
Not on Ubuntu? :cry:.***(Coming Soon!)*


# Code Formatting

Please follow, the following rigorously.

1. 2 Spaces for Indentation.
2. Two returns for horizontal spaces.

[TODO]: *A better approach Coming soon!*


# General UI/UX guidelines <a name="uiux-guidelines"></a>

When developing UI some of the guidelines are not explicitly mentioned
by the designer bu should be kept in mind:

1. All click-ables should have `cursor: pointer` property
2. For every modal, the width and height of the modal should be constant.
It should not change according to the content change inside it.


# Resources

For advanced and deep understanding:

1. [Using Angular 2 Patterns in Angular 1.x Apps](#https://egghead.io/courses/using-angular-2-patterns-in-angular-1-x-apps)
2. [Build Angular 1.x Apps with Redux](#https://egghead.io/courses/build-angular-1-x-apps-with-redux)
3. [Up and Running with redux-observable](#https://egghead.io/courses/up-and-running-with-redux-observable)
4. [Using Webpack for Production JavaScript Applications](#https://egghead.io/courses/using-webpack-for-production-javascript-applications)
5. [Writing Epic Unit Tests](#https://medium.com/kevin-salters-blog/writing-epic-unit-tests-bd85f05685b)
6. [Jest Docs](#https://facebook.github.io/jest/docs/en/getting-started.html)
7. [AngularJS using ES6](#https://github.com/michaelbromley/angular-es6)


# Code Architecture

The following patterns have been followed in the app: 

### Action performed by views are declarative 
All the actions performed by the view are *declarative* in nature. 

**Example Scenario**: If the on the button click an API has to be called and
the data fetched has to be displayed in the lower half of the page,
the view should not have any idea about how to do this.
Rather the view just dispatches and action saying `getData`.
The following tasks are performed by the **Epic**.

The epic will listen for this action and call the API to get the data.
When the data is fetched, the epic will
dispatch an action to save it in the redux store.
The redux store will in turn update the variables bounded to the view
thus re-rendering(updating) the view.

The view will just declarative-ly tell what it should be done and the
rest is handled by the `action-reducer-epic-action-reducer` equation.

### Naming Pattern for Constants
The naming of the action-constants should adhere to the following rules:

1. It should always start with a verb => `GET`, `SET`, `UPDATE`, `SHOW`,
`HIDE` etc.
2. The constants for making an AJAX call should exists in triplets
<br> `GET_DATA` => To initiate AJAX call.
<br> `GET_DATA_SUCCESS` => When the call is succeeded.
<br> `GET_DATA_FAILURE` => When the call fails.
3. Each module should have an **unique** string(name of the module in
all caps) that will be prefixed to the *value* of every constant,
just to make them unique with respect constants of other modules
in the app. <br>**Note:** We are not prefixing the constants but
just their value so as to make the use of it in the app easy, since it
would be very difficult to write constants with same prefix in the whole
module again and again.
4. General Pattern for making constants: <br>
`export const GET_DATA = '${prefix}GET_DATA'`

### Naming Pattern for Actions
The naming of the action should adhere to the following rules:

1. All actions should be made using the `actionFactory` by just
injecting the constant.
2. Name of the action should be exactly the name of the constants but in
**Camel Case**.

### Making the actions available in the view
To let the views dispatch actions directly, the following pattern
is being used:

1. An angular factory is being made.
2. All the actions that are required by the view will be imported from
actions.js into the factory file.
3. The factory is made to return those actions.
4. The factory is registered on the module.
5. The factory is then injected into the container component.
6. Finally the injected factory is then passed as the second parameter
to the redux's connect function, so as to wrap those actions into
dispatch calls.

### The two most common used reducer patterns
After writing a lot of custom reducers, we have finally came to a
conclusion that for the starting of the module we can use just the
two types of reducers for every key in the state.

These patterns have saved a lot of coding time by acting as a dummy
reducers till the time more complexity is being introduced into the
module. And most of the times these dummy reducers ends being the
full time main reducer.

These two reducers patterns are:

1. `dataSet`: This reducer, for a particular action will simply
take the data from the `action.payload` and sets it in the store. For
all other actions it returns the last state.
2. `dataFetch`: This reducer is a bit more complicated.
It acts on three actions: <br><br>
**The General One**: For this action the reducer will set
`isLoading: true` <br>
**The Success One**: For this action the reducer will take the data from
`action.payload` and set it in the store in the data
and also set `isLoading: false` <br>
**The Failure One**: For this action the reducer will take the error
from `action.payload` and set in the store in the error key and also set
`isLoading: false`

There is a 99% chance that you will have to make a lot of these reducers.
For the sake of saving time and keeping your code DRY we have take a step
forward and made two function factories to generate these reducers.

Yeah! you guessed it right the name of these factories are:

1. `dataSetReducer`: This factory takes 1 action and returns the
reducer of the type `dataSet`
2. `dataFetchReducer`: This factory takes 1 action and returns the
reducer of the type `dataFetch`. <br>
*Now you might be wondering that how does it generate a reducer that acts
on 3 actions by simply using 1 action. It leverages the naming pattern
of action and constants and assumes actions for **success** and
**failure**.*

### What are Epics? <a name="what-are-epics"></a>
Think of Epics as a kin of event listener so instead of listening to
events they listens to action(redux-actions) and performs some
tasks(async or tasks following async), but in the end they should return
an action by calling an action-creator.

These are mainly used for doing async calls or the tasks that follows
the async calls like selecting the default, redirecting to another url
all after the response of the AJAX call.

*NOTE: I am cutting a big corner here by not explaining what are
observables`*

It has multitude of operators that it uses to work on actions or more
aptly stream of actions. The ones we use are:

1. `ofType`: To specify which action should the epic listen for.
2. `filter`: This helps in **further** filtering the actions it is
listening based on some property like some key in the payload or state.
3. `switchMap`: To make an API call.
4. `map`: To convert an action into some other data to make the payload
for the API call or to other actions for dispatching
5. `do`: It comes in handy when you want to do some `console.log`-ing.

### What the hell is a Miner? <a name="what-the-hell-is-a -miner"></a>

A miner a container(angular service) of functions to access the state(redux store).

It serves two purposes:

1. Getting some date from the store to make some decision in the epic.
2. Making payloads for the API calls.

All the functions inside the miner have the same signature as mentioned
below:

```
<functionName>({<moduleName>: state}, <meta data>) {
  // do somethings
  return <some data>
}
```

**For Ex:**

```
isCurrentProgramActive({enrollStudent: state}) {
  return state.currentProgram.data.status === 'active';
}
```

### The Container Component Pattern

This pattern states that every module will have one(maybe more)
container component that will hold every other component as its children.

This component will have the following features:

1. Only this component is allowed to have a controller.
2. Only it will connect to the redux store in its `$onInit` and
unsubscribe from it in its `$onDestroy`
3. Only this component will have the `mapStateToThis` function to attach
keys from store to the `this` of the its controller, so that they are
available in the template.
4. All the methods related to the UI rendering and managing will reside
inside its controller for ex: a method for some complicated `ng-if`.
5. The **name with which it will be registered** on the module will
be same as that of the module.

### Making the data and actions available to child components

Please read
*[The Container Component Pattern](#the-container-component-pattern)*
before reading this section.

All the child components are wrapped inside the **container component**
and have isolate scope, this makes them impossible to access data
members and methods from the parent(container) components to render
their view.

##### Accessing Data Members

To access data members, the parent component passes the them to the child
components through their [bindings](#https://docs.angularjs.org/guide/component#component-based-application-architecture).

##### Accessing Method Members

To Access method members, the child component's component definition
object defines the value for the `require` keyword and thus requires
the controller of the container component as a value of the `parent`
property on the its controller.

```
require: {
  parent: "^<name of the container component>"
}
```

```
require: {
  parent: "^enrollmentList"
}
```
<br>
This maintains the isolated scope of the child component, by convention,
and also saves us from dirty style of passing functions from parent
component to child component using `&` and also from the dirtier style
of calling the  passed function in the child component's template using
`({name: 'superman'})`.


### Leveraging Directives to manage UI

*(Under experimentation)*

This is a pattern that takes help of directives rather than AngularJS
components and makes UI management easy.

**For Ex:**
You have a table and and depending on some condition of the data in it
you want to highlight some rows. There are two possible solution:

1. Use `ng-class`.
2. Make a directive that access the scope of the table in its link
function and take a decision ti highlight it or not.

**Another Ex:**
You have a list and want to let the user traverse it using `up` and
`down` arrow keys, you can simply make a directive that adds `keypress`
event listener on the list's parent element and do the traversing in the
callback.

#### Writing Styles

We use `scss` to style our applications.

While writing styles, make sure you follow the following guidelines:

1. For every template, a class should be given to the parent element.
And in the stylesheet corresponding to the template every styles should
be nested inside the same class.<br>
This helps im modularizing the css and avoids overwrites when all the
css files are concatenated in the build step.
2. **For making buttons**: We have only two types of buttons everywhere in
our app (We try to maintain it but, at times it we have to go out of
bounds). To keep our code DRY there are mixins for these buttons in the
`baseStyle.scss` of the `shared` directory, namely:
  1. `border-inverted`: This has white background and colored text and
  inverts the colors on hover, i.e. background takes the color of the
  text and text becomes white.
  2. `solid-inverted`: This has colored background and white text and
  inverts color on hover, i.e. background becomes white and the text
  takes the color of the background.
3. You can find more color and font style variables in the
same file and I encourage you to use them as much as possible instead
of introducing your own colors or styles.
4. If in case you have you have your own mixins or variables,
make sure you put them in the same file or else the build step will
throw an error of style not found.


### Wrapping up a module

<!-- To registration the module on AngularJS follow the following steps:  -->

<!-- 1. Make an index.js file in the top level of the module directory. -->
<!-- 2. Import ngRedux and angular. -->
<!-- 3. Make an   -->

Now when you are done developing your module, it time to register it as
an actual AngularJS module.

Registering of the module and all it components, services and factories
happens inside `index.js` file residing inside the top level of the
module directory.

```
moduleDirectrory:
    - index.js
    - moduleActions.js
    etc.
```

The pattern we follow to register the module is
to make a `const` variable and store the reference of the module we get
after registering it as the angular module with all its dependencies and
all its components, services and factories, and then export it so that we
will be able to import it and inject it as a dependency in our main app.
<br>**Note that this a `default` export**.

In the same file we also `export` the `rootReducer` made by combining
all the reducers from the `reducers.js` file from the module directory.
<br>**Note that this is a `non-default` export**.

One thing to remember here is that the name with which we export the
module and the name with which we export our rootReducer has some
similarity:

* The module name is of the form: `ModuleName`
* The rootReducer name of the form: `moduleName`


### Handling Mixpanel tracking calls

To send events to [Mixpanel](#https://mixpanel.com) we make a separate
`AnalyticsEpic.js` file at the top level of the module and listen for
**redux-actions** and based on
that make calls to the function `sendToMixpanel` defined in the
`analytics.js` in the `app/student/common` directory.

This has the following added benefits:

1. It prevents our template's HTML elements from being cluttered by
`track-clicks` attribute, like we use to do earlier.
2. It also prevents the methods of the controller being cluttered from
`sendToMixpanel` calls.
3. It also makes easy for the developer to prepare any kind of payload
for sending with the event, since these epics have access to the store.
4. It make the code more modular since we have a separate file whose sole
purpose in life is to send events to mixpanel and thus making it more
of a plug and play thing.


### Handling internal tracking

There are a lot of times where mixpanel tracking is not sufficient and
we have to use our internal tracking by calling some APIs.

We chose the vanilla `XMLHttpRequest` class to make the AJAX calls for
this purpose for the following reasons:

1. This separates it from the other AJAX calls being made in the app
and thus giving us the freedom to make any customisation like calling
an entirely diff domain or adding and removing some headers
2. Moreover we don't care about the response at all making it
unnecessary to use the heavy lifting done by the AngularJS's `$http`
provider.

Further these calls are also made by the epics in the
`AnalyticsEpics.js` file.


# Directory Structure

The app contains 4 separate apps, namely admin, student, support, instructor.

Each app contains multiple directories.

Each one of those directories represent on module.
A module has the following structure:

```
enrollmentList/

  components/
    enrollmentListContainer/
      enrollmentListContainer.js
      enrollmentListContainer.html
      enrollmentListContainer.scss

  services/
    enrollmentListApi.js
    enrollmentListMiner.js
    
  enrollmentListConstants.js
  enrollmentListActions.js
  enrollmentListReducers.js
  enrollmentListEpics.js
  enrollmentListFactory.js
  enrollmentListMiner.js
```

NOTE:

1. The components directory is a collection of all the components for this
module.
2. The services directory is a collection of all classes registered as
services on the module.
3. Each file/directory must start with the name of the module.
4. We make separate scss file for each component.
5. All redux and observable related things go into the module root
directory.


## Tools Used

The following tools are used to make the life of our developers simpler
:sunglasses:

1. **redux-dev tools Chrome Extension**: To make debugging redux simpler.
2. **Raven**: We use our own version of Raven to send errors over email.
3. **raven-redux**: To send redux store related data as meta data in error
mail.
4. **npm**: As our single package manager.
5. **gulp**: To minify and put templates in Angular's `$templateCache`.
6. **Webstorm**: We highly recommend using webstorm as the IDE
for development. You can even find the IDE config file `.idea` in the
repo for having same config across all developers.
7. **jest**: For testing epics, reducers and components.
8. **Webpack**: For minifying and bundling our app.
9. **babel**: For transpiling ES6 code to ES5 for browser who still
don't support it.


# Get in touch? <a name="get-in-touch"></a>

In case of any issue in installing or you find any bug in this
readme or in code contact the author/admin of this repo:

##### Rajat Vijay: [rajat@acadview.com](#mailto:rajat@acadview.com)
