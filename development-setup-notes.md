# Mac Python 开发环境配置笔记：GitHub + Git + PyCharm

> 适用环境：macOS + PyCharm + Python 3.13 + GitHub  
> 当前练习仓库：`python-learning`  
> 本地项目路径：`~/Projects/python-learning`  
> 当前虚拟环境：`~/Projects/python-learning/.venv`

---

## 一、整体认识：这些工具分别做什么？

| 工具 | 用途 |
|---|---|
| GitHub | 在线托管代码，展示项目，与他人协作 |
| Git | 记录代码变化，提交、回退和同步代码 |
| Terminal（终端） | 通过命令操作电脑、运行程序 |
| Python | 编写和运行 Python 程序 |
| PyCharm | 编写代码、调试程序、管理 Python 环境 |
| Interpreter（解释器） | 真正负责执行 Python 代码的程序 |
| Virtualenv / `.venv` | 为每个项目隔离 Python 依赖 |
| Token | 用于身份认证，不同平台的 Token 用途不同 |

简单理解：

**PyCharm 负责写代码，Python 负责运行代码，Git 负责记录版本，GitHub 负责在线保存代码。**

## 二、创建 GitHub 账户和仓库

### 2.1 创建 GitHub 账户

1. 打开 https://github.com/
2. 注册账户并完成邮箱验证。
3. 记住自己的 GitHub 用户名。
4. 登录后即可创建仓库、查看代码和管理项目。

当前练习账户对应的仓库：

- 用户名：`zap712x`
- 仓库名称：`python-learning`
- 仓库地址：https://github.com/zap712x/python-learning

### 2.2 创建仓库

1. 登录 GitHub。
2. 点击右上角的 `+`，选择 `New repository`。
3. 输入仓库名称，例如 `python-learning`。
4. 选择 `Public` 或 `Private`。
   - Public：其他人可以查看代码。
   - Private：只有获得授权的人可以查看。
5. 点击 `Create repository`。

如果本地已经有项目，并计划将它推送到新仓库，注意本地与远程仓库的初始化方式需要相互匹配，避免重复初始化造成冲突。

### 2.3 Git 和 GitHub 的区别

Git 是本地的版本管理工具；GitHub 是托管 Git 仓库的在线服务。

即使没有网络，也可以在本地使用 Git 提交代码。但要把代码同步到 GitHub，通常需要网络连接和相应的认证权限。

---

## 三、Mac 如何打开命令行

### 3.1 最快捷的方式

在 Mac 键盘上按：

`Command (⌘) + Space`

这会打开 Spotlight 搜索。

然后输入：

`Terminal`

按回车，即可打开终端。

### 3.2 在 PyCharm 中打开终端

在 PyCharm 中，可以通过菜单 `View → Tool Windows → Terminal` 打开内置终端。

不同版本的菜单位置可能略有不同。

### 3.3 常用终端命令

| 命令 | 用途 |
|---|---|
| `pwd` | 显示当前所在目录 |
| `ls` | 查看当前目录下的文件 |
| `cd 文件夹名` | 进入指定文件夹 |
| `cd ..` | 返回上一级目录 |
| `cd ~` | 回到用户主目录 |
| `mkdir 项目名` | 创建文件夹 |
| `clear` | 清空终端显示 |
| `python3 --version` | 查看 Python 版本 |
| `git --version` | 查看 Git 版本 |

注意：终端中输入的命令通常需要按回车执行。

### 3.4 进入自己的项目目录

```bash
cd ~/Projects/python-learning
```

查看当前目录：

```bash
pwd
```

查看文件：

```bash
ls -la
```

---

## 四、检查和配置 Git

### 4.1 检查 Git 是否安装

在终端执行：

```bash
git --version
```

当前 Mac 已成功识别 Git，版本为：

```text
git version 2.50.1 (Apple Git-155)
```

macOS 自带的 Git 已经可以使用，不需要为了开发专门下载 Linux 版本的 Git。

### 4.2 配置 Git 提交身份

Git 提交时需要记录提交者的名字和邮箱。

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

例如：

```bash
git config --global user.name "Developer"
git config --global user.email "your-email@example.com"
```

上面的名字和邮箱只是示例，请替换成自己的信息。

查看配置：

```bash
git config --global --list
```

