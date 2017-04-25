## Parsing command line arguments in a Ruby script

### OptionParser

http://ruby-doc.org/stdlib-2.4.1/libdoc/optparse/rdoc/OptionParser.html

OptionParser is a class for command-line option analysis.

`example.rb`
```ruby
require 'optparse'

options = {}
OptionParser.new do |opts|

  # Simple example
  opts.on("-v", "--verbose", "Run verbosely") do |v|
    options[:verbose] = v
  end

  # Required argument example
  opts.on("-r", "--require LIBRARY", "Require the LIBRARY before executing your script") do |lib|
    options[:lib] = lib
  end
end.parse!

p options[:verbose]
p options[:lib]
```

```bash
# exmpale
$ ruby ./example.rb --require json -v
```


### OpenStruct

https://ruby-doc.org/stdlib-2.3.1/libdoc/ostruct/rdoc/OpenStruct.html

An OpenStruct is similar to a Hash, but allows the definition of arbitrary attributes.

Example

```ruby
require 'ostruct'

person = OpenStruct.new
person.name = "Jinkyou Son"

# also
person = OpenStruct.new(name: "Jinkyou Son")

puts person.name  # -> "Jinkyou Son", amazing!
```


### Combination

```ruby
options = OpenStruct.new
OptionParser.new do |opt|
  opt.on('-i', '--identity IDENTITY_FILE_PATH', 'Identity file path') {|o| options.identity_path = o }
  opt.on('--verbose', 'Run verbosly') {|o| options.verbose = o}
end.parse!

p options.identity_path
p options.verbose
```


Reference:  
http://stackoverflow.com/questions/26434923/parse-command-line-arguments-in-a-ruby-script  
http://ruby-doc.org/stdlib-2.4.1/libdoc/optparse/rdoc/OptionParser.html  
https://ruby-doc.org/stdlib-2.3.1/libdoc/ostruct/rdoc/OpenStruct.html  
