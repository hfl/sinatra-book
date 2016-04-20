初识 Sinatra
=======================

## 太魔性了

您在概述一章里已经知道了如何安装 Sinatra、他的依赖程序，然后还写了一个 "hello world" 程序。在这章里您将进入框架旋风之旅来互相熟悉一下。

## 路由

Sinatra 在路由方面表现的超级有弹性，他使用 HTTP 方法和正则表达式来匹配请求的 URL。最基本的 HTTP 请求方法有：

*   GET
*   POST
*   PATCH
*   PUT
*   DELETE

路由就是程序的主干，他们就像导航图来协调用户和程序之间的互动。

您很容易就可以构建起 [RESTful 网络服务][restful-web-services]。下面就一个例子：

```ruby
get '/dogs' do
  # get a listing of all the dogs
end

get '/dog/:id' do
  # just get one dog, you might find him like this:
  @dog = Dog.find(params[:id])
  # using the params convention, you specified in your route
end

post '/dog' do
  # create a new dog listing
end

put '/dog/:id' do
  # HTTP PUT request method to update an existing dog
end

patch '/dog/:id' do
  # HTTP PATCH request method to update an existing dog
  # See RFC 5789 for more information
end

delete '/dog/:id' do
  # HTTP DELETE request method to remove a dog who's been sold!
end
```

As you can see from this contrived example, Sinatra's routing is very easy to get
along with. Don't be fooled, though, Sinatra can do some pretty amazing things
with Routes.

Take a more in-depth look at [Sinatra's routes][routes], and see for yourself.

[routes]: http://www.sinatrarb.com/intro#Routes
[restful-web-services]: http://en.wikipedia.org/wiki/Representational_State_Transfer#RESTful_web_services
[RFC 5789]: http://www.rfc-base.org/rfc-5789.html

## 过滤器

Sinatra offers a way for you to hook into the request chain of your
application via [Filters][filters].

Filters define two methods available, `before` and `after` which both accept a
block to yield corresponding the request and optionally take a URL pattern to
match to the request.

### 之前（before）

The `before` method will let you pass a block to be evaluated **before** _each_
and _every_ route gets processed.

```ruby
before do
  MyStore.connect unless MyStore.connected?
end

get '/' do
  @list = MyStore.find(:all)
  erb :index
end
```

In this example, we've set up a `before` filter to connect using a contrived
`MyStore` module.

### 之后（after）

The `after` method lets you pass a block to be evaluated **after** _each_ and
_every_ route gets processed.

```ruby
after do
  MyStore.disconnect
end
```

As you can see from this example, we're asking the `MyStore` module to
disconnect after the request has been processed.

### 模式匹配

Filters optionally take a pattern to be matched against the requested URI
during processing. Here's a quick example you could use to run a contrived
`authenticate!` method before accessing any "admin" type requests.

```ruby
before '/admin/*' do
  authenticate!
end
```

[filters]: http://www.sinatrarb.com/intro#Filters

## Handlers

Handlers are top-level methods available in Sinatra to take care of common HTTP
routines. For instance there are handlers for [halting][halting] and
[passing][passing].

There are also handlers for redirection:

```ruby
  get '/' do
  redirect '/someplace/else'
end
```

This will return a 302 HTTP Response to `/someplace/else`.

You can even use the Sinatra handler for sessions, just add this to your
application or to a configure block:

```ruby
enable :sessions
```

Then you will be able to use the default cookie based session handler in your
application:

```ruby
get '/' do
  session['counter'] ||= 0
  session['counter'] += 1
  "You've hit this page #{session['counter']} times!"
end
```

Handlers can be extremely useful when used properly, probably the most common
use is the `params` convention, which gives you access to any parameters passed
in via the request object, or generated in your route pattern.

[halting]: http://www.sinatrarb.com/intro#Halting
[passing]: http://www.sinatrarb.com/intro#Passing


## 模板

Sinatra is built upon an incredibly powerful templating engine, [Tilt][tilt].
Which, is designed to be a "thin interface" for frameworks that want to support
multiple template engines.

Some of Tilt's other all-star features include:

*   Custom template evaluation scopes / bindings
*   Ability to pass locals to template evaluation
*   Support for passing a block to template evaluation for "yield"
*   Backtraces with correct filenames and line numbers
*   Template file caching and reloading

Best of all, Tilt includes support for some of the best templating engines
available, including [HAML][haml], [Less CSS][less], and
[CoffeeScript][coffeescript]. Also a ton of other lesser known, but equally
awesome [templating languages][tilt] that would take too much space to list.

All you need to get started is `erb`, which is included in Ruby. Views by
default look in the `views` directory in your application root.

So in your route you would have:

```ruby
get '/' do
  erb :index # renders views/index.erb
end
```

or to specify a template located in a subdirectory


```ruby
get '/' do
  erb :"dogs/index"
  # would instead render views/dogs/index.erb
end
```

Another default convention of Sinatra, is the layout, which automatically looks
for a `views/layout` template file to render before loading any other views. In
the case of using `erb`, your `views/layout.erb` would look something like
this:

```ruby
<html>
  <head>..</head>
  <body>
    <%= yield %>
  </body>
</html>
```

The possibilities are pretty much endless, here's a quick list of some of the
most common use-cases covered in the README:

*   [Inline Templates][inline]
*   [Embedded Templates][embedded]
*   [Named Templates][named]

For more specific details on how Sinatra handles templates, check the [README][templates].

[tilt]: http://github.com/rtomayko/tilt
[haml]: http://haml-lang.com/
[less]: http://lesscss.org/
[coffeescript]: http://coffeescript.org/
[inline]: http://www.sinatrarb.com/intro#Inline%20Templates
[embedded]: http://www.sinatrarb.com/intro#Embedded%20Templates
[named]: http://www.sinatrarb.com/intro#Named%20Templates
[templates]: http://www.sinatrarb.com/intro#Views%20/%20Templates

## 帮助方法

Helpers are a great way to provide reusable code snippets in your application.

```ruby
helpers do
  def bar(name)
    "#{name}bar"
  end
end

get '/:name' do
  bar(params[:name])
end
```
