Jincor
===================

![](https://habrastorage.org/webt/59/d5/42/59d542206afbe280817420.png)
## What's Jincor?
Jincor is a wholesome, secure, compliant and breezy to use platform, that will allow any business to work with smart contracts and cryptocurrency payments easily with no legal, technical or operational complications and in a cost-efficient manner.
It will let companies use all the benefits of blockchain-based technologies without having to develop and implement them on their own. With Jincor, managers and employees will be able to execute cryptocurrency transactions in a fully transparent way and meeting all the compliance requirements, as well as to carry out any corporate relations by creating smart contracts, which will be written to a private blockchain based on Hyperledger technologies.
Overall, our goal is to build a private blockchain and the platform that will make it possible even for smart enough (tech-savvy, heavy iPad user) 5-year-old kid to register in Jincor ecosystem, initiate the smart contract and pay to a supplier. And that's all in a very user-friendly, compliant and legal way. In our opinion, this will lead to a complete changeover in the corporate interactions model, which will eliminate injustice, flaws on business commitments human mistakes factor and make businesses (including small) from all around the world much closer to blockchain technologies and vice versa.

Technically, Jincor is a set of microservices, blockchain solutions(transaction storage and smart-contracts) and frontend applications unite in one system.

Jincor team is also maintains some open-source libraries

## APIs
* [Company](https://jincortech.github.io/backend-company/index.html)
* [Auth](https://jincortech.github.io/backend-auth/index.html)
* [Verify](https://jincortech.github.io/backend-verify/index.html)

## Services
* [Company](https://github.com/JincorTech/backend-company) - service which handles all the logic associated with companies and employees(employee is a build break for each company)
* [Admin](https://github.com/JincorTech/backend-admin) - admin panel to rule them all(currently only companies and employees)
* [Auth](https://github.com/JincorTech/backend-auth) - services for JWT issuing and verification. We use auth to authorize both: users and services
* [Verify](https://github.com/JincorTech/backend-verify) - service which verifies user's contacts(email, phone number, 2 factor)
* [Messenger](https://github.com/JincorTech/backend-synapse) - matrix based messenger written on Python(MUST be replaced as soon as possible by the own solution)
* [ICO Dashboard](https://github.com/JincorTech/backend-ico-dashboard) - dashboard for an ICO campaign.

## Frontend apps
* [Companies](https://github.com/JincorTech/frontend-company) - frontend app for companies and searching
* [Messenger](https://github.com/JincorTech/frontend-messenger) - frontend app for messaging
* [Landing](https://github.com/JincorTech/frontend-laughing-robot) - Brand new landing page with SSR
* [ICO Dashboard](https://github.com/JincorTech/frontend-supreme-happiness) - ICO dashboard application built on top of [Frontend Boilerplate](https://github.com/JincorTech/frontend-static-boilerplate)
* [-Landing-](https://github.com/JincorTech/frontend-landing) - landing page of the product
* [-ICO Landing-](https://github.com/JincorTech/frontend-landing-ico) - landing page for ICO campaign



## Blockchain
* [ICO](https://github.com/JincorTech/ico) - JCR token, pre ICO, ICO
* [HL Sanbox](https://github.com/JincorTech/hyperledger-fabric-sandbox) - Hyperledger Fabric Sandbox. Here we are playing with custom blockchain

## Libraries

### Backend
* [PHP Auth Client](https://github.com/JincorTech/auth-php-client) - client to communicate with [Auth](https://github.com/JincorTech/backend-auth) service from the PHP
* [Laravel Auth Client](https://github.com/JincorTech/laravel-auth-client) - client to communicate with [Auth](https://github.com/JincorTech/backend-auth) service from Laravel Framework. Built on top of [PHP Auth Client](https://github.com/JincorTech/auth-php-client)

### Frontend
* [Frontend Boilerplate](https://github.com/JincorTech/frontend-static-boilerplate) - the boilerplate we use to build our frontend applications


## Structure overview
[![Structure overview](https://habrastorage.org/web/6ec/09c/e8f/6ec09ce8fde849dc8339f0cd5a27121d.png)](https://habrastorage.org/web/6ec/09c/e8f/6ec09ce8fde849dc8339f0cd5a27121d.png)
