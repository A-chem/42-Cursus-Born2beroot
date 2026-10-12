### **Client-side configuration file**

- **Used by**: SSH client (on your computer, when you connect to a server).
- **Purpose**: Configures how your computer behaves when connecting to **other** computers (the servers).
- **Where it is**:
    - System-wide: `/etc/ssh/ssh_config`
    - User-specific: `~/.ssh/config`

**Example**:  
If you always connect to a server using a specific username or port, you can define that in `ssh_config`, so you don’t have to type it each time.

`Host myserver.com   User myusername   Port 2222`

This means that every time you use `ssh myserver.com`, it will automatically use `myusername` and port `2222` without you needing to specify them.

- **Examples of configuration options in `ssh_config`**:
    
    - `Host` – Specifies the host or alias for which the configuration applies.
    - `User` – Defines the default username to use for connections to certain hosts.
    - `Port` – The default port for the SSH connection (usually 22).
    - `IdentityFile` – Specifies the private key file for authentication.
    - `ForwardAgent` – Allows SSH agent forwarding.
    - `ProxyJump` – Specifies a jump host for routing SSH connections