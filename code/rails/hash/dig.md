
## Dig accept dynamic variables

I have an array:
```
image_path = ["avatar", "image", "url"]
```
and a hash:
```
object:
{
  "id": 1
  "name": "SuSindo"
  "avatar": {
    "image": {
      "url": "https://profile.me"
    }
  }
}
```

Now, I want to get url by image_path
```
object.dig("avatar", "image", "url")
=> "https://profile.me"
```
If I follow the example above, I must pass the correct order of the keys to get value.

**If I have a dynamic array, I can't do that.**
```
object.dig(image_path)
=> nil
```
Add * before image_path array:
```
object.dig(*image_path)
=> "https://profile.me"
```
