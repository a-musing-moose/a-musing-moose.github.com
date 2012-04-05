---
layout: post
title: Looping over really big database tables
---

I deals with large (not Big with a capital B but still pretty large) amounts of
data quite often.  We have recently been trying to optimise what would appear to
be a fairly simple problem - iterating over the entire contents of a table.

Initially this seems quite easy. We could do a simple:

    SELECT * FROM My_Table;
    
Obviously this only works for very small tables as you would be loading the
while shebang into memory. Next you might try:

    SELECT * FROM My_Table
    ORDER BY <primary_key>
    LIMIT <offset>,<batch_size>;
    
This gives you the ability to pull back the data in managable chunks. Sadly this
still only works for fairly small tables.  In my case the table is an
itermediate between our regular database and
[Solr](http://http://lucene.apache.org/solr/) which we use for searching. So as
we iterator over the database, those chunks of data are transformed into xml and
then pushed into solr. The table is relatively wide and contains about 15
million rows.

We have a little python app that runs a number of threads and does this in
parallel. It works out the number row (a simple COUNT(*)) and then runs 4
threads, each doing chunks of 1000 at a time until it hits the row count. This
was on the VM hosting solr and the database taking a matter of days. Not good.

After talking to a colleague it turns out that adding order by really kills
performance when combined with an OFFSET/LIMIT. Seems that for every request the
DBMS sorts the whole table, seeks to the OFFSET and then yanks the LIMIT number
of rows. Not good.

Even by making this optimisations we were still seeing some odd behaviour.
Namely that as we increased the OFFSET the queries were taking longer and longer
to complete. Also not good.

Finally after doing some digging and researching I came up with a formula that
actually worked. The final SQL statemet we came up with is:

    SELECT * FROM `SearchAll`
    WHERE ProductId > <primary_key>
    ORDER BY ProductId ASC 
    LIMIT <batch_size>;
    
This has been going for ~4 hours and is just shy of 11 million. Is Good!
