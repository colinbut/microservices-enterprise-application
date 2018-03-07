# Microservices Enterprise Application


### Keynote

This is a fictional enterprise application that is built using a Microservices architecture.

Rather than having a big monolithic application (in the case of a traditional legacy enterprise application - as demonstrated here.), 
here we showcase the whole application being broken down into several distinct 'micro' services. 

See table below for list of microservices.




| Microservice                      | GitHub Repository                                             | Language  |
| --------------------------------- | ------------------------------------------------------------- |-----------|
| User Service                      | https://github.com/colinbut/user-service.git                  | Java      |
| Registration Service              | https://github.com/colinbut/registration-service              | Java      |
| Exclusion Service                 | https://github.com/colinbut/exclusion-service                 | Java      |
| Subscription Service              | https://github.com/colinbut/subscription-service.git          | Ruby      |
| Email Service                     | https://github.com/colinbut/email-service.git                 | Golang    |
| Registration Email Service        | https://github.com/colinbut/registration-email-service        | Python    |
| Marketing Service                 | TBC                                                           | TBC       |
| Notification Service              | TBC                                                           | TBC       |
| Audit Service                     | TBC                                                           | TBC       |
| Reporting Service                 | TBC                                                           | TBC       |


This microservice project demonstrates a Polygot nature (different microservices implemented using different programming languages) to develop microservices which is quite common. In real life, in a corporate company, you 
might have different teams being responsible for different microservices with each of these teams free to choose whatever tech stack they wish or is comfortable using.

#### Breaking a monolith

It is well publicised that the best way to develop microservices architecture is to start with a Monolith and break it down. Some people even try to 
do it from scratch at the start. 

Here, in my own personal project, i have built from scratch for the purpose of just a demo project.

#### Communucation

Two styles:

1. Synchronus HTTP REST [API calls]
2. Asynchronous Messaging (JMS and AMQP)

#### Roadmap

Adopt another style of communitcation - Event-Driven Architecture (EDA) style with the use of Event Sourcing and CQRS techniques:

1. Event driven (publish and subscribing (Pub/Sub) to events)
2. Use an Event Store for transportation and querying of events (Apache Kafka)
3. CQRS - breaking query and command into completely separate workflows