注意：Git 的 `user.name` 和 `user.email` 主要用于提交记录，不等于 GitHub 登录认证信息。

---

## 五、GitHub Token 与身份认证

### 5.1 Token 是什么？

当通过 HTTPS 使用 Git 操作 GitHub 时，可能需要身份认证。

GitHub Personal Access Token（个人访问令牌，简称 PAT）可以在相应场景中代替账户密码进行认证。

它不是普通密码，也不是用来直接运行 Python 程序的代码。

官方文档：

https://docs.github.com/zh/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens

### 5.2 如何创建 Token

如果确实需要手动创建：

1. 登录 GitHub。
2. 进入 `Settings`。
3. 找到 `Developer settings`。
4. 进入 `Personal access tokens`。
5. 选择 `Fine-grained tokens`。
6. 点击生成新 Token。
7. 设置有效期，并只授予完成任务所需的最小权限。
8. 如果需要操作自己的仓库，选择对应的仓库并设置必要权限。
9. 创建后立即安全保存。

对于推送代码，通常需要允许目标仓库的内容写入；实际权限应根据使用场景确定。

### 5.3 如何使用 Token

使用 HTTPS 进行 Git 操作时，如果终端要求输入用户名和密码：

- Username：填写 GitHub 用户名。
- Password：在需要 PAT 的认证流程中填写 Token，而不是 GitHub 登录密码。

某些客户端会通过浏览器或系统钥匙串完成认证，因此不一定每次都要求手动输入 Token。

**安全提醒：**

- 不要把 Token 发给别人。
- 不要把 Token 写进 Python 源代码。
- 不要把 Token 提交到 GitHub。
- 不要把真实 Token 保存到公开笔记里。
- 如果 Token 泄露，应尽快撤销并重新生成。

GitHub 也支持 GitHub CLI、SSH 等其他认证方式。

### 5.4 GitHub Token 和 OpenAI API Key 不一样

| 凭证 | 用途 |
|---|---|
| GitHub Token | 认证 GitHub 操作或访问相应资源 |
| OpenAI API Key | 让应用程序认证并调用 OpenAI API |

这两个凭证不能互相替代。后续学习 OpenAI 项目时，如果需要 API Key，应单独配置，并注意 API 使用可能产生费用。

---

## 六、在 PyCharm 中打开项目

### 6.1 打开已有项目

1. 打开 PyCharm。
2. 选择 `File → Open`。
3. 选择本地项目文件夹。
4. 例如：

```text
/Users/imac/Projects/python-learning
```

5. 打开项目后，左侧 Project 面板可以查看文件。

当前项目中已经有：

```text
python-learning/
├── .venv/
├── hello.py
└── README.md
```

其中：

- `.venv/`：Python 虚拟环境。
- `hello.py`：练习 Python 的文件。
- `README.md`：项目说明文档。

### 6.2 运行 Python 程序

`hello.py` 中的代码：

```python
print("Hello, GitHub!")
```

在 PyCharm 中打开该文件，点击运行按钮，即可执行代码。

当前已经成功运行，并输出：

```text
Hello, GitHub!
```

说明 Python 解释器已经可以正常执行程序。

---

## 七、Python 解释器和虚拟环境

### 7.1 什么是 Python 解释器？

Python 解释器负责执行 Python 代码。

本机已安装 Python 3.13.16，基础解释器路径为：

```text
/usr/local/bin/python3.13
```

查看版本：

```bash
python3 --version
```

如果需要确认实际执行的 Python 路径，可以执行：

```bash
which python3
```

注意：`which python3` 显示的是当前终端环境中找到的 `python3` 路径；它不一定与 PyCharm 项目所选择的解释器相同。

### 7.2 什么是虚拟环境 `.venv`？

虚拟环境可以理解为某个 Python 项目的独立运行环境。

例如：

- 项目 A 需要某个版本的依赖包。
- 项目 B 需要另一个版本的依赖包。
- 两个项目可以各自管理依赖，不必全部安装到同一个全局 Python 环境中。

`.venv` 目录保存该项目虚拟环境的相关文件。

**每个项目可以有自己的虚拟环境。**

### 7.3 在 PyCharm 中创建虚拟环境

操作步骤：

