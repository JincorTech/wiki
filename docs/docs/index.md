Jincor Docs
================

[![Build Status](https://travis-ci.com/JincorTech/wiki.svg?token=zhVTspsPSE9j1Tuwzqe2&branch=master)](https://travis-ci.com/JincorTech/wiki)

This repo contains Jincor docs in markdown format.


## Process

Create branch using Git Flow, then write some text and make pull request. Travis will build and deploy site from master branch automatically.


## Development

*Preferably use Yarn package manager*

1. `yarn` - install deps
1. `yarn start` - run site in dev mode on [localhost:3000](http://localhost:3000)
1. `yarn build` - generate static to `_docpress` dir


## Structure

```
README.md - main page
docs/
├── README.md - left-side navigation
├── index.md - main backend page
├── frontend/
├── docs/
│   └── index.md - you are here
├── backend/
│   ├── %modulename%
│   ├── index.md - module page
│   ├── deploy.md
│   └── anotherpage.md
├── blockchain/
└── frontend/
```

## Travis steps

1. `yarn` - install deps
1. `yarn build` - build app
1. `./node_modules/.bin/git-update-ghpages JincorTech/wiki docs -e GITHUB_TOKEN="yourghtoken"` - deploy


## Github token

Go to [github settings](https://github.com/settings/tokens/new) and generate new token with `repo`, `user` and `gist` permissions.

## Dependencies docs

1. [docpress](http://docpress.github.io/)
1. [git-update-ghpages](https://github.com/rstacruz/git-update-ghpages)
