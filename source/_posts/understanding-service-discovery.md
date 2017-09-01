---
title: Understanding Service Discovery
---

## Why service discovery?

Let's assume we have X number of applications deployed across Y number of hosts which needs to communicate with each other. How do we can ensure that our components can freely communicate using proper hosts and ports?

In the ideally world we would like to be able to answer simple questions:

* How do we know which services are running?
* How we can identify services in network (host, port)?

The basic approach is using static configuration with simple mapping where specific application is deployed. However, in modern cloud based infrastructure (which we see more often these days) can be really painful. We can regenerate our config after each deployment but does not really give us any flexibility we are looking for.

And there comes service discovery tools which can help with this tasks. <mark>There are many types of service discovery  - passive and active, agent and agentless.</mark> Which is the best discovery method? The answer is dependent on your needs.

## Agentless vs Agent service discovery pattern

With agentless approach, there is no agent on discoverable hosts which means there is no need of managing an agent on every discoverable host. This leads to minimal overhead required during the deployment the service and less configuration management. However, there can be a difficulty in recoding an server state without an agent in place.

Opposite to this is agent discovery pattern. On every host you want to be discoverable in your network, there is a need to deploy the agent which will handle registering hosts into catalog called - service registry. From there, you can query service registry to find out which hosts contains which services and connect to them accordingly.

### Active vs Passive service discovery pattern

The difference between these two are in the matter of decision making. Active service discovery pattern moves the decision to the application in terms which backend should be used and in detecting failures. Passive patterns separate decision making from services. Applications cannot decide which backend connect.

## Existing service discovery solutions

### [Apache Zookeeper](https://zookeeper.apache.org/)

*Pros*

* Mature technology
* Feature rich
* Apache Fundation support

*Cons*

* Latency-dependent
* No multi datacenter support
* Client number limit

### [coreOS etcd](https://coreos.com/etcd/)

*Pros*

* Data persistence
* CoreOS out of the box integrration

*Cons*

* Young project.

### [Consul by Hashicorp](https://www.consul.io/)

*Pros*

* Easy to setup
* Hashicorp!
* Multidata center support
* Gossip protocols
* Consensus protocols (Raft)
* DNS or HTTP based service discovery

*Cons*

* Immature. Even younger than etcd.

## Comparison

| | Zookeeper | Consul | Etcd |
| -------- |:-----------:|:----------:|:------------:|
| Service Discovery | HTTP API | HTTP API + DNS | HTTP API |
| Healthchecking | TCP | HTTP API | Up to application |
| Key/Value store | Strong consistency | 3 consistency modes | Strong consistency |
| Multidatacenter support | <span style="color: red">&#x2717;</span> | <span style="color: green">&#x2713;</span> | <span style="color: red">&#x2717;</span> |
| ACL | <span style="color: red">&#x2717;</span> | <span style="color: green">&#x2713;</span> | <span style="color: green">&#x2713;</span> |
| Language | Java | Go | Go |

<p  style="text-align: center; font-size: 0.9em; opacity: 0.5"><br />Tab. 1. Comparison of production ready service discovery solutions</p>

## Other resources

If you want to read more, these are some other great resources in this topic:

* [Understanding Modern Service Discovery with Docker](http://progrium.com/blog/2014/07/29/understanding-modern-service-discovery-with-docker/)
* [Open-Source Service Discover](http://jasonwilder.com/blog/2014/02/04/service-discovery-in-the-cloud/)
* [Service Discovery in a Microservices Architecture](https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/)
* [Active vs. passive discovery in distributed applications](http://containersummit.io/articles/active-vs-passive-discovery)
* [Service Discovery: Zookeeper vs etcd vs Consul](https://technologyconversations.com/2015/09/08/service-discovery-zookeeper-vs-etcd-vs-consul/)
* [etcd vs consul vs ???](https://gist.github.com/kchida/d1c15f3968f4f8272c49)
