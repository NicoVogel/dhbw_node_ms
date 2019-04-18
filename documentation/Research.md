# Research

## MS Security

The API gateway will be secured with [JWT](https://jwt.io/introduction/). The payload of a Token is variable. The following structure would be suitable minimum for the planned structure:

````js

{
    userid: "<an user uuid>",
    permission: {
        groups: [
            "<group A>"
        ],
        roles: [
            "<role A>"
        ],
        specific: [
            {
                resource: "<specific name for a resource which is used as an ID>",
                type: "<ALL, POST, GET, PUT, DELETE>"
            }
        ]
    }
}

````

## MS communication

A good start point to learn the communication between microservices is [Communication in a microservice architecture](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/architect-microservice-container-applications/communication-in-microservice-architecture). This article provides a general overview which possibilities there are and starting to show which should be used.

**TL;DR**: There are two communication types.

1. Synchronous calls between microservices, use REST (or equivalent like GraphQL) in combination with [HTTP long pooling](https://www.pubnub.com/blog/2014-12-01-http-long-polling/).

2. Asynchronous calls between microservices, use Events. Events use the publish and subscribe pattern [[1]](#sources) and a common protocol which provides this for multiple clients is AQMT (or equivalent) [[2]](#sources).

Depending on the task you want to achieve you use a different approach which builds on top of publisher-subscriber pattern. The simple concept is explained [here (Event-driven architecture)](https://microservices.io/patterns/data/event-driven-architecture.html) and a more advanced approach is [Sage](https://microservices.io/patterns/data/saga.html).

Sage is used if you want to update multiple databases in a row and want the possibility of rolling back.

Communication should be async between MS. In case of REST use HTTP pooling to make it. [1]
HTTP pooling in short: use callback functions. [2]
If there are a lot of data to be send, another implementation for the Node default HTTP client is required. One option would be *[agentkeepalive](https://github.com/node-modules/agentkeepalive)*. [3]

## Client Security

There are two things which need to be considered when programming the client.

2. make sure no cross site scripting is possible [4]
    1. [general angular security mesurements](https://ordina-jworks.github.io/angular/2018/03/30/angular-security-best-practices.html)
    2. [Angular Security](https://angular.io/guide/security)
    3. [Node.js Security Tips](https://blog.risingstack.com/node-js-security-tips/)

## Sources

- [1] [publisher-subscriber explained and compared with Observer](https://hackernoon.com/observer-vs-pub-sub-pattern-50d3b27f838c)
- [2] [Choosing Your Messaging Protocol: AMQP, MQTT, or STOMP](https://blogs.vmware.com/vfabric/2013/02/choosing-your-messaging-protocol-amqp-mqtt-or-stomp.html)

- [3] [Node.js Connection Pooling](http://pmalouin.blogspot.com/2015/04/nodejs-connection-pooling.html)
- [4] [5 Practical Scenarios for XSS Attacks](https://pentest-tools.com/blog/xss-attacks-practical-scenarios/)