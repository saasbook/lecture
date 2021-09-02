---
title: "Lecture 3: Ruby & SaaS"
---

# Today's Topics

* Learning a New Language
* Playing Around with Ruby
* APIs / REST / More SaaS

# Logsticics

* CHIPS 2.5 Deadline Extended until Friday 11:59PM
* Module 1&2 Quiz on Tuesday, 45 mins, 2pm. (No Lecture)
  * Zoom Links will be emailed to everyone
  * Alternate times: Tuesday evening, Weds Moring
  * Ed post coming soon.

# SaaS In The (Old, But Not Really) News

“10 Lesser Known DOM APIs you may want to use”
https://blog.greenroots.info/10-lesser-known-web-apis-you-may-want-to-use-ckejv75cr012y70s158n85yhn
via https://weekly.statuscode.com

### Highlights:

* Async Clipboard API
* Battery Status API
* Performance API
* Broadcast Channel API

# Q&A

# Let's Talk About Ruby...

<video class="u-full-width" style="height:250px" poster="/assets/posters/talks/wat.poster-4f5425901c10ffeaceb61f82e25dc40b9212aadf078cead0dc6ffe40696e2bec.png" preload="none" controls="">
          <source src="https://destroyallsoftware-talks.s3.amazonaws.com/wat.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&amp;X-Amz-Credential=AKIAIKRVCECXBC4ZGHIQ%2F20210902%2Fus-east-1%2Fs3%2Faws4_request&amp;X-Amz-Date=20210902T062957Z&amp;X-Amz-Expires=14400&amp;X-Amz-SignedHeaders=host&amp;X-Amz-Signature=ed0a96373bccd42447e31b44078aca415a0fd2bc40d1e4b9e233b074b18f0a15">
          <track label="English" kind="captions" srclang="en" src="/captions/talks/wat.vtt">
</video>

[Gary Berndhart, Destroy All Software](https://www.destroyallsoftware.com/talks/wat)

# Learning a new language

(From the book!)

1. Types and typing.
1. Primitives.
1. Methods.
1. Abstraction and Encapsulation.
1. Idioms.
1. Libraries.
1. Debugging.
1. Testing.

# Ruby

Ruby is inspired by Smalltalk.
It's quite permissive, but has a few consistent rules.

* _Everything_ is an object.
  * Yes, even `Integer`.
* _Metaprogramming_ is common in Ruby.
* `a.b` means calling the **method** `b` on object `a`.
* `a + b` is the same as `a.+(b)`
  * `a.b = 3` is calling a method!

# Examples
```ruby
grading_option = :pass_fail
today = { class: 'CS169', lang: 'ruby' }
people = ['Harry', 'Ron', 'Hermione', 'Snape']

def give_bezos_money?(cost, balance)
  cost < balance / 3 # alternatively, just: false
end
```

# Examples

```rb
# A block
[1, 2, 3].each do |num|
  puts "MOAR! #{num*100}"
end

# Another block
[1, 2, 3].map { |number| number * 100 }

# A lambda!
shout = -> (words) { words.upcase }
```
Random Note: A block is _not_ an argument to the function.

# Classes

* Ruby is an OO language, but embraces FP, too.
* Classes can be modified at any time!
* There is no (direct) access to instance variables.
  * We use getters and setters, `attr_reader`, `attr_writer`, `attr_accessor`.
* We can define an `initialize` method.
* We get a new class by calling `Class.new`
* `@instance_variable`, `@@class_variable`, `self`

# Class Example

```ruby
class Book
  @@total_books = 0

  def initialize(title, author)
    @title = title
    @author = author
    @@total_books += 1
  end

  def title
    @title
  end

  def title=(value)
    @title = value
  end

  def author
    @author # these methods use implict returns!
  end

  def author=(value)
    @author = value
  end
end
```

# Metaprogramming an classes

* `attr_accessor` defines setters, getters, and the instance variables.
* `attr_reader` defines the getter and the instance variables.
* `attr_writer` define the setter and the instance variables.

```ruby
class Book
  attr_accessor :title
  attr_accessor :author

  def print_at
   puts "Title #{@title}"
   puts "Author #{@author}"
  end

  def print_self
    puts "Title #{self.title}"
    puts "Author #{self.author}"
  end

  def print_plain
    puts "Title #{title}"
    puts "Author #{author}"
  end
end
```

# Ruby Fun Things

# Blocks, Procs, and Labmdas. Oh my!

[**Read More**](https://www.rubyguides.com/2016/02/ruby-procs-and-lambdas/)

* Blocks and Lambdas: Primary means of passing function-like control around
* Procs: Similar to lambdas, but the `return` applies to the caller. (See the above link for an example)
* Lambdas (and procs) are true closures. Yay!

# Some Ruby Conventions

* End methods with a `?` if they return a boolean.
  * Common style is to avoid `is_`, `has_` prefixes.
* End methods with a `!` if there be dragons.
  * Raises exceptions, mutations are the common cases.

# Some Tips

* Don't go overboard on the syntactic sugar.
* Be careful with mutations in the conditonal statement:

```rb
if @user = lookup_user_from_somewhere
  render :hooray
else
  render :error
end
```

# REST, APIs More SaaS

# REST

"Representatitonal State Transfer"

A Kind of Meaningless name, but a powerful concept.

A **route** is a verb (HTTP Method) and a path.

We use "nesting" in a path to communicate hierarchy.

# A Brief Rant About URLs.

"Uniform Resource Locators"

A URL idetifies an entity, a praticular concept.

Don't break the web. :(

# TheMovieDB

```
curl https://api.themoviedb.org/3/movie/550?api_key=6c22b5cc0c1957087d270e1f9be93f37
```

# (Basic) HTTP Requests in Ruby

[Many Ways to make requests](https://www.rubyguides.com/2018/08/ruby-http-request/)

```ruby
require 'net/http'

Net::HTTP.get('example.com', '/index.html')
```

```ruby
net = Net::HTTP.new("example.com", 443)

net.use_ssl = true
net.get_response("/")
```
