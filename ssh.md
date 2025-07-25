# SSH Configs

## How to troubleshoot your ssh config
   ```bash
   sudo sshd -t
   ```

## How to remove a known host from the list
   ```bash
   ssh-keygen -R <hostname_or_ip>
   ```

## How to add ssh key to agent
   ```bash
   ssh-add /path/to/private/ssh/key
   ```

## How to copy a public ssh key to server
  ```bash
  ssh-copy-id -i /public/key/location.pub username@server_ip
  ```

## How to generate a new ssh key in Windows 
  ```powershell
  ssh-keygen -t ed25519 -C "your_email@example.com"
  Get-Service -Name ssh-agent | Set-Service -StartupType Manual
  Start-Service ssh-agent
  ssh-add -l
  ssh-add c:/Users/USERNAME/.ssh/id_ed25519
  ```

## How to generate a new ssh key in Linux
  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.com"
  eval ssh-agent
  echo $SSH_AGENT_SOCK
  ssh-add -l
  ssh-add c:/Users/USERNAME/.ssh/id_ed25519
  ```

## How to check ssh authentication
   ```bash
   ssh -vT git@github.com
   ```

## List ssh keys added to the agent
   ```bash
   ssh-add -l
   ```

## Config

### Global SSH Config
    ```sshconfig
    Host *
    User your-username            # Default username for SSH connections
    IdentityFile ~/.ssh/id_rsa    # Default SSH private key
    ServerAliveInterval 60        # Keep connection alive every 60 seconds
    Compression yes               # Enable compression to speed up transfer
    ForwardAgent yes              # Forward SSH agent
    ```

### Example for a specific server
    ```sshconfig
    Host myserver
    HostName example.com          # Actual server hostname or IP address
    User admin                    # Override default username
    Port 2222                     # Use a custom SSH port
    IdentityFile ~/.ssh/my_key    # Use a specific SSH key for this server
    LocalForward 8080 localhost:80 # Forward local port 8080 to remote port 80
    ```

### Another example with a short alias
    ```sshconfig
    Host devbox
    HostName 192.168.1.10
    User developer
    Port 22
    IdentityFile ~/.ssh/id_dev
    ProxyJump bastion.example.com # Jump through a bastion host
    ```

### Example for GitHub
    ```sshconfig
    Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_key
    ```
