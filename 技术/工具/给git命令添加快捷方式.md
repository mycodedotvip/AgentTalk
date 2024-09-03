在 Git 中添加命令别名（alias）可以让你更快地执行常用的 Git 命令。以下是如何给 Git 命令添加别名的步骤：

### 1. **添加全局别名**
   你可以通过修改全局的 Git 配置文件（通常位于 `~/.gitconfig`）来添加别名。使用以下命令：
   ```bash
   git config --global alias.别名 'git 命令'
   ```
   例如，给 `git status` 添加一个简短的别名 `st`：
   ```bash
   git config --global alias.st 'status'
   ```
   现在你可以通过运行 `git st` 来查看仓库的状态。

### 2. **查看别名**
   如果你想查看当前配置的所有别名，可以运行：
   ```bash
   git config --get-regexp alias
   ```

### 3. **在配置文件中手动添加别名**
   你也可以直接编辑 `~/.gitconfig` 文件来添加别名。打开文件并在 `[alias]` 部分添加你的别名，例如：
   ```ini
   [alias]
       co = checkout
       br = branch
       ci = commit
       st = status
       lg = log --oneline --graph --decorate --all
   ```

### 4. **别名中包含复杂命令**
   如果你希望在别名中包含多个参数或复杂的命令，可以使用引号包围完整的命令。例如：
   ```bash
   git config --global alias.last 'log -1 HEAD'
   ```
   这个别名 `last` 会显示上一次提交的日志。

### 5. **使用 shell 命令作为 Git 别名**
   如果你需要在别名中使用 shell 命令，你可以使用 `!` 来指定 shell 命令。例如，清理未跟踪的文件和目录：
   ```bash
   git config --global alias.cleanup '!git clean -fd && git reset --hard'
   ```

### 6. **删除别名**
   如果你想删除某个别名，可以使用以下命令：
   ```bash
   git config --global --unset alias.别名
   ```
   例如，删除 `st` 别名：
   ```bash
   git config --global --unset alias.st
   ```

通过这些步骤，你可以自定义 Git 命令，使得日常使用更高效、更符合你的习惯。
