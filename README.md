# BFO-Allen-Model
Classes and SWRL rules added to the Basic Formal Ontology to implement the [Allen temporal model](https://en.wikipedia.org/wiki/Allen%27s_interval_algebra). This started because I wanted to create a little tutorial showing users of the Stanford Protege OWL ontology editor how to: create a Custom Tab with the Rules view. In previous tutorials I used the SWRLTab but there are certain cases where the Rules view is better. The most common such case is when you have an ontology such as those in the OBO Foundry (which includes BFO) that use codes rather than intuitive names for IRIs. The SWRLTab only recognizes IRI names so if you try to write rules for OBO ontologies they end up looking like: 

OBO00000123456(?p, ?b) ^ OBO00000345645(?p, ?mr) -> OB123000003492(?p, ?l)

The Rules View recognizes the rdfs:labels rather than the IRI. It also supports completion using control-space as most views in Protege do (but the SWRLTab currently doesn't). To create my example rules I needed an ontology that used codes and the first one I had at hand was BFO. Glancing at BFO, I realized a logical way to extend it was to add some rules so it could implement the full Allen temporal model. See the Wikipedia link above for more on the Allen model but it's the defacto standard people use for temporal reasoning. It supports intuitive relations among temporal intervals such as one interval overlaps, contains, precedes, etc. another interval. I wrote a rule for my tutorial and I realized it wouldn't take much effort to implement the Allen model. Which I've done. I've also included some example intervals (e.g., WWII) from military history and the relevant first and last instances. I apologize for the military domain, I enjoy reading military history when I'm not reading about computer science and when I had to think of events that overlapped, contained, etc. the first thing that came to mind were battles in the US Civil War and WWII. This ontology is an extension of BFO that supports the full Allen model. Specifically, what I've added are:

1) Object properties with doman and range of Temporal Interval for the Allen model relations such as contains, overlaps, etc. For the full list see the Wikipedia link above.

2) A data property called dateTime with domain Temporal Instant and range xsd:dateTime. Each BFO temporal interval has properties 'has first instant' and 'has last instant'. These properties are used by the rules to determine which relations hold between which intervals.

3) A rule that determines if a Temporal Interval precedes another interval by comparing their dateTime values.

4) All the rules needed to compute the Allen relations. Of course the reasoner does much of the work for you in both 3 and 4 so only a few rules are required. Inverse and transitive properties and the reasoner take care of the rest. 
