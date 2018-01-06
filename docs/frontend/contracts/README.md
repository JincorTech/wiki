## Jincor Frontend Contracts

[![Build Status](https://travis-ci.com/JincorTech/frontend-contracts.svg?token=zhVTspsPSE9j1Tuwzqe2&branch=develop)](https://travis-ci.com/JincorTech/frontend-contracts)

----------------------------

## Description

This frontend application can help user to solve these tasks:
  * For company administrators:
    * Watch contracts list and sign statuses for each company contract
    * Watch details for each of constacts
    * Create new smart contract with wizard
    * Sign a contract from another company

  * For employees:
    * Watch contracts list and sign statuses for each of contracts from companies
    * Watch details for each of constacts
    * Sign a contract from company

## Build & Run

  1. Install [Git](http://git-scm.com/) and [Node](http://nodejs.org/).

  2. Open your terminal and clone `JincorTech/frontend-contracts` by running:
    ```
    $ git clone git@github.com:JincorTech/frontend-contracts.git
    ```

  3. Now go to the project's folder:
    ```
    $ cd frontend-contracts
    ```

  4. Install dependencies:
    ```
    $ npm install
    ```
  
  5. Start in development mode:
    ```
    $ npm start
    ```

  To build the project in production mode:
    ```
    $ npm run build
    ```

## Configuration

  To connect to the real host you need to pass further NodeJS environment variables:

  COMPANIES_API_PATH - path to the companies api host with api prefix.
  For example: 'https://companies-api.jincor.com/api/v1'

  WALLETS_API_PATH - path to the wallets api host with api prefix.
  For example: 'https://wallets-api.jincor.com/api/v1'

## Use api mocks

  The project's root directory contains apiMock.ts file. In this file you can find api mocks for autonomous run.
  Unfortunately there is no convenient way to use mocks for now. However you can just export fake get, put and post methods from the /src/utils/api/index.ts file instead of real methods.

## Tools & libraries

  The project have these libraries as the base:

  1. [React](https://github.com/facebook/react/)
  2. [Redux](https://github.com/reactjs/redux)
  3. [React-redux](https://github.com/reactjs/react-redux)
  4. [Redux-saga](https://github.com/redux-saga/redux-saga)
  5. [react-css-modules](https://github.com/gajus/react-css-modules)
  6. [seamless-immutable](https://github.com/rtfeldman/seamless-immutable)
  7. [i18next](https://github.com/i18next/i18next)
  8. [TypeScript](https://github.com/Microsoft/TypeScript)

## Structure

  The project's /src/ directory contains these parts:

  * /assets/ - stores static content
  * /components/ - react presentational components without logic
  * /containers/ - react container components that have a connection to the store and can dispatch actions
  * /helpers/ - helpers that can help to solve different kinds of tasks grouped by they purpose
  * /i18n/ - set up i18n configuration
  * /locales/ - static files with translations grouped by locales and sections of the application
  * /redux/ - reducers and store configuration
  * /sagas/ - redux sagas grouped by section of the store and root saga
  * /utils/ - utilities for different tasks such as creating actions, validators etc.

## Refactoring

  * For now some of the project containers contains presentational logic such as templates construction. These parts could be refactored to replace presentaional logic to the separate components.
  * It's would be good to change a custom solution in the containers/employmentAgreement/CreateContractForm to the redux-form.


---------------------------

[Jincor Tech](https://github.com/JincorTech)
