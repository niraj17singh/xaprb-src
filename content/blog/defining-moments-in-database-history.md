---
title: Defining Moments in Database History
date: '2017-03-19T20:59:17+00:00'
author: Baron Schwartz
categories:
- Databases
description: ''
image: ''
draft: true

---
I've been privileged to be intimately involved with one defining set of technology shifts in the mid-2000s, which ultimately created both a new industry-defining set of technologies and the impetus for the emergence of a contender. I'm referring to the rise of the LAMP stack. I've been reflecting recently on what perhaps were key factors in that phenomenon and what's happened since then, indeed, what's happening now.

First, what was it about the LAMP stack, anyway? All of the ingredients in that stack were interesting and signaled tectonic shifts (or were the result of them), but I'm particularly interested in MySQL, the database that came to power much of the Internet as we know it today. MySQL was remarkable for many reasons, although it's easy to forget them in hindsight. It wasn't the first or perhaps even the best open source database, but it was [just enough better](/blog/just-enough-better) that it became the best for the situation at hand. And ultimately it became a commercial success that even in hindsight seems improbable.

I've thought of many necessary conditions for MySQL to flourish in 2000-2010. The big question is which combination of those conditions were sufficient. I am not certain of the answer, but I'm certain the answer is plural.

And yet, partially because of its enormous popularity, MySQL helped spur the rise of NoSQL in 2008-2009. These databases sought to define a new moment in database history: one in which legacy relational technology was finally replaced by an utterly new generation. If you were around at the time, you might remember how vehemently people decried relational, joins, SQL, ACID, etc. It was not sufficient to lambaste a technology or implementation: you needed to have some highly-fermented bile against the concepts and foundations themselves or you weren't really a NoSQL believer.

Where do we find ourselves today? Relational implementations rapidly improved (enter NewSQL), and NoSQL was backronymed to mean "not only SQL" instead of being a rejection of SQL. Many NoSQL databases today sport SQL-like languages. The obvious question has to be addressed: was it just a flare-up? Is there any need for next-generation data storage and processing? Or is good old relational going to improve and obviate every next-gen data technology anyway?

I believe strongly that the answer is no. I see a few current trends and I'm sure that at least some of them will eventually become something enduring in some form.

### Next-Generation Databases

Relational, and SQL, are painful. SQL is a [Yoda language](/blog/2013/02/01/if-yoda-you-were-sql-you-would-invent/) that causes a lot of problems. It obscures intent, introduces illogical logic such as tri-valued truth, prompts huge books from Celko and Date about the small subset of how to do it right, and creates endless opportunities for the server to do things you didn't intend and cause performance disasters.

Not least, SQL is an open sore in a program. Think about it: you've got this nice strictly-typed language with all sorts of compiler guarantees, and in the middle of it is a meaningless string blob that isn't compiled, syntax-checked, or type-checked. It is bound to a foreign source of data through an API that isn't knowable to the program or compiler, and may change without warning. It's the programming equivalent of "I give up, random potentially correct garbage of dubious meaning goes here." It's the equivalent of an ugly CDATA in an XML document.

This should present _significant_ opportunities for improvement. One can imagine a number of sensible first steps to take: find a way for the program and the database to use the same language and toolset; design a database query language that works similarly to a programming language; memory-map the database into the program; and so on. Problems begin immediately, and indeed the relational model was created to solve many of those issues---issues that have been happily and naively reinvented ever since. Those who are ignorant of history are doomed to repeat it.

But into this fray waded a brave new generation in 2009, with map-reduce databases, key-value databases, Javascript databases, and so forth. All with some good ideas, all going in some productive direction, all with at least some aspects that could be legitimately criticized.

A while ago I [predicted](/blog/2013/01/10/bold-predictions-on-which-nosql-databases-will-survive/) that MongoDB, Redis, and Riak would survive in a meaningful way. Of these, Riak seems to have been sidelined, but MongoDB and Redis are going strong.

Which other NoSQL databases have had impact on par with those two? Perhaps Cassandra, and arguably Neo4J, but both of those are less mainstream. MongoDB and Redis are ubiquitous.

Why? It's instructive to look at the problems they solve. Redis starts with a simple conceptual foundation: label a piece of data, then you can use the label to fetch and manipulate the data. The data can be richly structured in ways that are familiar to programmers, and the operations you can perform on these structures are a Swiss Army knife of building blocks for applications. The types of things that otherwise force you to write boilerplate code or build frameworks.