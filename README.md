README.md

Objective of this project:

- Learn about `link_to`
- Learn about `prefix path`

----------------

<%= link_to("About Page", "/about") %>

gererates this HTML:

<a href="/about">About Page</a>

A cool trick for the 2nd argument.

instead of using the explicit path "/about", you can use the PREFIX path which you can get through "rake routes" on your terminal.  So in this case if the prefix path for "/about" was named "about", our first line would look like this: 
<%= link_to("About Page", about_path) %>

Why its so important to use your PREFIX instead of your URL? Because if your URL changes, as long as you defined your PREFIX, it will not break your code.

so when you define your route it should look like this:

get '/about' => '#about', :as => :about

that way it will keep working whether you change the URL name or not.

One more trick:

Wherever a route has a route variable, like in the example below:
get '/posts/:id' => 'posts#show', :as => :post
(the variable is :id)

the helper method that you will use to generate that method expects an argument for the variable in this route.

So it would look like this:

app.post_path(1)
where post represents the PREFIX and 1 represents the :id.
it will return "/posts/1" URL

Lets say you want to retrieve the last post and so you say: last_post = Post.last

How would you generate the route for that post, what argument should you pass?

app.post_path(last_post.id)

Pretty cool, right?

What is cooler is that you can use this to generate the same URL: 
app.post_path(last_post)

It is important to understand that Rails is not that smart, it is just generating URLs based on the argument passed. Whatever you pass as argument, that is what Rails will use to generate the route, so if you pass something like:
app.post_path("CamelCasedURL") it will generate this route:
"/posts/CamelCasedURL"