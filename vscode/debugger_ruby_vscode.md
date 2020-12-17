# How to debugger ruby in VSCode

Bước 1: Install extension ruby

Bước 2: Tạo file launch.json
```
{
  "name": "Rails server",
  "type": "Ruby",
  "request": "launch",
  "cwd": "${workspaceRoot}",
  "program": "${workspaceRoot}/bin/rails",
  "args": [
     "server"
  ],
  "env": {
    "PATH": "$PATH",
  },
  "pathToRDebugIDE": "pathToRDebugIDE",
}
```

Để get env PATH và pathToRDebugIDE bạn chạy lệnh sau:
```
printf "\n\"env\": {\n  \"PATH\": \"$PATH\"\n}\n"
```

Get đầy đủ
```
printf "\n\"env\": {\n  \"PATH\": \"$PATH\",\n  \"GEM_HOME\": \"$GEM_HOME\",\n  \"GEM_PATH\": \"$GEM_PATH\",\n  \"RUBY_VERSION\": \"$RUBY_VERSION\"\n}\n\n"
```


```
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Rails server",
      "type": "Ruby",
      "request": "launch",
      "cwd": "${workspaceRoot}",
      "program": "${workspaceRoot}/bin/rails",
      "args": [
         "server"
      ],
      "env": {
        "PATH": "/home/do.thi.nhung/.rbenv/shims:/home/do.thi.nhung/.rbenv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin",
      },
      "pathToRDebugIDE": "/home/do.thi.nhung/.rbenv/versions/2.6.5/bin/rdebug-ide",
    }
  ]
}

```
