Here's a generic Ruby class:

```ruby
class Car
  attr_reader :color, :make
 
  def initialize(color, make)
    @color = color
    @make = make
  end
 
  def repaint(color)
    @color = color
  end
end
```

Now if I asked you to write some tests for it, you might write some code like this:

```ruby
car = Car.new("red", "mazda") # we expect this line of code to successfully create a new Car object, right?
puts car.make                 # this should output "mazda"
puts car.repaint("blue")      # this shouldn't cause any errors
puts car.color                # this should output "blue"
```

Instead of writing driver code to test the class, here's how you would test it using Rspec:

```ruby
require "rspec"
require_relative "car"
 
describe Car do
  let(:car) { Car.new("red", "mazda") }
 
  context "#initialize" do
    it "creates a Car object" do
      expect(car).to be_an_instance_of Car
    end
 
    it "requires two parameters" do
      expect { Car.new }.to raise_error(ArgumentError)
    end
  end
 
  context "#color" do
    it "should return the color" do
      expect(car.color).to eq "red"
    end
  end
 
  context "#make" do
    it "should return the make" do
      expect(car.make).to eq "mazda"
    end
  end
 
  context "#repaint" do
    it "requires a parameter" do
      expect { car.repaint }.to raise_error(ArgumentError)
    end
 
    it "returns the color" do
      expect(car.repaint("blue")).to eq "blue"
    end
 
    it "should change the color of the car" do
      car.repaint("blue")
      expect(car.color).to eq "blue"
    end
  end
end
```
