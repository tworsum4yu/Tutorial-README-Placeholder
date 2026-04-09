# Cypress Introduction

***FYI:*** *Everything is the doc will be a basic cover for some of the stuff I used whilst using cypress, so it won't give the full image of what cypress can do. Please find below a link to the docs if you are interested on more information.*

***Cypress docs:*** *https://docs.cypress.io/app/get-started/why-cypress*

---

## What is Cypress?

Cypress is a testing tool that allows you to write code that simulates how a user interacts with your application. You define a series of actions and Cypress executes them automatically. These interactions are then used to verify that the application behaves as expected.

For example; in a quiz application, you could write a test where Cypress selects an incorrect answer. The test would then check that the application correctly identifies the answer as wrong and responds appropriately, such as displaying an error message or indicating the correct answer.

***Important Note:*** *Whilst writing your tests, you need to remember that cypress is meant to do the checks for you. Don't be like me and just write the interaction code and use your eyes to verify that everything is acting as you expect.*

---

## Getting Started

Getting ready with cypress is real simple. All you got to do is install the npm dependencies for your project.

> npm install cypress --save-dev

Above is the command you can use to install the cypress dependency. <br>

Following, you will need to run the so that you can get the files you need to start working with cypress.

> npx cypress open

Runs cypress and opens up an application window that looks like below.

![Cypress App Window](./assets/Cypress1.png) <br>

From here, you will need to click on E2E testing. This will generate the folder structure that cypress will read your tests from. The file structure will look something like below.

> cypress
> > e2e
> > fixtures
> > support

The e2e directory is where cypress will read your tests from, so that is the directory you need to store all your tests. If it doesn't create this on startup, you can just add it. <br>



