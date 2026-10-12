## Server-side configuration file

- **Used by**: SSH server (on the remote server you are connecting to).
- **Purpose**: Configures the SSH server itself. This file controls **how the server** handles incoming SSH connections.
- **Where it is**: `/etc/ssh/sshd_config`

**Example**:  
On the server side, you might want to restrict certain types of connections. For instance, you can disable **root login** or set rules for how passwords should be handled.

`PermitRootLogin no PasswordAuthentication yes`

This means that the server **does not allow root logins**, and **password-based authentication is allowed**.

**Examples of configuration options in `sshd_config`**:

- `PermitRootLogin` – Specifies whether root login is allowed via SSH.
- `PasswordAuthentication` – Defines whether password-based authentication is permitted.
- `PubkeyAuthentication` – Enables or disables public key authentication.
- `Port` – Defines the port that the SSH server listens on.
- `AllowUsers` – Specifies which users are allowed to connect to the SSH server.
- `MaxAuthTries` – Sets the maximum number of authentication attempts before the connection is closed.