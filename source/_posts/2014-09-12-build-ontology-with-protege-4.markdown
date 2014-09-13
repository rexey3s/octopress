---
layout: post
title: "Build ontology OWL2 with Protege"
description: "This is a part of my research about automatic reasoning at uit.edu.vn"
tags: [researching, ontology, owl2, protege4]
categories: [Semantic Web, Ontology]
comments: true
share: true
---
The purpose that I decided to write this article are reviewing all the stuffs about ontology in my research progress, sharing knowledge about semantic web technology and finding some new ideas for my thesis at university.
In this first article, I will make a brief tutorial how to build an ontology by using Protege and OWL2 - a web ontology language.
<h2> What is an ontology ? Is it a puzzle word ? </h2>
* In short, an ontology represent the knowledge within a domain. But I prefer calling it's `knowledge of knowledge`. **E.g.**, an ontology which represent a Transportation domain, properly has classes such as Vehicle, Vessel, Train, Aircraft, etc. and all individuals 
which belong to these classes.
<br>
   _I know it may be confused if it is the first time you have heard about it.
But I hope ontology will be more comprehensive as far as you go through this article_

 * **OWL Ontology**
    
    - OWL **Ontology** is a set of axioms, which assert explicitly 3 types of things  **classes**, **individuals** and **properties**. Using **reasoner**we can infer other implicit facts which are hidden in the ontology. 
    - **E.g.**, Individual ``FerrariF430`` belongs to class ``Car``, and the class ``Car`` is a subclass of ``Vehicle``, a reasoner will infer that ``FerrariF430`` is also a ``Vehicle``.
    - Moreover, there are 2 types of properties in OWL ontologies:
        + Data Properties: we can call they are properties of an individual itself, it links individual to a piece of typed data. **E.g.**, ``xsd:dateTime, xsd:String``
        + Object Properties: represent the relationship among individuals or the individuals itself (``reflective`` Object Property)
   
