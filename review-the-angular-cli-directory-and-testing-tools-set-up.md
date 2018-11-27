# 3. Review the Angular CLI directory and testing tools set up

By default the Angular CLI will configure both unit tests and e2e tests in your new Angular CLI application.

The default tools that most teams use for testing Angular are the same ones set up by the Angular CLI

#### The Jasmine test framework <a id="thejasminetestframework"></a>

Provides everything needed to write basic tests. It ships with a HTML test runner that executes tests in the browser.

#### Angular testing utilities <a id="angulartestingutilities"></a>

The Angular testing utilities create a test environment for the Angular application code under test. Use them to condition and control parts of the application as they interact within the Angular environment.

#### Karma <a id="karma"></a>

The karma test runner is ideal for writing and running unit tests while developing the application. It can be an integral part of the project's development and continuous integration processes. This guide describes how to setup and run tests with karma.

#### Protractor <a id="protractor"></a>

Use protractor to write and run end-to-end \(e2e\) tests. End-to-end tests explore the application as users experience it. In e2e testing, one process runs the real application and a second process runs protractor tests that simulate user behavior and assert that the application responds in the browser as expected.

The [angular.io](https://angular.io/docs/ts/latest/guide/testing.html) official testing docs are 99 pages long which hopefully gives you an idea of how big a topic frontend testing is with Angular and how the platform is truly designed to be tested from the ground up.

![](https://firebootcamp.ghost.io/content/images/2017/01/testing-directory-structure-1.png)

**Figure: Angular CLI Folder Structure**

1. e2e - The folder with all the e2e tests
2. app folder - Any files in this folder with a suffix of .spec.ts will be picked up and run by the test runner \(Karma or WallabyJS\)
3. test.ts - Specific testing config for Angular
4. karma.conf.js - Testing config for the Karma test runner
5. protractor.conf.js - Testing config file for Protractor to run e2e tests

