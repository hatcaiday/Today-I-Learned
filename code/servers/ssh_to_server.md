# How to ssh to server

## 1. Get ssh file.
## 2. Run command:
```
ssh username@ip_server -i link_to_your_ssh_file
```
## 3. Show docker image:
```
docker ps
```
## 4. Attach docker image to show log:
```
docker logs -f image_name
```

## 5. Run rails console
- cd to rails app
```
cd applications/rails app_name
docker-compose exec app bash
bin/rails c
```
