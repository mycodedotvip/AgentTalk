在GitHub上创建一个新项目非常简单。以下是详细的步骤：

1. **登录GitHub账户**：
   打开 [GitHub](https://github.com) 并使用你的账号登录。如果没有账号，先注册一个。

2. **创建新仓库**：
   - 在右上角的加号 (`+`) 图标上，选择 **“New repository”**。
   - 或者直接访问 [创建新仓库页面](https://github.com/new)。

3. **填写项目信息**：
   - **Repository name（仓库名称）**：输入项目的名称，保持简洁易懂。
   - **Description（描述）**：可选，简单描述项目的内容或目标。
   - **Public or Private**：选择是公开项目（Public）还是私人项目（Private）。
   - **Initialize this repository with a README**：建议勾选此选项，创建仓库时生成一个初始的 `README.md` 文件，便于后续文档管理。

4. **添加.gitignore 和 License**（可选）：
   - `.gitignore` 文件可以选择合适的模板，比如 Java、Python、Node.js 等，过滤掉不需要上传的文件。
   - **License**：为项目选择适当的开源许可证。

5. **点击 “Create repository”**：
   点击 **“Create repository”** 完成创建。

6. **推送本地项目到GitHub**（可选）：
   如果你在本地已经有项目代码，可以按照以下命令将代码推送到刚创建的 GitHub 仓库中：

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/your-username/your-repository.git
   git push -u origin main
   ```

至此，你的GitHub新项目就创建并可以开始协作了！
