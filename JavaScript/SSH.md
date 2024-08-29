### SSH的主要功能：

1. **远程登录**：允许用户通过命令行连接到远程服务器，并执行命令。
2. **文件传输**：可以使用`scp`（secure copy）或`SFTP`（SSH File Transfer Protocol）来安全地传输文件。
3. **端口转发**：可以通过SSH加密其他协议的通信，比如通过SSH隧道来转发HTTP流量。

### SSH的工作原理：

SSH通过使用公钥加密和对称加密的组合来确保数据传输的机密性和完整性。连接过程中，客户端和服务器首先进行密钥交换，然后使用加密通道进行通信。

### 常见的SSH命令：

- `ssh user@hostname`：连接到远程主机。
- `scp file user@hostname:/path`：通过SSH传输文件。
- `sftp user@hostname`：使用SFTP传输文件。

SSH广泛用于服务器管理、开发环境的远程控制，以及保障通信的安全。