# Kubectl Installation on Ubuntu EC2

### Download kubectl
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

### Install Kubectl
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

### Verify Kubectl
```
kubectl version --client
```


**Note: If you are planning to install Docker on any other distributions of linux or other operating systems like Windows, please follow the official documentation for steps.**