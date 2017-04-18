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
