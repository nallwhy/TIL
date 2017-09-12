### 2017-09-08

#### Mailcatcher

https://github.com/sj26/mailcatcher  
https://gorails.com/episodes/testing-emails-with-mailcatcher


#### How We Made Writing Tests Fun and Easy

https://blog.daftcode.pl/how-we-made-writing-tests-fun-and-easy-2d7e1fac6d16


#### ruby-vips

This gem provides a Ruby binding for the libvips image processing library.

https://github.com/jcupitt/ruby-vips


### 2017-09-05

#### Deploying Ruby on Rails application to Heroku using Docker

https://www.amberbit.com/blog/2017/6/17/deploying-ruby-on-rails-application-to-heroku-using-docker/

#### Concurrent Ruby

https://github.com/ruby-concurrency/concurrent-ruby


### 2017-09-02

#### How to make Ajax calls — The Rails way

https://m.patrikonrails.com/how-to-make-ajax-calls-the-rails-way-20174715d176


### 2017-09-01

#### The Safe Navigation Operator (&.) in Ruby

http://mitrev.net/ruby/2015/11/13/the-operator-in-ruby/


### 2017-06-13

#### Letter Opener

https://github.com/ryanb/letter_opener

Preview email in the default browser instead of sending it

#### Devise Masquerade

https://github.com/oivoodoo/devise_masquerade  
https://gorails.com/episodes/devise-masquerade

Login as any user easliy

#### Retryable

https://github.com/nfedyashev/retryable

#### Building APIs with Ruby on Rails and GraphQL

https://www.sitepoint.com/building-apis-ruby-rails-graphql/


### 2017-05-26

#### Rails Speed with Ruby 2.4.0 and Current Discourse

http://engineering.appfolio.com/appfolio-engineering/2017/5/22/rails-speed-with-ruby-240-and-discourse-180

Update your Ruby!


### 2017-05-11

#### RailsPanel

https://github.com/dejan/rails_panel

Chrome extension for Rails development that will end your tailing of development.log.


### 2017-05-09

#### Rails 5.1 has introduced Date#all_day helper

http://blog.bigbinary.com/2017/04/24/rails-5-1-has-introduced-date-all_day-helper.html

```ruby
# Old
User.where(created_at: Date.today.beginning_of_day..Date.today.end_of_day)

# New
User.where(created_at: Date.today.all_day)
```

##### Rob Biedenharn's comment

The only problem with this is actually a problem with BETWEEN. If you have a timestamp that is 2017-04-09 23:59:59.5 UTC (just a half second before the day changes), then neither of these will capture that timestamp:

```
>> Date.today.all_day

=> Sun, 09 Apr 2017 00:00:00 UTC +00:00..Sun, 09 Apr 2017 23:59:59 UTC +00:00

>> Date.tomorrow.all_day

=> Mon, 10 Apr 2017 00:00:00 UTC +00:00..Mon, 10 Apr 2017 23:59:59 UTC +00:00
```

if `d` is some date, then the proper range is:

`d ... (d+1)` (note the range-end-excluding syntax) giving:

`column >= d AND column < (d+1)`


### 2017-05-05

#### Administrate

https://github.com/thoughtbot/administrate

#### Rails DB

https://github.com/igorkasyanchuk/rails_db

Rails Database Viewer and SQL Query Runner

#### Rails ERD

https://github.com/voormedia/rails-erd

Generating a diagram based on your application's Active Record models

#### Postgres tips for Rails developers

https://www.citusdata.com/blog/2017/04/28/postgres-tips-for-rails/


### 2017-05-02

#### contracts.ruby

https://github.com/egonSchiele/contracts.ruby

#### Improve your Ruby application's memory usage and performance with jemalloc

https://www.levups.com/en/blog/2017/optimize_ruby_memory_usage_jemalloc_heroku_scalingo.html

#### Slim down hefty Rails controllers AND models, using domain model events

https://www.rubytapas.com/2017/04/11/skinny-controller-domain-model-events/

#### Zen Rails Security Checklist

https://github.com/brunofacca/zen-rails-security-checklist

#### R14 - Memory Quota Exceeded in Ruby (MRI)

https://devcenter.heroku.com/articles/ruby-memory-use


### 2017-04-30

#### Converting number to string with comma on Rails

http://stackoverflow.com/questions/1078347/is-there-a-rails-trick-to-adding-commas-to-large-numbers

```ruby
123456789.to_s(:delimited) # => "123,456,789"
```


### 2017-04-26

#### Build a RESTful JSOn API with Rails 5

https://scotch.io/tutorials/build-a-restful-json-api-with-rails-5-part-one

Good tutorial.


### 2017-04-25

#### Oj

A fast JSON parser and Object marshaller.

https://github.com/ohler55/oj
https://precompile.com/2015/07/25/rails-activesupport-json.html

#### Running command line commands within Ruby script and Getting stdout.

`%x[echo hi]`

http://stackoverflow.com/questions/3159945/running-command-line-commands-within-ruby-script


### 2017-04-24

#### Call ruby function from command-line

http://stackoverflow.com/questions/10316495/call-ruby-function-from-command-line

`test.rb`
```ruby
def test_function
  "hello"
end
```

```bash
$ ruby -r "./test.rb" -e "puts test_function 'hi'"
hello
```

But as it uses stdout by `puts`, it returns **all** messages of execution. BAD.


### 2017-04-21

#### Dig

http://ruby-doc.org/core-2.3.0_preview1/Hash.html#method-i-dig

```ruby
> hash = {a: [{b: [{c: 0}]}]}
=> {:a=>[{:b=>[{:c=>0}]}]}
> hash.dig(:a, 0, :b)
=> [{:c=>0}]
> hash.dig(:a, 1, :b)
=> nil
```


### 2017-04-18

#### Enumerize

https://github.com/brainspec/enumerize


### 2017-04-13

#### Get nth weekday for a given month

http://stackoverflow.com/questions/20283667/how-to-determine-the-nth-weekday-for-a-given-month

```ruby
def nth_weekday(year, month, n, wday)
  first_day = DateTime.new(year, month, 1)
  arr = (first_day..(first_day.end_of_month)).to_a.select {|d| d.wday == wday }
  n == 'last' ? arr.last : arr[n - 1]
end
```


### 2017-04-12

#### RubyMonk

https://rubymonk.com/

RubyMonk, the best site to learn Ruby ever, has come back!


### 2017-04-07

#### Hanami

http://hanamirb.org/

Hanami 1.0 is released!

#### One Line of Code that Compromises Your Server

https://martinfowler.com/articles/session-secret.html

Secret key 보안에 관련된 이야기. It's not only for rails but for other web platforms.


### 2017-03-28

#### Why we ended up not using Rails for our new JSON API

https://blog.dnsimple.com/2017/03/why-we-ended-up-not-using-rails-for-our-new-json-api/

Hanami 를 쓰게 되지는 않겠지만, command/service pattern 은 가져와서 쓰면 좋겠다.
