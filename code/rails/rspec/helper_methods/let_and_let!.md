## `let` and `let!`

### 1. `let`
Use `let` to define a memoized helper method. The value will be cached
across multiple calls in the same example but not across examples.

Note that `let` is lazy-evaluated: it is not evaluated until the first time
the method it defines is invoked.

`let` được tạo khi gọi đến nó.

Ex:
```
describe "#get_time" do
  let(:current_time) { Time.now }

  before(:each) do
    puts Time.now # => 2020-05-05 22:04:30 +0700
  end

  it "should return the time" do
    sleep(5)
    puts current_time # => 2020-05-05 22:04:35 +0700
  end
end
```

### 2. `let!`
You can use `let!` to force the method's invocation before each example.

`let!` được tạo ngay khi định nghĩa.

Ex:
```
describe "#get_time" do
  let!(:current_time) { Time.now }

  before(:each) do
    puts Time.now # => 2020-05-05 22:04:30 +0700
  end

  it "should return the time" do
    sleep(5)
    puts current_time # => 2020-05-05 22:04:30 +0700
  end
end
```
