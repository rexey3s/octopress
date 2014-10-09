---
layout: post
title: "How to install SWRL Tab plugin for Protege 5"
date: 2014-10-09 23:45:00 +0700
comments: true
categories: [worklog]
tags: [protege5, owlapi, swrlapi, swrltab, sqwrl, ontology, owl2, query, rule]
---

{:.text-justify}
Protege Team has recently pushed out a new SWRL API (included SWRL API, SQWRL API, Drools Rule Engine and a SWRL Tab Plugin). SWRL Tab Plugin is a powerful tools that can help you manipuladte rule and query OWL by SQWRL. The tool 's come out so many dependencies are missing that you have to build and install from source. Here is the guide.

### Prerequisites

* [Protege 5](http://protege.stanford.edu/products.php#desktop-protege)
* [Java 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
* Maven 

Install maven for Ubuntu

``` sh
$ sudo apt-get install maven
```

### SWRL API, SWRL Drools Engine

1. Build and install SWRL API to local maven repositories

Clone this  repo [SWRL API](https://github.com/protegeproject/swrlapi)

``` sh
$ git clone https://github.com/protegeproject/swrlapi.git
$ cd swrlapi
swrlapi$ mvn clean package # => Build jar 
swrlapi$ mvn install:install-file -Dfile=./target/swrlapi-1.0-SNAPSHOT.jar
    \ -DpomFile=./pom.xml
```

or if you run into a problem of missing dependencies , follow this way

``` sh
$ git clone https://github.com/protegeproject/swrlapi.git
$ cd swrlapi
swrlapi$ mvn dependency:go-offline
swrlapi$ mvn -o clean package # => Build jar 
swrlapi$ mvn install:install-file -Dfile=./target/swrlapi-1.0-SNAPSHOT.jar
    \ -DpomFile=./pom.xml
```

2. Build and install SWRL Drools Engine to local maven repositories

Clone this repo [SWRL Drools Engine](https://github.com/protegeproject/swrlapi-drools-engine)

``` sh
$ git clone https://github.com/protegeproject/swrlapi-drools-engine.git
$ cd swrlapi-drools-engine
swrlapi-drools-engine$ mvn clean package
swrlapi-drools-engine$ mvn install:install-file -Dfile=./target/swrlapi-drools-engine-1.0-SNAPSHOT.jar
    \ -DpomFile=./pom.xml
```

### Build and install SWRL Tab plugin

Check out [this repo](https://github.com/protegeproject/swrltab-plugin)

``` sh 
$ git clone https://github.com/protegeproject/swrltab-plugin.git
$ cd swrltab-plugin
swrltab-plugin$ mvn clean package
```
 
Then copy the ``jar`` file in ``target`` folder to the ``plugin`` folder in Protege_5 folder

```
swrltab-plugin$ cp target/swrltab-plugin-1.0-SNAPSHOT.jar ~/Protege_5.0-beta/plugins
```

Here some images of SWRLTabs working in Protege 5

**SWRLTab** 
![alt text](/images/swrltab.png "SWRLTab")

**SQWRLTab** 
![alt text  ](/images/sqwrltab.png "SQWRLTab")

**Rules View** 
![alt text](/images/normalruleview.png "Rules View")

