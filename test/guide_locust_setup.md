# Setting up locust

## 1. Install pip3
```
sudo apt-get install python3-pip
```

## 2. Install virtualenv
```
sudo pip3 install virtualenv
```

## 3. Create workspace
```
mkdir <workspace_name>
cd <workspace_name>
```

## 4. Setup virtual env
```
virtualenv -p py python3
source venv/bin/activate
```
## 5. Install locust
```
pip3 install locust
```
Check locust version.
