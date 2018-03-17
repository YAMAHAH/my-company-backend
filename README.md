# my-company-backend

This **backend** application is a mono-repo version of the [lab](http://ivans-innovation-lab.github.io/). It exposes an REST API to be consumed by [internal employees or partners](http://idugalic.pro/2017-12-26-API-Strategy/).

At this stage the API gets hardened and because the API is used across organizational boundaries (consumed by partenrs), the API team will learn a new set of lessons including support, documentation, authentication schemes and so on. There is a need for a independend release cycle and deployment pipeline of an API (backend) only.

Repository is structured in two folders:

- my-company-apps (deployable applications)
   - monolith application or
   - microservices applications
- my-company-libs (libraries/components that are used by applications)

Libraries are actually components that are implemented in a separate maven projects and packaged independently into 'jar' archives. This is giving us an opportunity to create a service (REST API applications) for every component independently and apply microservices architecture style.

## Benefits

- Release management is simple (Libraries are always in SNAPSHOT. Every application depends on the latest library/component SNAPSHOT. I should introduce release versions on the level of application/s because this applications are exposing REST API that will be consumed by external partner applications, and you want to communicate changes). Maven repo tools like Nexus are not necessary.
- **Continuous Integration is improved** (The code is integrated and tested more frequently because everything is build and tested on every push to one repository, so we know how change on a library level will affect some of the applications early in the process)
- No need for additional tools (In mult-repo scenario you need to coordinate many repos which is very hard. We tend to use ChatOps platforms like Atomist and Slack to coordinate our work. In mono-repo scenario we can rely on Github only.

## Drawbacks

- **Scaling development is difficult** (Multiple teams on the same code base)
- No separate deployment of applications (All applications are deployed on every change in the git repo at the same time)
- Securing the repo is hard (It is difficult to grant granular access rights to folders/modules/apps)

## Note

You notice that in a multi-repos scenario we are not sure how the change in a library will affect the applications early in the process. This can be improved, but it requires specific integration testing and more infrastructure. This is not the case in mono-repo environment where we can practice Continuous Integration in a better way, which is by my opinion good benefit of a mono-repo environment. 

Organizing multiple teams over a one repo is hard, and this is a big drawback of a mono-repo environment.

For me it was important to realize directions in which my organization can move to be able to produce quality code fast. Will you go to mono-repo or multi-repo really doesn't matter, you should be able to go in both directions. The thing is to make your architecture aware of this, and structure your applications accordingly.


## Running instructions

### Clone it

```bash
$ git clone https://github.com/ivans-innovation-lab-monorepos/my-company-backend.git
```

### Run it

```bash
$ cd my-company-backend
$ mvn clean install
$ mvn spring-boot:run
```
