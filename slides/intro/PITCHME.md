# Filip Hric

- QA Lead & Slido test automation maker, Cypress ambassador
- filip (at) slido.com
- [@filip_hric](https://twitter.com/filip_hric)

+++

## What we are going to cover 1/3

- example TodoMVC
  * web app, data store, REST calls
- basic page load test
- selector playground
- resetting state
- XHR spying and stubbing, fixtures

+++

## What we are going to cover 2/3

- CI and Cypress dashboard
- test reporters
- configuration and environment variables
- retry-ability
- debugging
- visual testing

+++
## What we are going to cover 3/3

As long as ⏳ permits

- page objects vs app actions
- fixtures and backend
- preprocessors
- component testing
- plugins
- code coverage

+++

Please: if you have experience with Cypress.io, help others during the workshop 🙏

+++

## Requirements

You will need:

- `git` to clone this repo
- Node v6+ to install dependencies

```text
git clone https://github.com/filiphric/cypress-workshop.git
cd cypress-workshop
npm install
```

+++

## Repo organization

- `/todomvc` is a web application we are going to test
- all tests are in `cypress/integration` folder
  - there are subfolders for exercises
    - `01-basic`
    - `02-adding-items`
    - `03-selector-playground`
    - `04-reset-state`
    - etc
- keep application `todomvc` running!

Note:
We are going to keep the app running, while switching from spec to spec for each part.

+++

## `todomvc`

Let us look at the application.

- `cd todomvc`
- `npm start`
- `open localhost:3000`

**important** keep application running through the entire workshop!

+++

It is a regular TodoMVC application.

![TodoMVC](/slides/intro/img/todomvc.png)

+++

Look at XHR when using the app

![Network](/slides/intro/img/network.png)

+++

## Questions

- what happens when you add a new Todo item?
- how does it get to the server?
- where does the server save it?
- what happens on start up?

Note:
The students should open DevTools and look at XHR requests that go between the web application and the server. Also the students should find `todomvc/data.json` file with saved items.