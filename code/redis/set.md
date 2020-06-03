set with ex, px, nx, xx

In sources code redis gem
```
# Set the string value of a key.
#
# @param [String] key
# @param [String] value
# @param [Hash] options
#   - `:ex => Fixnum`: Set the specified expire time, in seconds.
#   - `:px => Fixnum`: Set the specified expire time, in milliseconds.
#   - `:nx => true`: Only set the key if it does not already exist.
#   - `:xx => true`: Only set the key if it already exist.
# @return [String, Boolean] `"OK"` or true, false if `:nx => true` or `:xx => true`
def set(key, value, options = {})
  args = []

  ex = options[:ex]
  args.concat(["EX", ex]) if ex

  px = options[:px]
  args.concat(["PX", px]) if px

  nx = options[:nx]
  args.concat(["NX"]) if nx

  xx = options[:xx]
  args.concat(["XX"]) if xx

  synchronize do |client|
    if nx || xx
      client.call([:set, key, value.to_s] + args, &BoolifySet)
    else
      client.call([:set, key, value.to_s] + args)
    end
  end
end
```

In ruby code:

`redis.set "key_name", "true", ex: 30`

`redis.set "key_name", "true", px: 30`

`redis.set "key_name", "true", nx: 30`

`redis.set "key_name", "true", xx: 30`
