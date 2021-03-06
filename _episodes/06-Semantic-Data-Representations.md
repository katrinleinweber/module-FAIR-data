---
title: "Lesson 5: Semantic Data Representations"
teaching: Self Paced
exercises: 0
questions:
- "How do I represent my data as linked data?"
objectives:
- "To get an introduction to semantic representations of data and what resources are available to assist"
keypoints:
- How to develop a semantic data representation for your data.
---

### Introduction

We provided a very brief overview of some of the concepts involved in the semantic web and linked data in [Episode 01:  Web of Data](https://github.com/ReproNim/module-FAIR-data/blob/gh-pages/_episodes/01-Web-of-Data.md).  Please review this module if you need an introduction to concepts such as persistent identifiers, URI's, RDF and triples.

Here we will focus specifically on a set of technologies collectively called the [semantic web](http://www.linkeddatatools.com/semantic-web-basics).  The concept of the [semantic web](https://en.wikipedia.org/wiki/Semantic_Web) was introduced by Tim Berners Lee to describe a web of data accessibly by machines through the web. The semantic web is often called web 3.0, "a way of linking data between systems or entities that allows for rich, self-describing interrelations of data available across the globe on the web" [Linked Data Tools](http://www.linkeddatatools.com/semantic-web-basics).

What does that mean exactly?  A more detailed and technical explanation is provided through the lessions below.  But in plain terms, the semantic web provides a protocol for publishing data on the web that allows machines to access them based on a set of relationships.  If fully realized, it allows bits of information about the same entity contained in different different databases, developed and maintained by different people, to be easily and automatically assembled without having to go through any manual mapping.

The basis of this ability is the encoding of data as a graph where each data point is connected to other data points through specific relationships. This graph structure contrasts with the usual tabular form that we use to store our data, e.g., in a relational database or spreadsheet.  Consider the following table for an fMRI study:

| Subject   | Task   | Brain region |
|----------|--------|--------------|
| Male023  | SBLS   |  Hip         |

This table indicates that a subject was given a task, in this case the Salthouse and Babcock Listening Span task (SBLS), and showed activation in the hippocampus (Hip).  To interpret this data, a human would need a key to the abbreviations, but would easily be able to supply the relationships among the different data points.  But while a computer can easily read across the row to know that SBLS and Hip go with Male023, the nature of the relationship among the variables is not machine readable.

Let's say that there are two different databases in two different locations.  One, as in the table above, has brain activation as a function of region and task. The second has measured gene expression in different parts of the human brain.

| Region   | Gene   | Expression level |
|----------|--------|--------------|
| hippocampus  | GRM1   |  High         |

A reasonable question might be:  What brain regions are active in memory tasks that also express glutamate receptors?

In order to answer this question, we would go to database 1 and ask for the set of brain regions that are activated by memory tasks.  We may need to go to another source and find a list of tasks that measure memory, because database 1 only lists the name of the test.  We would then go to database 2 and run that list of brain regions to return a list of genes that are expressed in those regions.  Finally, we would match those genes against a list of glutamate receptors.

Those of you who are familiar with working across multiple databases (see episode XXXXX) probably know the problems likely to be encountered. Even assuming that the two databases used the same terminology for brain regions (are Hip and hippocampus the same?), the query is very time consuming to do.  Note that the human has to do the integration here-there is no way to type a query into your web browser that would do the integration for you.

In the world of the semantic web (which, in truth, some say is mythical), this query could be done by typing one or two (albeit very complicated) queries into your web browser, using a query language called [SPARQL](https://en.wikipedia.org/wiki/SPARQL). How is that possible?

If both databases had used semantic web technologies to design their database, they would have included critical pieces of information that relate different aspects of the data in a way that a computer can "understand".  So in database 1, they may have statements such as:
  -  "hippocampus" "is part of" "brain",
  -  "hippocampus" "is activated by" "Salthouse and Babcock Listening Span task",
  -  "Salthouse and Babcock Listening Span task" "measures" "working memory";
  -  "Working memory" "is a type of" "memory"

Each of these statements is called a triple because it includes a subject, object and predicate. These concepts and relationships also each have their own URI (Uniform resource identifier) as a unique and persistent identifier (see [Episode 01:  Web of Data](https://github.com/ReproNim/module-FAIR-data/blob/gh-pages/_episodes/01-Web-of-Data.md)). So additional relationships can be added to each node, growing the graph from these basic triples. So you could ask for any brain region that is activated by tasks that measure memory.

Similarly, database 2 might have encoded statements like:
  -  "hippocampus" "is part of" "brain",
  -  "hippocampus" "expresses" "GRM1",
  -  "GRM1" "is a" "gene"
  -  "GRM1" "encodes" "glutamate receptor".

 In this data structure, it would be straightforward to compose a query to return any brain part that expresses a gene that encodes a glutamate receptor.  Again, each of these concepts and relationships have their own URI (Uniform resource identifier) as a unique and persistent identifier.

Now imagine the case where both databases are building their databases from the same ontology, that is, a set of terms and the relationships among them, e.g., a set of brain regions, genes and tasks and a set of relations that connect them. Both databases therefore use the same URI's to identify elements in their databases.  The use of the same set of URI's, even in separate databases, allows someone to "mash up" the results between the two databases, by connecting results through a set of common URI's. So one would be able to compose a query across the two databases for the set of brain regions that both express glutamate receptors and are activated by working memory tasks, without the need for human intervention.  Because "hippocampus" has the same URI in both databases, there is no ambiguity in joining results from one database to another.

> ## Selected External Material
> An excellent set of tutorials is available on the semantic web and associated technologies through [Linkeddatatools.com](http://www.linkeddatatools.com/index.php) and so we won't replicate them here. The tutorials cover:
>
> 1. [Introduction To Graph Databases](http://www.linkeddatatools.com/introducing-rdf) - gives a brief overview of the way in which the semantic web stores data.
> 2. [RDF - A Quick Start](http://www.linkeddatatools.com/introducing-rdf-part-2) - an introductory look at Resource Description Framework (RDF), the format the semantic web uses to store data in graph databases.
> 3. [Semantic Modeling](http://www.linkeddatatools.com/semantic-modeling) - introduces the key aspects of describing data with meaning, or semantics - and the advantages this can offer.
> 4. [Introduction To RDFS & OWL](http://www.linkeddatatools.com/introducing-rdfs-owl) - the key syntax the semantic web uses to encode semantic meaning into data.
> 5. [Querying Semantic Data](http://www.linkeddatatools.com/querying-semantic-data) - how to query published semantic data using SPARQL protocol - the means to harness the immense discovery capabilities of the semantic web.
>
{: .callout}

#### References
> Additional materials:
>
>   - [Linked Data Guides and Tutorials](http://linkeddata.org/guides-and-tutorials)
>   - [Linked Data: Tim Berners-Lee, 2006](https://www.w3.org/DesignIssues/LinkedData.html)
>   - [W3C RDF Primer](https://www.w3.org/TR/rdf11-concepts/)
>
> Relevant Books:
>
>   - [Tom Heath and Christian Bizer (2011) Linked Data: Evolving the Web into a Global Data Space (1st edition). Synthesis Lectures on the Semantic Web: Theory and Technology, 1:1, 1-136. Morgan & Claypool.](http://linkeddatabook.com/editions/1.0/)
{: .callout}
