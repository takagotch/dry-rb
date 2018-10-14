### dry-rb
---
https://github.com/dry-rb

https://dry-rb.org/


#### dry-validation
#### dry-types
#### ...

```ruby
schema = Dry::Validation.Params do
  required(:name).filled
  required(:age).filled(:int?, gt?: 18)
end
schema.("name" => "Jane", "age" => "30").to_h
schema.("name" => "Jane", "age" => "17").messages


module Types
  include Dry::Types.module
  Greeting = Strict::String.enum("Hello", "Hola")
end
Types::Greeting["Hello"]
Types::Greeting["Goodbye"]

class Person < Dry::Struct
  attribute :name, Types::Strict::String
  attribute :age, Types::Strict::Integer
end
Persion.new(name: "Jane", age: 30)

class App < Dry::System::Container
  configure do |config|
    config.auto_register = %w[lib]
  end
  load_paths! "lib"
end

require "app/import"
class CreateAtricle
  include App::Import[repo: "repositories.articles"]
  def call(input)
    repo.create(input)
  end
end

Dry::Monads::Maybe(user).fmap(&:address).fmap(&:street)

class CreateArticle
  include Dry::Monads::Result::Mixin
  include Dry::Matcher.for(:call, with: Dry::Matcher::ResultMatcher)
  def call(input)
    if success?(input)
      output = some_action(input)
      Success(output)
    else
      Failure(input)
    end
  end
  create = CreateArticle.new
  create.(input) do |m|
    m.success do |output|
    end
    m.failure do |err|
    end
  end
end

```

