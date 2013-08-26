---
layout: post
title: Mongo DB installation
categories:
- Mongo DB
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-16 12:05:28'
---

The following command to install the latest stable version of MongoDB:

{% highlight bash %}
$ sudo apt-get install mongodb-10gen
{% endhighlight %}

When this command completes, you have successfully installed MongoDB! Continue for configuration and start-up suggestions.

<span style= "text-decoration: none; border-bottom:1px dashed;">**Starting MongoDB**</span>
----------

Upstart users can start the <tt>mongod</tt> process by issuing the following command:

{% highlight bash %}
$ sudo service mongodb start
{% endhighlight %}   

All other users can issue the following command to start <tt>mongod</tt>:

{% highlight bash %}
$ sudo /etc/init.d/mongodb start
{% endhighlight %}
	

You can verify that <tt>mongod</tt> has started successfully by checking the contents of the log file at <tt>/var/log/mongodb/mongodb.log</tt>

<span style= "text-decoration: none; border-bottom:1px dashed;"><strong>Stopping MongoDB</strong></span>
----------

Upstart users can stop the <tt>mongod</tt> process by issuing the following command:

{% highlight bash %}
$ sudo service mongodb stop
{% endhighlight %}
	

All other users can issue the following command to stop <tt>mongod</tt>:

{% highlight bash %}
$ sudo /etc/init.d/mongodb stop
{% endhighlight %}
	

<span style= "text-decoration: none; border-bottom:1px dashed;"><strong>Restarting MongoDB</strong></span>
----------

Upstart users can restart the <tt>mongod</tt> process by issuing the following command:

{% highlight bash %}
$ sudo service mongodb restart
{% endhighlight %}
	

All other users can issue the following command to restart <tt>mongod</tt>:

{% highlight bash %}
$ sudo /etc/init.d/mongodb restart
{% endhighlight %}	
	

type "mongo" in your terminal to see the version



<h2 class="gray">Comments</h2>

<div>
<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</div>

<script type="text/javascript">
  var disqus_shortname = 'sukendhar';
  // var disqus_developer = 1;
  var disqus_identifier = 'http://sukendharreddy.com/mongo-db-installation/';
  var disqus_url = 'http://sukendharreddy.com/mongo-db-installation/';
  var disqus_script = 'embed.js';
  (function () {
  var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
  dsq.src = 'http://' + disqus_shortname + '.disqus.com/' + disqus_script;
  (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
  }());
</script>

  