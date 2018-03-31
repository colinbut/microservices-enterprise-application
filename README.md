# Microservices Enterprise Application


### Keynote

This is a fictional enterprise application that is built using a Microservices architecture.

Rather than having a big monolithic application (in the case of a traditional legacy enterprise application - as demonstrated here.), 
here we showcase the whole application being broken down into several distinct 'micro' services. 

See table below for list of microservices.




| Microservice                      | GitHub Repository                                             | Language  |
| :-------------------------------- | :------------------------------------------------------------ |-----------|
| User Service                      | https://github.com/colinbut/user-service.git                  | Java      |
| Registration Service              | https://github.com/colinbut/registration-service.git          | Java      |
| Exclusion Service                 | https://github.com/colinbut/exclusion-service.git             | Java      |
| Subscription Service              | https://github.com/colinbut/subscription-service.git          | Ruby      |
| Email Service                     | https://github.com/colinbut/email-service.git                 | Golang    |
| Registration Email Service        | https://github.com/colinbut/registration-email-service.git    | Python    |
| Account Service                   | TBC                                                           | Java      |
| Marketing Service                 | TBC                                                           | TBC       |
| Notification Service              | https://github.com/colinbut/notification-service.git          | Java      |
| Audit Service                     | https://github.com/colinbut/audit-service.git                 | Java      |
| Reporting Service                 | TBC                                                           | TBC       |



This microservice project demonstrates a Polygot nature (different microservices implemented using different programming languages) to develop microservices which is quite common. In real life, in a corporate company, you 
might have different teams being responsible for different microservices with each of these teams free to choose whatever tech stack they wish or is comfortable using.

#### Breaking a monolith

It is well publicised that the best way to develop microservices architecture is to start with a Monolith and break it down. Some people even try to 
do it from scratch at the start. 

Here, in my own personal project, i have built from scratch for the purpose of just a demo project.

#### Communication

Two styles:

1. Synchronus HTTP REST [API calls]
2. Asynchronous Messaging (JMS and AMQP)

#### Orchestration vs Choreography

This demo project showcases both styles in Orchestration and Choreography as outlined in above Communication section where we 
utilise 2 styles of communication.

In terms of Service Orchestration - See Registration Service. This service demonstrates orchestration where the Registration Service
does some orchestration in order to implement its Business Workflow. E.g. It first calls out to UserService to check whether
an already existing user with supplied registration details already exists before checking whether the supplied details are blacklisted or not.
Finally, successful registration by creating the user (again, making another synchronous HTTP REST API call out to User Service).
In addition, sends an message to Subscription Service for that to process the subscription email for the registration.

For Choreography, take a look at the following services:

- registration-email-service
- notification-service
- subscription-service
- email-service

Each of these services reacts to messages sent to either the RabbitMQ exchange (AMQP) or ActiveMQ queue (JMS).
 
This whole demo project uses a combination of these both techniques for the microservices's app's IPC (Inter Process Communication).
 

#### Environment Setup

[TBD]

#### Development Strategy

[TBD]

#### Testing Strategy

[TBD]

#### Deployment Strategy

The ideal strategy in terms of deployment (onto a production environment) would be to have in place
a mechanism to make use of Containers and Orchestration 

1. Dockerized Apps (Containers)
2. Kubernetes Cluster (Orchestration)

in local we can also run each microservice individually or attempt to mimic the 'production' setup by running the Docker 
containers since most (all?) of the microservices are Dockerized.

This project repo is a demo project hence doesn't go that far in showcasing the use of running and scaling the dockerized
microservices apps within Kubernetes. However, you can try. 

Also, you can try to deploy to the Cloud and make it Cloud-Native in order to take advantage of IAAS meaning you don't need to 
manage a cluster of Kubernetes pods/Docker containers manually. As it requires a lot of Ops work.  

You can try on the various cloud providers like AWS, GCP, Microsoft Azure, Red Hat OpenShift.
 
Alternative, you can try to deploy these microservices on the PAAS such as Heroku, CloudFoundry etc.

I didn't put much effort into the deployment side of things as i wanted to focus this demo project on the "App" side of things
in order to demonstrate how a Microservice architecture application looks like.

#### Caveats

[TBD]

#### Roadmap

Adopt another style of communitcation - Event-Driven Architecture (EDA) style with the use of Event Sourcing and CQRS techniques:

1. Event driven (publish and subscribing (Pub/Sub) to events)
2. Use an Event Store for transportation and querying of events (Apache Kafka)
3. CQRS - breaking query and command into completely separate workflows
