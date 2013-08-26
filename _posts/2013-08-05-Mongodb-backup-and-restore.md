---
layout: post
title: Mongo backup and restore
categories:
- Mongo DB
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-16 12:10:11'
---


<span style= "text-decoration: none; border-bottom:1px dashed;">**MongoDB backup & Restore**</span>
----------
To take backup of mongodb database

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>monogodb -db database_name > database_name.bson
</code></pre>
</div>

    
To restore backup file to database

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>mongorestore -db database_name folder_name
</code></pre>
</div>


Take backup from heroku MongoHQ using heroku-mongo-sync

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>heroku mongo:pull --app app_name
</code></pre>
</div>

Take backup from heroku MongoHQ from MongoHQ url

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>mongodump -h hatch.mongohq.com:27021 -d database_name -u admin -p sekret -o ~/tmp/mongodump
</code></pre>
</div>

Restore heroku MongoHQ database with backup 

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>mongorestore -h hatch.mongohq.com:27021 -d database_name -u admin -p sekret ~/tmp/mongodump/database_name
</code></pre>
</div>


<h2 class="gray">Comments</h2>

<div>
<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</div>

<script type="text/javascript">
  var disqus_shortname = 'sukendhar';
  // var disqus_developer = 1;
  var disqus_identifier = 'http://sukendharreddy.com/Mongodb-backup-and-restore/';
  var disqus_url = 'http://sukendharreddy.com/Mongodb-backup-and-restore/';
  var disqus_script = 'embed.js';
  (function () {
  var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
  dsq.src = 'http://' + disqus_shortname + '.disqus.com/' + disqus_script;
  (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
  }());
</script>
    