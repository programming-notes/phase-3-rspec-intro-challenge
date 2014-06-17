# Rspec Overview

### General Testing
- __TDD__
Test Driven Development. Write examples before implementation.
- __BDD__
Behaviour-Driven Development is about implementing an application by describing its behavior from the perspective of its stakeholders. ([The Rspec Book](http://pragprog.com/book/achbd/the-rspec-book))
- __RSpec__
(mention alternatives, write a simple hand sewn test)

### Testing Terms
#### Structure of an example (test)
- __Code Example__
An executable example of how the subject code can be used and its expected behavior. Also called a test, calling tests code examples reinforces the documentation value of RSpec tests.
- __Example Group__
defined with the 'describe' method, pass it a string, which is what we'll be describing, this reinforces the idea that Rspec is used to describe and document a system. 
- __It__
A block which defines a code example

#### Test Implementation
- __Expectations__
A requirement for any test. In code examples we set expectations of what should happen. If the expectations aren't met, the test fails.

```ruby
expect(user.active).to be_true
expect(user.favorites).to include("Ramen")
```

- __Mocks/Doubles/Stubs__
All the same thing. A test double is an object that stands in for another object in an example (test)

```ruby
user = mock(:user)
user = double(:user)
```

- __Message Stubs__
Returning a predefined response to a message within a code example

```ruby
user.stub(:name).and_return("Bobby McFerrin")
user.stub(:name => "Bobby McGee")
user = mock(:user, :name => "Bobby McFerrin")
```

- __Chaining Stubs__
Sometimes you need to stub deep (watch out for this, it's a bad code smell). `stub_chain` can help:

```ruby
user.stub_chain(:account, :billing_address).and_return("717 California St.")
user.account.billing_address # 717 California St.
```

- __Message Expectations__
A method stub that will raise an error if it is never called.

```ruby
user.should_receive(:name).and_return("Bobby McFerrin")
``` 

# Running Tests
#### Default rspec output is lame. Make it pretty

  rspec --color --format documentation some_spec.rb

Better yet, save this to your ~/.rspec config file:

  echo "--color --format documentation" > ~/.rspec
  
#### RSpec with Rails
Add `rspec-rails` to your Gemfile, `bundle install` then `rails generate rspec:install`. Use `rake spec` to run tests.