# WakaTime & GitHub 个人主页配置指南 🔮

为了让迷宫能够自动记录您（技术魔法师）投入在各维度魔法阵（不同编程语言）中的战斗时长，我们需要集成 WakaTime。

这份教程包含两部分：
1. **获取 WakaTime API 密钥**。
2. **将密钥配置到您的 GitHub 仓库的 Secret 宝物库中**。

---

## 阶段一：获得灵魂契约 (获取 WakaTime API Key)

1. 点击访问官方网站：[WakaTime](https://wakatime.com/)
2. 注册账号。如果可以，请直接选择 **"Continue with GitHub"** 快速登录。
3. 登录后，点击右上角的头像（您的个人资料），然后在下拉菜单中点击 **Settings**。
4. 在左侧菜单或主内容区寻找 **"Secret API Key"**（一串非常长且复杂的字符），这就是我们需要的东西。
   * 点击 `Copy` 将其复制到您的剪贴板中。
5. （可选）建议您同时在您的日常 IDE（如 VS Code, PyCharm, CLion, IDEA 等）的扩展商店里搜索并安装 `WakaTime` 插件，将这串 API Key 在本地也粘贴一份。这样它就会开始自动在后台记录您的编码时间。

---

## 阶段二：注入魔力至仓库 (配置 GitHub Actions Secrets)

既然我们在主页计划中生成了 `.github/workflows/wakatime.yml`，它需要权限去 WakaTime 那里偷偷帮您拉取数据。

1. 打开我们在 GitHub 上准备好的同名个人主页仓库（例如 `https://github.com/aoli789654/aoli789654`）。
2. 在仓库首界面的上方导航栏中，点击 ⚙️ **Settings**。
3. 在左侧的导航面板中向下滚动，找到 **Security** 部分，点击展开 **Secrets and variables**。
4. 在展开的子菜单中点击 **Actions**。
5. 在左上角的绿色按钮处，点击 **"New repository secret"**。
6. 在这一页您需要填写两个框：
   * **Name** (名称): 要求完全精准，请粘贴：`WAKATIME_API_KEY`
   * **Secret** (秘密值): 粘贴您在**阶段一**从 WakaTime 复制出来的那串长密码。
7. 点击绿色的 **"Add secret"** 按钮保存。

## 阶段三（可选项）：赋予 GitHub Token 权限以推送更新

由于我们的贪吃蛇和 WakaTime 自动化每天都需要提交代码到您的 README，仓库可能需要您的 GitHub Token。(大部分情况下 GitHub Actions 提供基础读写即可，但最好配置好)。

> 这个仓库默认配置即可，如果您发现 Action 失败并报没有写入权限的错：
> 请到此仓库 `Settings` -> `Actions` -> `General` -> 拖拽到最下方的 **Workflow permissions** -> 选择 **Read and write permissions** 并保存即可。

---

> [!NOTE]
> 您的 CI/CD 自动化会在您配置好 Secret 之后，在每天指定的时间（通常是夜间 0 点）自动触发。您也可以在 GitHub 界面的 `Actions` 选项卡里点击对应的 Workflow 并手动触发运行 (`Run workflow`) 来立刻查收您的经验值图形。
