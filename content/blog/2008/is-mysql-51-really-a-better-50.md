---
title: Is MySQL 5.1 really a better 5.0?
date: "2008-12-11"
url: /blog/2008/12/11/is-mysql-51-really-a-better-50/
categories:
  - Commentary
  - Databases
---
With all the furor over MySQL 5.1 GA, its release schedule, its quality, etc etc I think a fundamental claim is being left un-examined. Lots of people are saying that if you leave out the new features in 5.1 and look only at the features that existed in 5.0, it's better quality.

The implication is that the process of building 5.1 looked like this: rip out nasty code and fix it all up, so there's a brand new architecture free of code debt. Adjust existing features to use this new, high-quality, sensible server architecture. Add new features.

Is this accurate?

Time will tell, and I have not yet seen enough of 5.1 in real-world production environments. As Peter says, [it's not how many bugs there are---it's how many bugs affect you](http://www.mysqlperformanceblog.com/2008/12/10/mysql-51-went-to-ga-was-it-a-good-move/). In my line of work, we see bugs that only show up if you're, for example, running a server with hundreds of thousands of tables. Or similar edge cases. I see a lot of routine things, too, but my point is that I am somewhat reserving my opinion about 5.1's quality of existing features. As an example of what I mean, there were some bugs with 5.1 not using indexes correctly---a serious regression from 5.0. These have been fixed. Will there be others that haven't been found yet? Probably.

Here is my gut feeling about a few existing features: triggers were always a hack and remain a hack. The memory allocation algorithms of the query cache are suboptimal, and that hasn't changed fundamentally. Geospatial functions are largely unusable, and that hasn't improved. The [silly behavior of correlated subqueries](http://bugs.mysql.com/bug.php?id=32665) has probably been MySQL's number one slap-me-in-the-forehead misfeature since it was introduced in 4.x, and that isn't fixed (it will be in 6.0, but that's a whole other topic). Failsafe replication is code rot that was partially implemented and then abandoned in 4.x, causes bugs, and they haven't even removed the code ([read the bug report!](http://bugs.mysql.com/bug.php?id=11923)). UNION still uses a temporary table, whether it's required or not. LOAD DATA FROM MASTER never worked to begin with, and it's still there---it causes problems and should be ripped out. The Federated engine is probably best left alone. [Group commit is *still* broken for InnoDB](http://bugs.mysql.com/bug.php?id=13669) when binary logging and XA transactions are enabled. (This was broken during 5.0's release, is a serious regression since 4.1, and is definitely a server architecture problem. So much for the beautiful new server architecture in 5.1?)

Don't get me wrong. I'm not trying to bash 5.1's quality. I'm just taking issue with this unchallenged assertion that everything that wasn't introduced in 5.1 is rock solid, performs better, and works beautifully now. I don't know for sure; I suspect it is partially true and partially false, but time will tell.

I will say this: I'm generally happier with the quality and stability of 5.0 in the last little while, say since 5.0.6x. If you don't need 5.1's new features, why break something that works?


