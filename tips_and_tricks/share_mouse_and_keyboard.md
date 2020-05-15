## How to share mouse and keyboard between computers

### Step 1: Install Synergy
```
sudo apt install synergy
```
Note: Install on all computer to use
### Step 2: Setup the server
1. Open GUI of synergy
2. Click on "Server (share this computer's mouse and keyboard)"
3. Click button "Configure Server..."
4. On GUI of "Server configuration": add client computer: Enter screen name of client computer -> click OK
![](https://assets-global.website-files.com/5ce412cc94cd9f8474fdc392/5d4820f6baced77f37d61840_19f3fd3c2105f1039dd30cec54758f5ad3de6b98_serverconfigannotated.png)
5. Click start

### Step 3: Setup the client
1. Open GUI of synergy
2. Click on "Client (use another computer's mouse and keyboard)"
3. Enter server IP
4. Click start

**Bonus:**
- Show ip on ubuntu: `ifconfig`
- Show hostname on ubuntu: `hostname`