1. 打开项目。
2. 进入 `Settings` 或 `Preferences`。
3. 找到 `Python → Interpreter`。
4. 选择 `Add Interpreter`。
5. 选择 `Add Local Interpreter`，然后选择 `Virtualenv`。
6. 选择基础 Python 解释器。
7. 将虚拟环境位置设为项目目录下的 `.venv`。
8. 不勾选 `Inherit packages from base interpreter`。
9. 不勾选 `Make available to all projects`。
10. 点击 `OK`。

不同 PyCharm 版本的界面文字可能有所不同。

官方文档：

https://www.jetbrains.com/help/pycharm/configuring-python-interpreter.html

### 7.4 当前项目的解释器配置

当前已成功配置：

```text
项目路径：
~/Projects/python-learning

基础解释器：
/usr/local/bin/python3.13

虚拟环境：
~/Projects/python-learning/.venv

项目解释器：
~/Projects/python-learning/.venv/bin/python
```

PyCharm 底部显示：

```text
Python 3.13 (python-learning)
```

这表示项目使用自己的虚拟环境。

### 7.5 如何在终端中创建虚拟环境

如果以后不使用 PyCharm 自动创建，也可以通过终端执行：

```bash
cd ~/Projects/python-learning
python3 -m venv .venv
```

激活虚拟环境：

```bash
source .venv/bin/activate
```

激活后，终端提示符通常会出现：

```text
(.venv)
```

检查当前 Python：

```bash
which python
python --version
```

退出虚拟环境：

```bash
deactivate
```

如果虚拟环境已经存在，不要重复执行创建命令；直接激活即可。

### 7.6 安装 Python 依赖包

在虚拟环境激活后，可以使用：

```bash
python -m pip install requests
```

检查已安装的包：

```bash
python -m pip list
```

查看当前 Python 对应的 pip：

```bash
python -m pip --version
```

这里使用 `python -m pip`，可以减少误把依赖装进其他 Python 环境的风险。

如果项目包含 `requirements.txt`，通常可以安装文件中声明的依赖：

```bash
python -m pip install -r requirements.txt
```

请先确认当前目录下确实有该文件，再运行命令。

---

## 八、Git 仓库的基本操作

### 8.1 Git 工作流程

一般流程是：

1. 修改或新增代码。
2. 查看哪些文件发生了变化。
3. 把需要保存的变化放入暂存区。
4. 创建一次提交。
5. 将提交推送到 GitHub。

### 8.2 常用命令

查看当前状态：

```bash
git status
```

查看文件变化：

```bash
git diff
```

将指定文件放入暂存区：

```bash
git add hello.py
```

将所有未忽略的变化放入暂存区：

```bash
git add .
```

创建提交：

```bash
git commit -m "Update Python practice"
```

查看提交历史：

```bash
git log --oneline
```

推送到 GitHub：

```bash
git push
```

获取远程更新：

```bash
git pull
```

首次关联远程仓库时，可能需要设置远程地址和分支。不要在已经配置好的仓库中重复执行初始化操作。

### 8.3 如果从零开始创建本地 Git 仓库

以下命令只适用于尚未初始化 Git 的新项目：

```bash
mkdir my-python-project
cd my-python-project
git init
```

创建文件后：

```bash
git add .
git commit -m "Initial commit"
```

接着，在 GitHub 网站创建对应的空仓库，并按照 GitHub 页面提供的说明关联远程仓库。

例如，远程地址的形式为：

```bash
git remote add origin https://github.com/你的用户名/你的仓库名.git
```

如果默认分支使用 `main`，可以执行：

```bash
git branch -M main
git push -u origin main
```

如果本地已经有 Git 仓库，先使用 `git status` 和 `git remote -v` 检查状态，不要盲目再次执行 `git init` 或添加 `origin`。

---

## 九、`.gitignore`：哪些文件不应该上传？

Python 项目一般不需要把虚拟环境目录提交到 GitHub。

在项目根目录创建或编辑 `.gitignore`，可以添加：

```gitignore
# Python virtual environment
.venv/
venv/

# Python cache
__pycache__/
*.py[cod]

# Environment variables and secrets
.env

# IDE settings
.idea/
```

说明：

- `.venv/`：本地虚拟环境，不需要上传。
- `__pycache__/`：Python 自动生成的缓存。
- `.env`：可能存放 API Key 等敏感配置。
- `.idea/`：PyCharm 项目设置，通常不需要共享整个目录。

