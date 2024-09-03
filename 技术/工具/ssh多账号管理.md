在使用 SSH 连接多个 GitHub 账户时，管理不同的 SSH 密钥是关键。以下是设置和管理多个 SSH 账号的方法：

### 1. **生成多个 SSH 密钥对**
为每个 GitHub 账号生成一个 SSH 密钥对：
```bash
ssh-keygen -t rsa -C "email@example.com" -f ~/.ssh/id_rsa_github_personal
ssh-keygen -t rsa -C "work@example.com" -f ~/.ssh/id_rsa_github_work
```
这里，`-f` 参数指定了密钥文件的保存路径和文件名。

### 2. **添加 SSH 密钥到 SSH 代理**
为每个密钥添加到 SSH 代理：
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_github_personal
ssh-add ~/.ssh/id_rsa_github_work
```

### 3. **配置 SSH 配置文件**
编辑或创建 `~/.ssh/config` 文件，为每个 GitHub 账号配置不同的主机别名：
```bash
# Personal account
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github_personal

# Work account
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github_work
```

### 4. **克隆和推送代码**
使用配置的主机别名来克隆或推送代码：
```bash
git clone git@github-personal:username/repository.git
git clone git@github-work:username/repository.git
```
这样，GitHub 将会根据你使用的别名选择正确的 SSH 密钥。

### 5. **在 Git 操作中使用不同的账号**
在仓库的 `git config` 中设置特定的用户名和邮箱：
```bash
cd path/to/repository
git config user.name "Personal Name"
git config user.email "email@example.com"

git config user.name "Work Name"
git config user.email "work@example.com"
```

通过这种方式，你可以灵活地管理多个 GitHub 账户，并确保在不同的项目中使用不同的 SSH 密钥。
