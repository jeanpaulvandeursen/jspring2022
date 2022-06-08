# NLJUG J-Spring 2022

## Opening & First Keynote
Coen explaining DevSecOps at ABN AMRO, announcing the Open Sourcing of RESC

## Microservices integration patterns with Spring

Joris Kuipers - Trifork.

Working for the NL Lottery and associated gambling sites.

Favoured Gradle over Maven for building because of incremental build support and caching, reducing build time of a very large codebase to 3 minutes.

Functionality for gambling sites includes addiction and fraud prevention, thus emphasizing the need for proper logging and monitoring.

*Communication* between services goes through HTTP, using Apache HTTP Client, which needs to be properly tuned. OOTB defaults are not sensible, so using Spring autoconfig to create a set of sensible defaults:
* nr of connections;
* ignore cookies (machine to machine);
* connection timeout;
* socket timeout;

*Request/Response logging* considerations:
1. requires buffering to avoid loosing the object;
2. secrets and PII need to be obfuscated;
3. on-demand finegrained logging needs to be possible;

1. Use Spring BufferingClientHttpFactory class
2. regex-based logging obfuscator based on Logback
3. Spring sleuth header trace id ('baggage header')

*Observability*
* do structured format logging, for example on JSON, analyze using datadog;
* logback-spring.xml;
* console-json-appender.xml;
* logback.PropertyProvider;
* MDC - Mapped Diagnostic Context:
  * key-value pairs associated with current thread;
  * current user;
  * tenant;
  * request URL;
  * etc.;
* Per environment log levels in Spring config;
* Metrics: Micrometer Spring integration;

## Testcontainers

Oleg Selajev - AtomicJar

* [testcontainers website](https://testcontainers.org);
* Docker;
* [Junit / Spring integration](https://github.com/testcontainers/testcontainers-java);
* port randomization;
* (test) data driven;
* rust / python / go / .Net;
* Restassured;
* Ambiguity lib for asynchronous testing;
* Steps for using testcontainers:
  * add testcontainers dependency to master pom (also checkout modules);
  * add container to test class, for instance GenericContainer;
  * annotate test class with @Testcontainers and test method with @Container;
  * KafkaContainer abstracts away Kafka (extensive) config;
  * Adding only the Spring JDBC testcontainer URL suffices to have the testcontainer database spin up for the test;
  * Method .withCopyFileToContainer() to populate container config, or use (Redgate) Flyway for initial database setup;

Additional tips:
* tcpproxy lib with fixed port can be used to connect to testcontainer using a randomly assigned port, for instance to inspect a database's content;
* testcontainers can be reused, but be careful not to use this in a multi-user (CI) environment;

## Java Tools & Gems

Johan Janssen - ASML

