---
layout: post
title: Difference between Rails 2.3 and 3
categories:
- Rails 2.3 and 3
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-16 11:33:23'
---
<pre>1. Introduction of bundler (New way to manage your gem dependencies) 
2. Gemfile and Gemfile.lock (Where all your gem dependencies lies, instead of environment.rb) 
3. A new .rb file in config/ folder, named as application.rb (Which has everything that previously environment.rb had) 
4. Change in SQL Structure: Model.where(:activated =&gt; true) 
5. All the mailer script will now be in app/mailers folder, earlier we kept inside app/models. 
6. Rails3-UJS support. for links and forms to work as AJAX, instead of writing complex lines of code, we write :remote =&gt; true 
7. HTML 5 support. 
8. Changes in the model based validation syntax: validates :name, :presence =&gt; true 
9. Ability to install windows/ruby/jruby/development/production specific gems to Gemfile. 
<div class="highlight"><pre><code class="bash">group :production do 
  gem 'will_paginate' 
end</code></pre></div></pre>


<h2 class="gray">Comments</h2>

<div>
<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</div>

<script type="text/javascript">
	var disqus_shortname = 'sukendhar';
	// var disqus_developer = 1;
	var disqus_identifier = 'http://sukendharreddy.com/difference-between-rails-2-3-and-3/';
	var disqus_url = 'http://sukendharreddy.com/difference-between-rails-2-3-and-3/';
	var disqus_script = 'embed.js';
	(function () {
	var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
	dsq.src = 'http://' + disqus_shortname + '.disqus.com/' + disqus_script;
	(document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
	}());
</script>
