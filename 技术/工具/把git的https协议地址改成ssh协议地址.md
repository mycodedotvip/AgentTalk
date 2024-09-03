要将 GitHub 仓库的远程地址从 HTTPS 改为 SSH，可以按照以下步骤操作：

### 1. **查看当前远程仓库地址**
   首先，可以使用以下命令查看当前的远程仓库地址：
   ```bash
   git remote -v
   ```
   这会显示当前配置的远程仓库的地址。

### 2. **更改远程仓库地址为 SSH**
   使用 `git remote set-url` 命令，将仓库的远程地址改为 SSH 版本。以下是更改命令的格式：
   ```bash
   git remote set-url origin git@github.com:username/repository.git
   ```
   其中，`username` 是你的 GitHub 用户名，`repository` 是你的仓库名称。

### 3. **验证修改是否成功**
   再次使用 `git remote -v` 命令，确认远程仓库的地址已经更新为 SSH 协议：
   ```bash
   git remote -v
   ```

### 4. **测试 SSH 连接**
   确保你已经设置了 SSH 密钥，并且密钥已添加到你的 GitHub 账户。如果没有，可以参考 [GitHub 官方文档](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) 来配置 SSH 密钥。

   通过 `git pull` 或 `git push` 命令，测试 SSH 连接是否正常。

这样，你的 GitHub 仓库远程地址就成功从 HTTPS 改成 SSH 了。
