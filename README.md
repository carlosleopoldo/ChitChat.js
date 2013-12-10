ChitChat.js
============

ChitChat.js is an open-source chat bar client and node.js server that you can easily drop into your website.  Just one line in your web application template and all current users on your site will be able to chat with each other.  The server app is set up to be easily deployable to Heroku.  Similar to Facebook.com's Chat. For a longer explanation, see [here]("http://kyle-dorman.github.io/blog/2013/12/09/why-chitchat-dot-js/").

[DEMO]("http://intense-taiga-9081.herokuapp.com/users/new")

<h3>How to setup the ChitChat.js server:</h3>

1. Clone this repository
2. In the /public/javascripts/chatter_settings.js file, specify where you are deploying the node server to and what site
    you will be adding ChitChat.js to (note, you may not know where the node server is going to be deployed until after
    you deploy, this is ok just change the node_server_url once you do know)
3. Ensure the app has a Procfile with 
    <pre><code>web: node web.js</code></pre>
    This is required for deploying on heroku
5. Deploy to heroku (follow the walkthrough below or, https://devcenter.heroku.com/articles/getting-started-with-nodejs)
  in your console type each of these comands:
  1. heroku create
  2. git push heroku master
  3. heroku ps:scale web=1
  4. maybe write "heroku config:set NODE_ENV=production" // because node server is using Express
  5. heroku labs:enable websockets
  6. if you need to update the node_server_url, do so now and re-git commit and git push heroku master

<h3>How to setup the ChitChat.js client:</h3>

6. Install ChitChat.js in your web app
  1. In your global HTML file add two script files, include two scrpt tags:
  <pre><code>&lt;script src="https://code.jquery.com/jquery.js" &gt;&lt;/script&gt;
  &lt;script data-main="http://NODE_SERVER_URL/javascripts/chitchat"src="http://localhost/javascripts/require.js"&gt;&lt;/script&gt;</code></pre>
    * ChitChat.js is dependant on jQuery. JQuery must be loaded before loading ChitChat.js
  2. Add code to notify ChitChat.js when a user logs into your site. Use ChitChat function:
<pre><code>chatterApp.setUsername(username, callback)</code></pre>
    If the login does not cause a new page to load, no callback needs to be passed to setUsername. If login will require a new page to load, use the form submission as the callback. This allows the ChitChat.js server time to recognize the user login event before the page refreshes (should be wicked fast). In the simplest case, a user will visit a sign in/sign up page and then be rerouted to a new page. If this is the use case for your app, use code similar to example below:
    <pre><code>&lt;script&gt;
        var form = $("#new_user"); // set form to the signin/signup form
        $(form).on("submit", function(e) {
            e.preventDefault();
            chatterApp.setUsername($("#user_name").val(), this.submit());
            // this will trigger the login event on the global chatterApp variable
        });
&lt;/script&gt;</code></pre>

7. Customize the ChitChat.js CSS
  * customizations can be done to the public/stylesheets/chitchat.css file
  
8. And thats it! Test it out with a few users. Please feel free to reach out if any part of this walkthrough is not clear

<h4>Contributing:</h4>
Please feel free to contribute to this project. I am new to the world of open source code but am very receptive to comments/suggestions.
  
<h4>Thoughts:</h4>

* this app is a work in progress
* functionality to regognize a user logout has not been built
* a sass style sheet is needed for easier customization
* I was originally going to call this project chatter.js but switched to chitchat.js. Many variables still use chatter instead of chitchat. I appoligize if this causes any confusion. Eventually I will switch everything to chitchat
