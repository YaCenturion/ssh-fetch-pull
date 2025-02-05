
# 🚀 Remote Fetch & Pull GitHub Action  

This GitHub Action allows you to securely fetch and pull the latest changes from a remote Git repository via SSH.  
It also supports executing custom commands **before and after** the update process.  

## Features  
- ✅ **Secure SSH connection** using a private key  
- ✅ **Git fetch & pull** to update the repository  
- ✅ **Custom pre/post commands** for additional automation  
- ✅ **Easy integration** into any workflow  

## 🛠 Simple example

To use this action in your workflow, add the following to your `.github/workflows/deploy.yml`:  

```yaml
on:
  push:
    branches: [ "deploy" ]
  pull_request:
    branches: [ "deploy" ]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: yacenturion/remote-fetch-pull@v1
        with:
          HOST: "8.10.17.10"
          USERNAME: "root"
          SSH_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
          DEST_PATH: "/srv/myproject"
          RUN_BEFORE: "echo 'Starting deployment...'"
          RUN_AFTER: "systemctl restart nginx; ls -la"
```

## ⚙️ All Inputs  

| Name        | Description                                                 | Required |
|-------------|-------------------------------------------------------------|----------|
| `HOST`      | Target server hostname or IP address.                       | ✅ Yes   |
| `USERNAME`  | SSH username for authentication.                            | ✅ Yes   |
| `SSH_KEY`   | Private SSH key for secure connection (use GitHub Secrets). | ✅ Yes   |
| `DEST_PATH` | Absolute path to the Git repository on the server.          | ✅ Yes   |
| `RUN_BEFORE`| Optional bash commands to execute before `git pull`.        | ❌ No    |
| `RUN_AFTER` | Optional bash commands to execute after `git pull`.         | ❌ No    |
