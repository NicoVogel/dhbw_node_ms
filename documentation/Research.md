# Research

## MS Security

The API gateway will be secured with [JWT](https://jwt.io/introduction/). The payload of a Token is variable. The following structure would be suitable minimum for the planned structure:

````javascript

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

Communication should be async between MS. In case of REST use HTTP pooling to make it. [1]
HTTP pooling in short: use callback functions. [2]
If there are a lot of data to be send, another implementation for the Node default HTTP client is required. One option would be *[agentkeepalive](https://github.com/node-modules/agentkeepalive)*. [3]

In case of updating caches use Event-Based communication like AQMT. [1]

## Client Security

There are two things which need to be considered when programming the client.

1. use tokens to protect rest calls (STP) [4]
2. make sure no cross site scripting is possible [5]
    1. [general angular security mesurements](https://ordina-jworks.github.io/angular/2018/03/30/angular-security-best-practices.html)
    2. [Angular Security](https://angular.io/guide/security)
    3. [Node.js Security Tips](https://blog.risingstack.com/node-js-security-tips/)

## Sources

- [1] [Communication in a microservice architecture](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/architect-microservice-container-applications/communication-in-microservice-architecture)
- [2] [What is HTTP long pooling](https://www.pubnub.com/blog/2014-12-01-http-long-polling/)
- [3] [Node.js Connection Pooling](http://pmalouin.blogspot.com/2015/04/nodejs-connection-pooling.html)
- [4] [How to Secure Your NodeJS Web Application Using Synchronizer Tokens](https://medium.com/@lanil.marasinghe/how-to-secure-your-nodejs-web-application-using-synchronizer-tokens-959c45200876)
- [5] [5 Practical Scenarios for XSS Attacks](https://pentest-tools.com/blog/xss-attacks-practical-scenarios/)