## Docker Install into Termius

**``GENERAL STEPS AT THE TERMIUS TERMINAL``**

### 1. Update the system:
```
sudo apt-get update
```

### 2. Install dependencies:
```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

### 3. Add official Docker GPG key:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

### 4. Add Docker repository:
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

### 5. Install Docker CE:
```
sudo apt-get update
sudo apt-get install docker-ce
```

### 6. Verify the installation:
```
sudo docker run hello-world
```
OR
```
sudo docker --version
```