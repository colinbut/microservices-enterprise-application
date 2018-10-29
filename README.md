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
| Account Service                   | https://github.com/colinbut/account-service.git               | Java      |
| Marketing Service                 | TBC                                                           | TBC       |
| Notification Service              | https://github.com/colinbut/notification-service.git          | Java      |
| Audit Service                     | https://github.com/colinbut/audit-service.git                 | Java      |
| Reporting Service                 | https://github.com/colinbut/reporting-service.git             | Java      |



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

An example of a deployment structure (based on Docker/Kubernetes) can be found at [Microservices Enterprise Application Deployments](https://github.com/colinbut/microservices-enterprise-application-deployments)

Also, you can try to deploy to the Cloud and make it Cloud-Native in order to take advantage of IAAS meaning you don't necessary have to
manage a cluster of Kubernetes pods/Docker containers on bare-metal physical servers as this process requires a lot of Ops work. This approach
encourages pure vendor lock-in.

For example, if deploying on AWS and using AWS's full native integrated features you can run the microservices either on (legacy?) EC2 instances which are managed VMs on the cloud.
Or, you can use Elastic Container Service (ECS) to run the microservices in AWS's native containerized solution.

For the optimisitic tech player, one could try and run a Kubernetes cluster inside ECS or EC2 instances. Note that this is probably for the more advanced players.

In terms of Cloud vendors, various cloud providers like AWS, GCP, Microsoft Azure, Digital Ocean, Red Hat OpenShift is worth a look
 
Alternative, you can try to deploy these microservices on the PAAS such as Heroku, CloudFoundry etc.


#### Caveats

[TBD]

#### Roadmap

Adopt another style of communitcation - Event-Driven Architecture (EDA) style with the use of Event Sourcing and CQRS techniques:

1. Event driven (publish and subscribing (Pub/Sub) to events)
2. Use an Event Store for transportation and querying of events (Apache Kafka)
3. CQRS - breaking query and command into completely separate workflows
