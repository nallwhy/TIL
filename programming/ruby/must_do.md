### Improve your Ruby application's memory usage and performance with jemalloc

https://www.levups.com/en/blog/2017/optimize_ruby_memory_usage_jemalloc_heroku_scalingo.html


### Oj

A fast JSON parser and Object marshaller.

https://github.com/ohler55/oj
https://precompile.com/2015/07/25/rails-activesupport-json.html


### Dig

http://ruby-doc.org/core-2.3.0_preview1/Hash.html#method-i-dig

```ruby
> hash = {a: [{b: [{c: 0}]}]}
=> {:a=>[{:b=>[{:c=>0}]}]}
> hash.dig(:a, 0, :b)
=> [{:c=>0}]
> hash.dig(:a, 1, :b)
=> nil
```


### Why we ended up not using Rails for our new JSON API

https://blog.dnsimple.com/2017/03/why-we-ended-up-not-using-rails-for-our-new-json-api/

Hanami 를 쓰게 되지는 않겠지만, command/service pattern 은 가져와서 쓰면 좋겠다.


### Slim down hefty Rails controllers AND models, using domain model events

https://www.rubytapas.com/2017/04/11/skinny-controller-domain-model-events/


#### Zen Rails Security Checklist

https://github.com/brunofacca/zen-rails-security-checklist


#### Administrate

https://github.com/thoughtbot/administrate

#### ActiveAdmin

https://activeadmin.info/


#### Rails DB

https://github.com/igorkasyanchuk/rails_db

Rails Database Viewer and SQL Query Runner


#### Rails ERD

https://github.com/voormedia/rails-erd

Generating a diagram based on your application's Active Record models


#### Postgres tips for Rails developers

https://www.citusdata.com/blog/2017/04/28/postgres-tips-for-rails/


#### Scout

https://scoutapp.com/

Performance insights for Ruby & Elixir apps.


#### RailsPanel

https://github.com/dejan/rails_panel

Chrome extension for Rails development that will end your tailing of development.log.


#### Letter Opener

https://github.com/ryanb/letter_opener

Preview email in the default browser instead of sending it


#### Devise Masquerade

https://github.com/oivoodoo/devise_masquerade  
https://gorails.com/episodes/devise-masquerade

Login as any user easliy


#### Pry

https://github.com/pry/pry


#### Pundit

https://github.com/elabs/pundit


#### Retryable

https://github.com/nfedyashev/retryable


#### Building APIs with Ruby on Rails and GraphQL

https://www.sitepoint.com/building-apis-ruby-rails-graphql/


#### PgHero

https://github.com/ankane/pghero


#### Mailcatcher

https://gorails.com/episodes/testing-emails-with-mailcatcher


#### How We Made Writing Tests Fun and Easy

https://blog.daftcode.pl/how-we-made-writing-tests-fun-and-easy-2d7e1fac6d16


#### RailsPanel

https://github.com/dejan/rails_panel


#### yield_self

http://mlomnicki.com/yield-self-in-ruby-25/
