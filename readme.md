## Install helm
- On Mac
```
brew install helm
```

- On Windows via choco
```
choco install kubernetes-helm
```

- On Windows manual installation:
Go to the Helm GitHub releases page.

Download the latest Windows .zip file, e.g., helm-v3.x.x-windows-amd64.zip.

Extract the file to a directory of your choice.

Add the extracted folder to your system PATH  and open powershell and try `helm version` command


- On Debian/Ubuntu
```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

- On Linux
```
sudo dnf install helm
```

### Generate the manifests:
`helm template -g --output-dir ./ymls . -f stage/values.yaml -f stage/secrets.yaml`

### Install, Uninstall, List
- To install
```
helm install --dry-run wordpress-db -n wpdb . -f dev/values.yaml
helm install wordpress-db -n wpdb . -f dev/values.yaml -f dev/secrets.yaml --create-namespace
helm ls -n wpdb

helm install wordpress-app -n wpapp . -f dev/values.yaml -f dev/secrets.yaml --create-namespace
helm ls -n wpapp
```

- To upgrade
```
helm upgrade wordpress-db -n wpdb . -f dev/values.yaml -f dev/secrets.yaml
```
- To uninstall
```
helm uninstall wordpress-db -n wpdb
helm uninstall wordpress-app -n wpapp

```

### DB Connection issue
- the volume is used for db container is hostpath. if db is configured incorrectly, the miss-configured db files will be stored in the volume. Untill the volume is cleared, you will get db issue

- check the env variables
