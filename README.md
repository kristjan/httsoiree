# httsoiree

Like HTTParty, just a little less in your face.

## Install

```
gem install httsoiree
```

## Requirements

* Ruby 1.9.3 or higher
* multi_xml
* You like to converse with friends, perhaps over drinks.

## Usage

A drop-in replacement to HTTParty - you can even keep typing HTTParty. Or, if you prefer, you can HTTSoiree.

## Examples

```ruby
# Use the class methods to get down to business quickly
response = HTTSoiree.get('https://api.stackexchange.com/2.2/questions?site=stackoverflow')

puts response.body, response.code, response.message, response.headers.inspect

# Or wrap things up in your own class
class StackExchange
  include HTTSoiree
  base_uri 'api.stackexchange.com'

  def initialize(service, page)
    @options = { query: {site: service, page: page} }
  end

  def questions
    self.class.get("/2.2/questions", @options)
  end

  def users
    self.class.get("/2.2/users", @options)
  end
end

stack_exchange = StackExchange.new("stackoverflow", 1)
puts stack_exchange.questions
puts stack_exchange.users
```

See the [examples directory](http://github.com/jnunemaker/httparty/tree/master/examples) for even more goodies.

## Command Line Interface

httsoiree also includes the executable `httsoiree` which can be
used to query web services and examine the resulting output. By default
it will output the response as a pretty-printed Ruby object (useful for
grokking the structure of output). This can also be overridden to output
formatted XML or JSON. Execute `httsoiree --help` for all the
options. Below is an example of how easy it is.

```
httsoiree "https://api.stackexchange.com/2.2/questions?site=stackoverflow"
```

## Help and Docs

* https://groups.google.com/forum/#!forum/httparty-gem
* http://rdoc.info/projects/jnunemaker/httparty

## Contributing

Contribute to https://github.com/jnunemaker/httparty. This fork will stay pegged to the latest version.
