# Jincor Frontend Wallets

[![Build Status](https://travis-ci.com/JincorTech/frontend-wallets.svg?token=zhVTspsPSE9j1Tuwzqe2&branch=develop)](https://travis-ci.com/JincorTech/frontend-wallets)

----------------------------

## Description

This frontend application can help user to solve these tasks:
  * show the user his wallets
  * show wallet transactions
  * deposit funds into the wallet
  * transfer fund to another wallet

## Build & Run
  *You need install nodejs and yarn*

  1. clone the repo and install app dependencies
  1. `cp .env.example .env` - copy environment variables from example
  1. `yarn run start` - start app in dev mode
  1. `yarn run build` - build static
  1. `yarn run lint` - lint code
  1. Another useful commands specified in `package.json`

## Configuration

  Wallet requires just one environment variable:

  API_HOST - path to the wallets api host.

  Make `cp .env.example .env` to copy variables from example. Don't commit `.env` file.

## Structure

  The project's /src/ directory contains these parts:

  * /assets/ - stores static content
  * /components/ - react presentational components without logic
  * /containers/ - react container components that have a connection to the store and can dispatch actions
  * /helpers/ - helpers that can help to solve different kinds of tasks grouped by they purpose
  * /redux/ - reducers and store configuration
  * /sagas/ - redux sagas grouped by section of the store and root saga
  * /utils/ - utilities for different tasks such as creating actions, validators etc.

---------------------------

[Jincor Tech](https://github.com/JincorTech)
