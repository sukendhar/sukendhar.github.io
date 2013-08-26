---
layout: post
title: Mongo connection failure?
categories:
- Mongo DB
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-16 12:10:11'
---

Connection failed during mongo start:

Follow this steps:

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>rake rails:upgrade:backup
</code></pre>
</div>

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>mongod --repair
</code></pre>
</div>

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>sudo start mongodb
</code></pre>
</div>

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>sudo status mongodb
</code></pre>
</div>

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>mongo
</code></pre>
</div>


connection established message will be displayed.

<h2 class="gray">Comments</h2>

<div>
<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</div>

<script type="text/javascript">
	var disqus_shortname = 'sukendhar';
	// var disqus_developer = 1;
	var disqus_identifier = 'http://sukendharreddy.com/mongo-connection-failure/';
	var disqus_url = 'http://sukendharreddy.com/mongo-connection-failure/';
	var disqus_script = 'embed.js';
	(function () {
	var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
	dsq.src = 'http://' + disqus_shortname + '.disqus.com/' + disqus_script;
	(document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
	}());
</script>
