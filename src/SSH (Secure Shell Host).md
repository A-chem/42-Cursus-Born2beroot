SSH (Secure Shell) is a cryptographic network protocol used for securely accessing remote computers over an unsecured network. It's commonly used for logging into remote systems, executing commands, transferring files, and managing network infrastructure. SSH ensures that communication is encrypted, providing confidentiality and integrity of data exchanged between a client and a server.

Here are some key components of SSH:

1. **SSH Client**: A program used to connect to an SSH server (e.g., `ssh` command in Linux/Mac or tools like PuTTY in Windows).
2. **SSH Server**: The server running the SSH service that listens for incoming connections (commonly the `sshd` daemon).
3. **Authentication**: SSH supports two main types of authentication:
    - **Password Authentication**: Using a password to verify identity.
    - **Public Key Authentication**: Using a key pair (public and private keys) for more secure authentication.
4. **Encryption**: All data transferred over SSH is encrypted to prevent interception.
5. **Port**: By default, SSH uses port 22, but this can be customized for security reasons.
6. **File Transfer**: SSH supports secure file transfers using protocols like [[TCP (Transmission Control Protocol)]]
### **Step-by-Step Process of How SSH Works:**

SSH uses the client-server model. To establish a secure SSH channel, the two parties need to establish a TCP connection, negotiate the version number and algorithms to be used, and generate the same session key for subsequent symmetric encryption. After the user authentication is complete, the two parties can establish a session for data exchange. The SSH working process consists of the following phases:

#### 1. **Key Pair Generation**

- Imagine you have two "keys": a **public key** (like a lock that anyone can use) and a **private key** (like a key that only you can use).
- You create these two keys using a command on your computer. The public key is shared with the server (the remote computer you want to connect to), and you keep the private key secure.

#### 2. **Connecting to the Server**

- You use a program (like the `ssh` command) to connect to a server. This is like calling someone on the phone, but over the internet.
- SSH uses a port for communication. Before an SSH connection is established, the SSH server listens to connection requests on a specified port. After an SSH client sends a connection request to the specified port of the SSH server, a TCP connection is established between the SSH client and the SSH server, which then communicate with each other through this port.

#### 3. **Agreeing on How to Talk (Version and Algorithms)**

- When you call the server, both you and the server first check what kind of encryption (security) methods you will use to keep the conversation private. This is like agreeing on how to talk in a secret code before you start chatting.
- The SSH server and client negotiate to determine the SSH version to be used with the following process:

1. The SSH server sends the supported SSH version information to the SSH client through the established connection.

2. After receiving the version information, the SSH client determines the version to be used based on the SSH version it supports and sends the version to the SSH server.

3. The SSH server checks whether it supports the version determined by the client; if so, the version negotiation is successful

- SSH uses multiple types of algorithms, including the key exchange algorithm for generating session keys, symmetric encryption algorithm for data encryption, public key algorithm for digital signature and authentication, and HMAC algorithm for data integrity protection

#### 4. **Sending the Public Key**

- You send your **public key** to the server, telling it, "I have this key, and you can use it to check that I am who I say I am."

#### 5. **Login Request**

- The server looks at the public key you sent and checks if it matches any of the keys stored on the server.
- If it finds a match, it knows you are allowed to connect.

#### 6. **Server Sends a Secret (Session Key)**

- The server sends a random number (like a secret code) to your computer, but it **encrypts** this number using your **public key**.
- This is like sending a locked box to you, where only you can open it with your private key.

#### 7. **Unlocking the Secret (Private Key)**

- You use your **private key** to open the locked box and get the secret code (session key) that the server sent. This session key is a special key that will be used to encrypt everything you send and receive after this.

#### 8. **Now You Both Have the Same Key**

- Now that both you and the server have the same secret session key, you can use it to encrypt all your messages. This makes sure that no one else can read your messages.

**SSH key exchange**

1. The SSH server generates prime numbers **G** and **P**, and the server's private key **b**, and calculates the server's public key **y** using the following formula: **y = (G^b)%P**.

2. The SSH server sends prime numbers **G** and **P** and the server's public key **y** to the SSH client.

3. The SSH client generates a private key **a** and calculates a client public key **x** using the following formula: **x = (G^a)%P**.

4. The SSH client sends the client public key **x** to the SSH server.

5. The SSH server calculates the symmetric key **K** using the formula **K = (x^b)%P**, and the SSH client calculates the symmetric key **K** using the formula **K = (y^a)%P**. The mathematical law ensures that the symmetric keys generated by the SSH server and client are the same.

#### 9. **Send and Receive Encrypted Messages**

- After agreeing on the session key, you can send commands or data to the server. Everything you send is "locked" with the session key, and the server will "unlock" it using the same key. The server will also send you encrypted responses, which you can unlock with the same key.

#### 10. **SSH Tunneling (Forwarding Ports)**

- SSH can also create a **secure tunnel** for your data. Think of it like building a safe underground tunnel between you and the server. Anything you send through this tunnel is secure and can't be easily intercepted.
- For example, you can use a command like `ssh -L 8080:localhost:80` to securely forward traffic from your local computer's port 8080 to port 80 on the remote server. This is useful if you want to access a website on the server but keep it secure.


[[image(ssh).webp]]fgc