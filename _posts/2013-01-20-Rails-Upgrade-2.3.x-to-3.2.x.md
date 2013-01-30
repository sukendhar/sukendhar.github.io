---
layout: post
title: Rails upgrade 2.3.x to 3.2.x
---

Install Rails Upgrade plugin $ ruby script/plugin install git://github.com/rails/rails_upgrade.git

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>rake rails:upgrade:check
</code></pre>
</div>

This should give you an idea of the manual changes that need to be done, but you'll probably want to upgrade some of those automatically.  The fastest way to do this is to run 'rails .', which will simply generate a new app on top of your existing code.  But this generation also has the effect of replacing some existing files, some of which you might not want to replace.  To back those up, first run:
 
<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>rake rails:upgrade:backup
</code></pre>
</div>
    
That will backup files you've probably edited that will be replaced in the upgrade; if you finish the upgrade and find that you don't need the old copies, just delete them.  Otherwise, copy their contents back into the new files or run one of the following upgraders...
 
<h2>Routes upgrader</h2>
 
To generate a new routes file from your existing routes file, simply run the following Rake task:
 
<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>rake rails:upgrade:routes
</code></pre>
</div>
    
This will output a new routes file that you can copy and paste or pipe into a new, Rails 3 compatible config/routes.rb.
 
<h2>Gemfile generator</h2> 
 
Creating a new Gemfile is as simple as running:
 
<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>rake rails:upgrade:gems
</code></pre>
</div>
    
This task will extract your config.gem calls and generate code you can put into a bundler compatible Gemfile.
 
<h2>Configuration generator</h2>

<div class="highlight"><pre><code class="bash"><span class="nv">$ </span>rake rails:upgrade:configuration</code></pre>
</div>
 
Much of the configuration information that lived in environment.rb now belongs in a new file named config/application.rb; use the following task to generate code you can put into config/application.rb from your existing config/environment.rb