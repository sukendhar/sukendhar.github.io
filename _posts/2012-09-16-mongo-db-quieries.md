---
layout: post
title: Mongo DB Quieries
categories:
- Mongo DB
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-16 12:14:24'
---

<div><strong>Here is the some important frequently used mongodb queries.</strong></div>

<div>After running mongodb server(mongod) and  interactive shell(mongo),  Our’s first command should be</div>
<div>1. help</div>
<div>-&gt;Which will show a lot  of useful command that is helpful at any instance working with mongodb.</div>

<div>2.db.help();</div>
<div>-&gt;It is database level help command that will show some of data level command.</div>

<div>3. db.help;</div>
<div>-&gt; This command will show database level methods.</div>
<div>All above command is basic mongodb command.</div>

<div><strong>How to create database?</strong>
<strong>show dbs; to show all the databases...</strong>
<strong>show collections; to view all the table in db...</strong></div>
<div></div>
<div>1. use databasename;</div>
<div>In my case it is “use mongotest”,  here USE  is command to create database and  mongotest is database name. It is one of the nice feature of mongodb if there will be no database with this particular name, will create new database else use(move) to exiting database.</div>
<div><strong> Create table!!!!!!!</strong></div>


<div>1. db.tablename.save({“name”:”ankit”,”phone”:”1234567890″});</div>
<div><strong>Fetch data from tables!!!!!!!!!!</strong></div>
<div>1. db.tablename.find();</div>
<div>return data of table.</div>
<div>2.db.tablename.find;</div>
<div>return methods it self.</div>
<div><strong>Create another record!!!!!!!!!</strong></div>
<div>x={“name”:”abhay”,”phone”:”1234567890″}</div>
<div>db.contacts.save(x);</div>
<div>this is another way of creating new record and saving as an object.</div>
<div><strong>Fetch particular record from tables !!!!!!!!!!</strong></div>
<div>db.contacts.find({“name”:”ankit”});</div>
<div>N.T. -&gt; Search option is case sensetive.</div>
<div>find record using id</div>
<pre>&gt; db.contacts.find({_id:ObjectId("4ea3aa28eaaf3871b0549dfa")});
{ "_id" : ObjectId("4ea3aa28eaaf3871b0549dfa"),
 "name" : "ankit", "phone" : "1234567890" }</pre>
<div><strong>Update particular record into tables !!!!!!!!!!</strong></div>
<div>-&gt; there is two way to update table</div>
<div>1. Using save()-&gt;this is one of nice feature to mongodb, if there will already row in table it will update with new attribute else will create new record.</div>
<div>2. Using update()-&gt;will only update exiting record.</div>
<div>find record using object</div>
<pre>&gt; x = db.contacts.findOne({"name":"ankit"});
{
        "_id" : ObjectId("4ea3aa28eaaf3871b0549dfa"),
        "name" : "ankit",
        "phone" : "1234567890"
}
Now we have object x with reference of contacts table.
&gt; x
{
        "_id" : ObjectId("4ea3aa28eaaf3871b0549dfa"),
        "name" : "ankit",
        "phone" : "1234567890"
}</pre>
<div>Now i am going to add new attribute email</div>
<pre>&gt; x.email = "ankit@gmail.com"
ankit@gmail.com
Let's see updated row 
&gt; x
{
        "_id" : ObjectId("4ea3aa28eaaf3871b0549dfa"),
        "name" : "ankit",
        "phone" : "1234567890",
        "email" : "ankit@gmail.com"
}</pre>
<div>Now we fetch details from table</div>
<pre>&gt; db.contacts.find();
{ "_id" : ObjectId("4ea3aa28eaaf3871b0549dfa"),
 "name" : "ankit", "phone" : "1234567890" }
{ "_id" : ObjectId("4ea3b067eaaf3871b0549dfb"),
 "name" : "abhay", "phone" : "1234567890" }</pre>
<div>table is not updated here, we need to update table.</div>
<pre>&gt; db.contacts.save(x);
Now try again
&gt; db.contacts.find();
{ "_id" : ObjectId("4ea3b067eaaf3871b0549dfb"), 
"name" : "abhay", "phone" : "1234567890" }
{ "_id" : ObjectId("4ea3aa28eaaf3871b0549dfa"),
 "name" : "ankit", "phone" : "1234567890",
 "email" : "ankit@gmail.com" }</pre>
<div><strong>Delete particular record from tables !!!!!!!!!!</strong></div>
<pre>&gt; db.contacts.remove(x);
let's see row is there or not
&gt; db.contacts.find();
{ "_id" : ObjectId("4ea3b067eaaf3871b0549dfb"),
 "name" : "abhay", "phone" : "1234567890" }
</pre><br />
yah, this row is deleted
THAT ALL WAS THE CRUD OPERATION ON MONGODB TABLE.



<h2 class="gray">Comments</h2>

<div>
<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</div>

<script type="text/javascript">
  var disqus_shortname = 'sukendhar';
  // var disqus_developer = 1;
  var disqus_identifier = 'http://sukendharreddy.com/mongo-db-quieries/';
  var disqus_url = 'http://sukendharreddy.com/mongo-db-quieries/';
  var disqus_script = 'embed.js';
  (function () {
  var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
  dsq.src = 'http://' + disqus_shortname + '.disqus.com/' + disqus_script;
  (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
  }());
</script>

