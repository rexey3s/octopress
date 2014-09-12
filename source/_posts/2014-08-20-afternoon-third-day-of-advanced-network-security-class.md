---
layout: post
title: "Advanced network security note - 3rd day of class - Afternoon"
description: ""
tags: [lecture, note, network, securtiy, summer,Prof. Peter Reiher, 2014]
comments: true
share: true
---
``Today's class was a very interested topic DDos :))``

## Denial of Service Attacks
* The only goal is make the service unavailable to legitimate users

### Attacker Motivation
* Sometimes extortion
* Sometimes political in nature
* Sometimes personal feuds
* Sometimes as distractions (to other kind of attacks)
* Many others

### Ways of DOS attacks
* Can be acheived in a lot of  ways. E.g,
  - shutdown the power source of the target
  - crash your machine
  - crash your router
  - use up a key machine or network resource
* Using up resource is the most common approach
  - network bandwidth
  - processing power
  - RAM
  - Network stack resources
    + E.g., records of open connections (`TCP connections via SYN flood`)
  - OS or application resources
    + E.g., entries in a hash table

### Simple Denial of Service Attacks

* One machine tries to overload another machine
  - E.g., send more packets than the target can handle

* There is a fundamental problem for attacker:
  - *Attacker's machine must be more powerful than the target machine*
  - *Otherwise, the attack machine can't generate enought packets*
* *Sovling*  this problem by 2 possibilities:
  1.*Find a way to make the target pay more per message than the attacker*
  2. *Use more than one machine to attack*

#### 1.Make the target pay more

##### Denial of Service and Asymmetry
* sometimes generating a request is cheaper than formulating a repsonse
* If so, one attack machine can generate a lot of requests and effectively multiply its power
* E.g., send random garbage packets to machine expectig encrypted packets (obviously it have to decrypt those packets, which is an expensive process)
* Not always possible to achieve this asymmetry but often can be done

#### An example is SYN Flood
* TCP is connection-oriented
* Endpoints must keep information about current tcp conn. for detecting loss of packet and doing flow contronl and managing congestion
* Typically kept in a table of **fixed size** - *so attack this table not the bandwidth*

##### The TCP open connection table
* Design to support many TCP connections at a time.E.g., for high volume web server
* One entry per conn.
* reuse an entry once the connection ends
* some legitimate conns. will be slow

##### The basic of attack
* Attacker uses initial req/resp to start tcp sessions
* then he abandons them
* target keeps them open for a while
* Filling up the server's open connection table and prevening new real tcp sessions

##### How to defense

1. Don't let the attacker take too many open connection slots
  * Maybe restrict to 3 or 4 slots per IP addr
  * Doesn't help if attacker has a lot of machines and attacker spoofs IP addr
2. Drops unused conns. more aggressively
  * so half-open conns, don't waste the resource as long
  * bad impact on legitimate clients
3. Save most of your slots for good IP addr, but how about IP Spoofing
4. Make attacker pay more
  * he must pay sth for getting the open conns. table entry
  * if the cost is high enough, he can't afford to fill my table
  * so, what *currency* can we make him pay in ?
  * The solution is using SYN Cookies

* Good aspects of this approach
    - doesn't change tcp protocol
    - doesn't require clients to do anything
    - doesn't require server to save any information
    - can be turned on and off easily






