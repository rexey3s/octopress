---
layout: post
title: "Advanced network security note - 3rd day of class"
description: ""
tags: [lecture, note, network, securtiy, summer,Prof. Peter Reiher]
categories: [network securtiy]
comments: true
share: true
---

### Authentication and Authorization in Network Security

* Authentication is determining who someone is
* Authorization is determining someone is allowed to do something
* Authorization usually depends one authentication, which properly is not sufficient

### Perimeter of Defense and networks: Firewall

#### Perimeter Defense
* The idea is building an impenetrable perimeter around something valueable to protect it
* History of perimeter defense : castle, fortress, The Great Wall of China, etc.
* But they were all failed because of perimeter defense's weaknesses

#### Weaknesses of Perimeter Defense models
* Breaching the perimeter compromises all security
* 2 major assumptions:
  - The barrier is impenetrable (It usually isn't)
  - We can carefully control the entrance and exit points (we often can't)

### What is Firewall ?
* A machine to protect a network from malicious external attacks

#### Some types of Firewall

##### Filtering Gateways (Filtering firewall)
- Based on packet header information, either let packet go through or reject it<br>
- Stateless firewall


{:.table .table-hover}
|    Pros.    |     Cons.                         |
|:------------|:----------------------------------|
|`Fast`       | `Limited capabilities`            |
|`Cheap`      | `Depend on header authentication` |
|`Flexiable`  | `Generally poor logging`          |
|`Transparent`| `May rely on router security`     |

##### Application Level Gateway (proxy firewall/gateway)
  * Firewalls that understand the application-level details of network traffic
  * stateful firewall


{:.table .table-hover}
|    Pros.                 |           Cons.                    |
|:-------------------------|:-----------------------------------|
|`Highly flexiable`        | `Slower`                           |
|`Good Logging`            | `More complex and expensive`       |
|`Content-based filtering` | `Highly dependent on proxy quality`|
|`Potentially transparent `|                                    |



