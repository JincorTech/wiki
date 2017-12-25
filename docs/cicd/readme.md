CI/CD
======

Introduction
-------------

In this document we will describe only *CI/CD* for the beta stage.
The main approach is containerization of services with using of Docker.
[Docker Swarm](https://docs.docker.com/engine/swarm) is used for container
orchestration, load balancing, scaling, networking, and etc., i.e. for
our base infrastructure.


Access
-------

To easy access to docker swarm, [portainer](https://portainer.io) is used.
Note. In swarm mode you should think/work with service instead of a single container.
Portainer only available on the manager nodes (currently it's only [213.219.38.178:45372](http://213.219.38.178:45372)).


Structure
----------

Currently we have only 2 nodes: manager `213.219.38.178` (swarmnode01) and worker `139.162.198.67` (swarmnode02).
Nodes have private and shared network (overlay) between nodes.

* Manager services:
  - _portainer_           portainer/portainer:latest
  - _stage_nginx-proxy_   nginx:1.13.7-alpine               - listen 80 port and forward to services
  - _stage_companies_     jincort/backend-fpm-company:stage
  - _stage_wallets_       jincort/backend-wallets:stage
  - _stage_redis_         jincort/backend-redis:latest      - currently need only for job queue

* Worker services:
  - _stage_frontend-wallets_     jincort/frontend-wallets:stage
  - _stage_frontend-messenger_   jincort/frontend-messenger:stage
  - _stage_frontend-company_     jincort/frontend-company:stage
  - _stage_frontend-contracts_   jincort/frontend-contracts:stage
  - _stage_wallets_sender_       jincort/backend-wallets-test-sender:stage - service for sending initial test coins
  - _stage_auth_                 jincort/backend-auth:stage
  - _stage_verify_               jincort/backend-verify:stage
  - _stage_nginx-proxy_          nginx:1.13.7-alpine        - listen 80 port and forward to services

Both nodes listen `80` port and proxy to the internal services.
`Portainer` public port `45372`.

**Note**. Every container should minimize
of persistence to a local storage (local files, sqlite and etc.).
This guarantee running a container on any node without problems.
If container must use local persistence you should pin
to concrete node (use deployment constraints).

For default REST HTTP services nginx proxy is used to proxy request to the related
services (use internal virtual domain names (in swarm existing a service discovery to automate dns)).
It's good for security reason when hidding working services by frontend nginx (proxy).
But this is question to the architecture of the projects.


CI/CD as Sequence diagram
--------------------------

Whole process from the height of bird fly.

![CICD Sequence diagram](./cicd.png)

For more details see below sections.


Continuous Integration
-----------------------

This task is executed with usage of any external service (like *Codeship* or *Travis*,
maybe use own infrastructure based on [drone.io](https://drone.io) in future).
For details see these documentation on the official sites.

Basic configuration for service in the *CI* system should be configured like:

1. Any operations to deploy test environment.
Maybe its install and run `redis`, with `mongo` and fill-up by fixtures, for an example.
1. Run any tests to ensure all properly works.
1. Last step is for continious delivery.
The image must be `push` to the docker hub with `stage` tag. For an example for travis
it will be:

```
- export TAG=`([ "$TRAVIS_BRANCH" == "master" ] && echo production) ||
    ([ "$TRAVIS_BRANCH" == "develop" ] && echo stage) || echo dev-$(git rev-parse --short HEAD)`
- export DOCKERFILE=`[ -f Dockerfile.$TAG ] && echo Dockerfile.$TAG || echo Dockerfile`
- docker build -f $DOCKERFILE --no-cache -t jincort/your-service:${TAG} .
- docker login -u $DOCKER_USER -p $DOCKER_PASS
- docker push jincort/your-service:${TAG}
```

where `TAG` is set by current branch by mapping: `master -> production`, `develop -> stage`, and `other as dev-xxxxxx`).
`DOCKERFILE` is set by tag and using the special docker file (with `$TAG` extension) if it's existing, or else use default `Dockerfile`.

`doker login` is necessary when image repository is private in the docker hub.


Continuous Delivery
--------------------

After docker accepting an image the webhook is posted to the URL:
`http://username:password@213.219.38.178:58732/autodock/v1/`.
The special service on the manager swarm node (currently only `213.219.38.178`)
is listening webhooks. The service has a configuration file (where described
allowed repositories and related shell commands to run when hook is coming up).
After matching repository the service run a shell command like:
`docker service update --image ...`, and sending output of the command to
the slack `#stagestatus` channel.

**Note.** If any errors was occurred you should resolve it by manual way (use portainer, ssh and etc.).

**Note.** Maybe use more powerful [service](https://github.com/adnanh/webhook) in future,
currently used [tools-docker-webhooks](https://github.com/JincorTech/tools-docker-webhooks).


Howto
------

### Need to add new service to the stage?

1. Configure your *CI* commands with executing of: `docker push ...:stage`
1. The service image must be already in the docker hub with `stage` tag for the next steps.
1. Set-up necessary configurations in the portainer (networks, configs, secrets, volumes).
1. Configure `nginx proxy` (if you need a public access by domain for service by `80` port).
1. Start a service with using of portainer.
1. Check the service is working properly.
1. On the manager node update a file with your new image repository:
`/usr/local/etc/tools-docker-webhooks/config.json`
```
    ...
    "jincort/...": [
        "bash",
            "/home/maintainer/jincor/devops/dockerhub-webhooks/trigger.sh",
            "update",
            "${repository.repo_name}",
            "${push_data.tag}",
            "${push_data.pusher}"
    ],
    ...
```
1. Go to the docker hub of your repository to the webhooks tab.
Add hook like: `http://username:password@213.219.38.178:58732/autodock/v1/`.
**Note.** Username and password should have correct values!
1. Test your *CI/CD* by pull requesting to the develop branch.
Slack will post a notification message about result of update image on the swarm
stage if *CI* passed successfully.


Improvements
------------

The stage environment should be close as possible to the production version.
All configs must be similary as in the production.
Production DB-s (parts or whole tables) should be cloned (periodically) to the stage DB-s.
Based on [classic](http://nvie.com/posts/a-successful-git-branching-model/) gitflow,
the single branch *stage* should be used instead of set of *release* branches, and
*CI* should be configured to use that branch instead of *develop*.
