---
layout: post
title: "Reproducibility in Bioinformatics"
date: 2050-02-01
categories: opinion bioinformatics
---

The other day I had a thought, which has prompted this post. The thought came to me
when I was trying to create the perfect, most reproducible, script. It was a simple
analysis, but I wanted to ensure that if anyone ever needed to run it, or if anyone
wanted to reproduce my results, that they could simply fire up my code in the right
environment, and boom! They would have the Exact. Same. Results. But then I realized
that there was an issue that makes reproducibility in bioinformatics fundamentally
different than in other science. Or at least it seemingly does.

To illustrate my point, consider the following example. Imagine you have an
experiment that you want to run in the lab. You ask a volunteer in the lab to 
pipette an amount of fluid, and then proceed to use this concoction to generate a
conclusion, which you then send off for publication. Things seem great, until
someone tries to reproduce your results, and they fail to. Uh-oh!

But here is the tricky part. Imagine that the issue is in fact the brand of pipette.
You used brand A, and the person trying to reproduce your results used another
brand, and this was enough to change results. I think that most people would end up
at the conclusion that the experiment was not particularly robust, and for good
reason. 