注意：`.gitignore` 只会忽略尚未被 Git 跟踪的文件。已经提交过的敏感文件需要另外处理。

如果以后需要在项目中使用 OpenAI API Key，应避免把真实密钥写进公开仓库。

---

## 十、网络代理（可选）

此前配置 GitHub 连接时，使用过本地代理：

```text
127.0.0.1:7897
```

当 Clash Verge 正在运行，并且本地代理端口确实是 `7897` 时，Git 可以配置为使用该 HTTP 代理：

```bash
git config --global http.proxy http://127.0.0.1:7897
git config --global https.proxy http://127.0.0.1:7897
```

查看配置：

```bash
git config --global --get http.proxy
git config --global --get https.proxy
```

如果以后不再使用该代理，或者端口发生变化，可以删除 Git 的全局代理配置：

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

注意：只有确认不再需要这两个代理配置时才执行删除命令。代理端口必须与当前代理软件实际设置一致。

---

## 十一、一个新 Python 项目的标准准备流程

以后拿到一个新的 Python 项目，可以按照以下顺序检查。

### 第一步：获取代码

- 从 GitHub 克隆仓库，或者下载项目文件。
- 在 PyCharm 中打开正确的项目目录。
- 先阅读 `README.md`。

### 第二步：检查项目结构

重点查看：

- `README.md`：项目介绍和运行说明。
- `requirements.txt` 或 `pyproject.toml`：依赖配置。
- `.gitignore`：需要忽略的文件。
- `.env.example`：环境变量示例（如果有）。
- 程序入口文件：例如 `main.py`、`app.py`。

### 第三步：配置解释器

- 确认本机有兼容的 Python 版本。
- 为当前项目创建或选择虚拟环境。
- 检查 PyCharm 是否使用正确的 `.venv`。

### 第四步：安装依赖

只有在了解项目的安装说明后，才执行相应的安装命令。

如果项目有 `requirements.txt`：

```bash
python -m pip install -r requirements.txt
```

### 第五步：配置必要的环境变量

如果项目需要 API Key 或其他密钥：

- 按项目文档配置。
- 不要将真实密钥提交到 GitHub。
- 不要把 `.env.example` 里的占位值误当成真实密钥。

### 第六步：运行并验证

- 按 README 中的说明运行。
- 阅读终端输出。
- 如果报错，先记录完整错误信息，再逐步定位。

### 第七步：记录修改并提交

```bash
git status
git add .
git commit -m "Describe your changes"
git push
```

---

## 十二、常用命令速查表

| 目的 | 命令 |
|---|---|
| 查看当前目录 | `pwd` |
| 查看目录内容 | `ls -la` |
| 进入项目目录 | `cd ~/Projects/python-learning` |
| 查看 Python 版本 | `python3 --version` |
| 查看 Git 版本 | `git --version` |
| 查看当前 Python 路径 | `which python` |
| 激活虚拟环境 | `source .venv/bin/activate` |
| 退出虚拟环境 | `deactivate` |
| 安装依赖 | `python -m pip install 包名` |
| 查看依赖 | `python -m pip list` |
| 查看 Git 状态 | `git status` |
| 暂存修改 | `git add .` |
| 创建提交 | `git commit -m "提交说明"` |
| 推送到 GitHub | `git push` |
| 获取远程更新 | `git pull` |

---

## 十三、当前完成情况

- [x] 安装并打开 PyCharm。
- [x] 确认 Mac 上可以使用 Git。
- [x] 配置 Git 的提交者信息。
- [x] 创建并使用 GitHub 仓库 `python-learning`。
- [x] 在本地创建 `hello.py` 和 `README.md`。
- [x] 将代码推送到 GitHub。
- [x] 创建项目专属 `.venv`。
- [x] 在 PyCharm 中选择 Python 3.13 项目解释器。
- [x] 成功运行 `hello.py`。
- [ ] 继续探索 OpenAI 的 `openai-quickstart-python` 项目。
- [ ] 学习项目依赖、环境变量和 API 调用。

### 官方参考文档

- GitHub Token 管理：https://docs.github.com/zh/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
- GitHub 认证方式：https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github
- PyCharm Python 解释器：https://www.jetbrains.com/help/pycharm/configuring-python-interpreter.html
- Python 虚拟环境：https://docs.python.org/3/library/venv.html
