Return true if value is empty, else false

```
_.isEmpty(null);
// => true

_.isEmpty(true);
// => true

_.isEmpty(false);
// => true

_.isEmpty(1);
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false

_.isEmpty("");
// => true
```

In Ruby:
```
> nil.nil?
=> true

> true.nil?
=> false

> 2.nil?
=> false

> [1, 2, 3].nil?
=> false

> {a: 1}.nil?
=> false
```

In Rails:
```
Blank?
> nil.blank?
=> true

> true.blank?
=> false

> 2.blank?
=> false

> [1, 2, 3].blank?
=> false

> {a: 1}.blank?
=> false

> false.blank?
=> true

> "".blank?
=> true

```
