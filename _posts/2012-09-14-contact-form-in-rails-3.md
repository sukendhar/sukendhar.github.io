---
layout: post
title: Contact form in Rails 3
categories:
- Ruby on Rails
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-16 11:57:39'
---
The goal of this tutorial is to build a form that when submitted will validate and email the data.
<div><strong>Prerequisites</strong></div>
To simplify this, I’m just using Google Apps to manage email addresses. If you have your own email server just modify the settings as needed. To get started you’ll need:
<ol>
	<li>A Google Apps account, of course</li>
	<li>Ruby on Rails 3.2.2 (give or take a few version numbers)</li>
</ol>
<div><strong>Configuring Rails for GMail</strong></div>
In an existing or new application, open <code>config/application.rb</code>. Insert the following snippet in the <code>Application</code> class.
<pre><code>config.action_mailer.smtp_settings = {
  :address              =&gt; "smtp.gmail.com",
  :port                 =&gt; 587,
  :domain               =&gt; "yourdomain.dev",
  :user_name            =&gt; "from@yourdomain.dev",
  :password             =&gt; "Super-Secure-Password",
  :authentication       =&gt; :plain,
  :enable_starttls_auto =&gt; true
}

config.action_mailer.default_url_options = {
  :host =&gt; "yourdomain.dev"
}
</code></pre>
Set the value of <code>:domain</code> to the domain you’re using for Google Apps, and <code>:user_name</code> and <code>:password</code> to your Google Apps account credentials. In the second block replace <code>:host</code> with the domain where the application is reachable from. The <code>:host</code> option is used to ensure that all links in email templates generate full URLs.
<div><strong>The Message Model</strong></div>
To allow validation of the message, I create a model and just include <code>ActiveModel</code>’s validations. Allowing the model to be written just like any other Rails model.

Create the file <code>app/models/message.rb</code>, or with a name of your choice. Make the file look similar to the following.
<pre><code>class Message

  include ActiveModel::Validations
  include ActiveModel::Conversion
  extend ActiveModel::Naming

  attr_accessor :name, :email, :subject, :body

  validates :name, :email, :subject, :body, :presence =&gt; true
  validates :email, :format =&gt; { :with =&gt; %r{.+@.+\..+} }, :allow_blank =&gt; true

  def initialize(attributes = {})
    attributes.each do |name, value|
      send("#{name}=", value)
    end
  end

  def persisted?
    false
  end

end</code></pre>
This is fairly self explanatory. A message can have a subject and body, as well as the name and email address of the sender. All of the fields are required, and the email address is verified with a regular expression.
<div><strong>The Mailer Model and Views</strong></div>
Run <code>rails g mailer NotificationsMailer</code>. This generates <code>app/mailers/notifications_mailer.rb</code>.

We'll want <code>notifications_mailer.rb</code> to look similar to this snippet. Check out the <code>ActionMailer</code> API for specifics on what’s happening here.
<pre><code>class NotificationsMailer &lt; ActionMailer::Base

  default :from =&gt; "noreply@youdomain.dev"
  default :to =&gt; "you@youremail.dev"

  def new_message(message)
    @message = message
    mail(:subject =&gt; "[YourWebsite.tld] #{message.subject}")
  end

end</code></pre>
Replace <code>:to</code>, <code>:from</code> and <code>:subject</code> with the address you’d like the email sent to, the address it’s being sent from (should be the one you configured the Rails application with), and the subject of the email.

Create the file <code>app/views/notifications_mailer/new_message.text.erb</code>.How the message looks is entirely up to you. Here’s an example of how it could be laid out.
<pre><code>Name: &lt;%= @message.name %&gt;

Email: &lt;%= @message.email %&gt;

Subject: &lt;%= @message.subject %&gt;

Body: &lt;%= @message.body %&gt;</code></pre><br />
<div><strong>The Controller and View</strong></div>
Run <code>rails g controller contact</code> and then open <code>app/controllers/contact_controller.rb</code>.

The controller will only need two actions: <code>new</code> and <code>create</code>.
<pre><code>class ContactController &lt; ApplicationController

  def new
    @message = Message.new
  end

  def create
    @message = Message.new(params[:message])

    if @message.valid?
      NotificationsMailer.new_message(@message).deliver
      redirect_to(root_path, :notice =&gt; "Message was successfully sent.")
    else
      flash.now.alert = "Please fill all fields."
      render :new
    end
  end

end</code></pre>
To get these actions working, open up <code>config/routes.rb</code> and insert the following two lines.
<pre><code>match 'contact' =&gt; 'contact#new', :as =&gt; 'contact', :via =&gt; :get
match 'contact' =&gt; 'contact#create', :as =&gt; 'contact', :via =&gt; :post</code></pre>
When a <code>GET</code> request is made to <code>/contact</code>, the <code>new</code> action is called. When a <code>POST</code> request is made to <code>/contact</code>, the <code>create</code> action is called.

Create <code>app/views/contact/new.html.erb</code>. As with the email template, this template is entirely up to you, I'm only providing an example of what it could look like.
<pre><code>&lt;%= form_for @message, :url =&gt; contact_path do |form| %&gt;
  &lt;fieldset&gt;
    &lt;div&gt;
      &lt;%= form.label :name %&gt;
      &lt;%= form.text_field :name %&gt;
    &lt;/div&gt;

    &lt;div&gt;
      &lt;%= form.label :email %&gt;
      &lt;%= form.text_field :email %&gt;
    &lt;/div&gt;
    &lt;div&gt;
      &lt;%= form.label :subject %&gt;
      &lt;%= form.text_field :subject %&gt;
    &lt;/div&gt;

    &lt;div&gt;
      &lt;%= form.label :body %&gt;
      &lt;%= form.text_area :body %&gt;
    &lt;/div&gt;
  &lt;/fieldset&gt;

  &lt;fieldset&gt;
    &lt;%= form.submit "Send" %&gt;
  &lt;/fieldset&gt;
&lt;% end %&gt;</code></pre>
<div><strong>Try it</strong></div>
Start your <code>rails server</code> and go to <code>/contact</code>. Fill out the form and hit send. If everything was done correctly an email should arrive in the inbox of the address specified.


<h2 class="gray">Comments</h2>

<div>
<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</div>

<script type="text/javascript">
  var disqus_shortname = 'sukendhar';
  // var disqus_developer = 1;
  var disqus_identifier = 'http://sukendharreddy.com/contact-form-in-rails-3/';
  var disqus_url = 'http://sukendharreddy.com/contact-form-in-rails-3/';
  var disqus_script = 'embed.js';
  (function () {
  var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
  dsq.src = 'http://' + disqus_shortname + '.disqus.com/' + disqus_script;
  (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
  }());
</script>

