# 本质是一个学习日志

感谢 [Taeyoung96](https://github.com/Taeyoung96/Troubleshooting-Note) 的仓库给我的启发。  
这个项目让我开始系统地记录我在学习、开发、或者使用 AI 过程中遇到的问题和解决方案。

我暂时没有博客，这个仓库就是我的问题记录中心。  
我希望帮助那些和我相似的**笨蛋**更容易的从网上/AI学习知识  
这里将会逐步记录我**蒸馏**出的知识。  
如果题目很大的话我会单独开一个`.md`

**不定期更新**

---

## 记录格式

🔑 **关键词**:  
⚠️ **问题出现**:  
✅ **解决方案**:  
📚 **出处**:  

---

🔑 **关键词**: `.md` 怎么换行  
⚠️ **问题出现**: 我在 `README` 使用 “段落之间空一行” 换行的时候，段落之间总是空一行。  
✅ **解决方案**: 在句末使用 `<br>` 或在行尾加两个空格。  
📚 **出处**: [GitHub Flavored Markdown Spec](https://github.github.com/gfm/#paragraphs)

---

🔑 **关键词**: `.md` 怎么将文字标黑只有鼠标放上去才显示  
⚠️ **问题出现**: 想在 `README` 里写一点 `████████`。  
✅ **解决方案**: Markdown 本身不支持这种交互效果。我找到两种别的办法：  

<details>
  <summary>1. 鼠标悬停提示: <span title="我其实在吐槽">这句话表面很冷静</span></summary>

  ```html
  <span title="我其实在吐槽">这句话表面很冷静</span>。
  ```
</details>

<details>
  <summary>2. 用&lt;details&gt;标签</summary>
  
  ```html
  <details>
    <summary>标题</summary>
    被遮住的内容在这里。
  </details>
  ```
</details>

📚 **出处**: [GPT]

---

🔑 **关键词**: `.md` 怎么将 ``` 显示出来  
⚠️ **问题出现**: Markdown 内嵌代码块时想显示反引号。  
✅ **解决方案**:  
* 直接使用更多数量的反引号，例如外层 `~~~~` 包裹内层 ```。
* 或者使用 HTML 实体：`&#96;&#96;&#96;`

📚 **出处**: [GitHub Docs – Writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

🔑 **关键词**: `.md` 怎么正常显示 `<`、`>`、`特殊符号`  
⚠️ **问题出现**: 在 README 里直接写 `<details>`、`<div>` 时会被当作 HTML 解析。  
✅ **解决方案**: 使用 HTML 实体转义：  `<` → `&lt;` 、 `>` → `&gt;`  
📚 **出处**: [GitHub Flavored Markdown Spec – HTML blocks](https://github.github.com/gfm/#html-blocks)

---

🔑 **关键词**: `.md` 在 `<details>` 里显示代码块  
⚠️ **问题出现**: 在 `<details>` 标签里写 ``` 的代码块时，渲染失败或代码不显示。  
✅ **解决方案**: 最简单的做法是在 `last line` 标签和代码块之间**空一行**。  
📚 **出处**: [GitHub Flavored Markdown Spec – HTML blocks](https://github.github.com/gfm/#html-blocks)

---

🔑 **关键词**: `.md` 显示三个反引号 ```  
⚠️ **问题出现**: 想在 Markdown 中显示 ``` 但被识别为代码块起止符。  
✅ **解决方案**: 外层使用更多反引号（如 `~~~~` 包裹 ```），或使用 HTML 实体 `&#96;&#96;&#96;`。  
📚 **出处**: [GitHub Docs – Writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

🔑 **关键词**: Ubuntu 24 安装 Docker（NO_PUBKEY 错误）  
⚠️ **问题出现**: 使用 `get.docker.com` 脚本报 “NO_PUBKEY”，无法安装。  
✅ **解决方案**: 使用官方 APT 源 + GPG keyring 方式添加并安装 Docker。  
📚 **出处**: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

---

🔑 **关键词**: 安装 `livox_ros_driver2` on Ubuntu 24.04 + ROS 2 Jazzy  
⚠️ **问题出现**: 官方推荐 Foxy/Humble；在 Jazzy 上出现缺少 `package.xml`、接口路径/SDK 兼容性报错。  
✅ **解决方案**: 先本地编译并安装 Livox-SDK2，然后在工作区构建 `livox_ros_driver2`（复制 `package_ROS2.xml` 为 `package.xml`，`colcon build --cmake-args -DROS_EDITION=ROS2 -DCMAKE_BUILD_TYPE=Release -DHUMBLE_ROS=humble`）。  
📚 **出处**: <https://github.com/Livox-SDK/livox_ros_driver2/issues/131>

---

🔑 **关键词**: sudo 临时免密码（延长验证缓存）  
⚠️ **问题出现**: 开发过程中频繁输入 `sudo` 密码影响效率。  
✅ **解决方案**: 在 `/etc/sudoers.d/` 为当前用户设置 `timestamp_timeout`（例如 60 分钟），并用 `visudo -c` 校验。  
📚 **出处**: `man sudoers`（`timestamp_timeout`）

---

🔑 **关键词**: 创建 ROS 2 Python package（ament_python）  
⚠️ **问题出现**: 新建后 `ros2 run` 找不到或导入失败，忘了把目录标记为 Python 包。  
✅ **解决方案**: 在包的 Python 目录下**务必包含** `__init__.py`（即使为空），并在 `setup.py` 的 `entry_points` 注册可执行入口；构建时可用 `--symlink-install` 加速开发。  
📚 **出处**: ROS 2 ament_python 模板 / 实践

---

🔑 **关键词**: ROS 2 Dummy Node（模拟 D455 深度点云）  
⚠️ **问题出现**: 设备不在身边但需要点云输入调试。  
✅ **解决方案**: 用 `rclpy` 创建发布 `sensor_msgs/PointCloud2` 的节点；点字段含 `x,y,z,intensity,rgb`，在 RViz 选择 `RGB8` 查看彩色轴向参考。  
📚 **出处**: 自建示例 / 实践

---

🔑 **关键词**: RViz “Missing transform”  
⚠️ **问题出现**: 显示点云时报缺少 TF（如 `map -> camera_link`）。  
✅ **解决方案**: 使用 `static_transform_publisher` 发布静态 TF；或在节点内广播合适的父子坐标系。  
📚 **出处**: ROS 2 TF2 实践

---

🔑 **关键词**: `static_transform_publisher` 新式参数  
⚠️ **问题出现**: 旧式参数调用提示 “Old-style arguments are deprecated”。  
✅ **解决方案**: 使用新式命名参数：`--x --y --z --roll --pitch --yaw --frame-id --child-frame-id`。  
📚 **出处**: ROS 2 TF2 文档 / CLI 帮助

---

🔑 **关键词**: `camera_link` vs `camera_depth_optical_frame`  
⚠️ **问题出现**: 点云方向与相机直觉不一致，难以判断“相机向前”。  
✅ **解决方案**: 光学系采用 `x 右、y 下、z 前`，与成像/深度投影一致；若以 `map` 固定，添加 `map -> camera_depth_optical_frame`（或 `camera_link -> camera_depth_optical_frame`）的静态 TF。  
📚 **出处**: ROS REP-103 / Intel RealSense 坐标系约定

---

🔑 **关键词**: `ip -a` 无效  
⚠️ **问题出现**: 在 Ubuntu 中运行 `ip -a` 无效。  
✅ **解决方案**: 正确命令是 `ip a` 或 `ip addr`；常用 `ip link`、`ip route` 查看接口与路由。  
📚 **出处**: `iproute2` 常用命令

---

🔑 **关键词**: `--symlink-install` 是什么  
⚠️ **问题出现**: Python 包每次改源码都要重建，效率低。  
✅ **解决方案**: `colcon build --symlink-install` 以符号链接安装，修改 Python 源码后通常无需重建（改 `setup.py`/`package.xml` 仍需重建并 `source`）。  
📚 **出处**: colcon 文档 / 实践

---

🔑 **关键词**: `setup.py` 构建报错 `NameError: name 'dummy_camera' is not defined`  
⚠️ **问题出现**: 构建 `ament_python` 包时报该错误。  
✅ **解决方案**: `setup.py` 中 `packages=[...]` 应写为包名字符串或变量（如 `packages=[package_name]` 或 `['dummy_camera']`），而不是未定义的变量名。  
📚 **出处**: Python setuptools 规则 / 实践

---

🔑 **关键词**: 运行时报 `PackageNotFoundError: dummy-camera`  
⚠️ **问题出现**: `ros2 run` 时入口脚本已生成但发行 metadata 未被找到。  
✅ **解决方案**: 修改了 `setup.py`/`package.xml` 后需要重建并 `source`；确认存在 `__init__.py`、`resource/<pkg>`、以及安装产物 `*.dist-info`。  
📚 **出处**: ament_python 打包流程 / 实践

---

🔑 **关键词**: PointCloud2 字段解释  
⚠️ **问题出现**: 不清楚 `fields/point_step/row_step/data` 的含义与对齐。  
✅ **解决方案**: `fields` 定义每点结构（如 `x,y,z,intensity,rgb`）；`point_step`=每点字节数；`row_step`=每行字节数；`data`=二进制拼接；`is_dense` 标示是否含 NaN。  
📚 **出处**: `sensor_msgs/PointCloud2` 消息定义

---

🔑 **关键词**: 深度点云“长方体”而非“相机视角”  
⚠️ **问题出现**: 用均匀随机 `x,y,z` 采样导致点云像盒子，不像相机看到的世界。  
✅ **解决方案**: 使用相机内参将 `(u,v,depth)` 投影到 3D：`x=(u-cx)/fx*z`，`y=(v-cy)/fy*z`，`z=depth`；建议使用 `camera_depth_optical_frame`。  
📚 **出处**: 相机针孔模型 / RealSense 投影公式

---

🔑 **关键词**: `Unknown license 'TODO: License declaration'` 警告  
⚠️ **问题出现**: 构建包时出现许可证占位符警告。  
✅ **解决方案**: 将 `package.xml` 中 `<license>` 改为实际许可（如 `MIT`），并在包根目录添加 `LICENSE` 文件。  
📚 **出处**: ROS 2 包规范 / 实践

---

🔑 **关键词**: `AutoDesk Fusion` 登陆验证收不到邮件   
⚠️ **问题出现**: 我用学校邮箱注册了一个账号自动验证了学生Access，但是安装好了就提示我"最近更换过邮箱，需要邮箱链接验证" ，但是收不到邮件  
✅ **解决方案**: 自己注册一个新账号 加入老账号的`team`，然后将老账号的`Setting -> User Managment` 中的 自己的`Fusion Access` 关闭并且 `Assign` 给 新账号  
📚 **出处**: [Difficulty with Changing Autodesk Registration Email - New Email Associated with BIM360. Reddit.](https://www.reddit.com/r/AutoCAD/comments/1hcpx4m/difficulty_with_changing_autodesk_registration/)  

---

🔑 **关键词**: Jetson Orin Nano 开机失败、syslog 爆满、Chromium 崩溃、PackageKit 死循环  
⚠️ **问题出现**:  
我在 Jetson Orin Nano（2TB SSD）上开发时突然弹窗提示系统磁盘已满。我尝试手动删除 `/var/log` 下的日志文件，但巨型 `syslog` 无法正常删除。没有继续排查，我直接重启，结果系统无法进入桌面，也无法正常启动。

最终发现根因是 **syslog 被疯狂写入到几十 GB**，导致根分区被写满，使得 Jetson 在重启时直接挂掉。

问题由以下已知 Jetson bug 引发：

* Chromium（snap 版本）在 Jetson 上存在 zygote 错误，会 **狂刷 syslog**

* PackageKit / update-notifier 长时间循环查询更新

* 系统默认 logrotate **没有限制 syslog 最大体积**

* Jetson 官方已承认 Chromium + PackageKit 触发崩溃

✅ **解决方案**:  

<details>
  <summary>1. 在其他 Linux 机器中挂载 Jetson SSD，并找到巨型 syslog</summary>

使用 ls 查看日志：

```
ls -lh /media/xxx/ROOTFS/var/log
```

你会看到 `syslog` 体积达到 **20GB～80GB**。

</details>

<details>
  <summary>2. 删除损坏或过大的 syslog，并重建空日志文件</summary>

```
sudo rm /media/.../var/log/syslog
sudo touch /media/.../var/log/syslog
sudo chown syslog:adm /media/.../var/log/syslog
sudo chmod 640 /media/.../var/log/syslog
```

</details>

<details>
  <summary>3. 修复 logrotate，限制 syslog 最大体积（强制）</summary>

编辑：

```
/etc/logrotate.d/rsyslog
```

添加：

```
size 100M
rotate 4
compress
```

这样 syslog 永远不会无限膨胀。

</details>

<details>
  <summary>4. 禁用 Jetson 上最常导致 syslog 爆炸的服务（PackageKit / Apport / Update Notifier）</summary>

```
sudo systemctl disable --now packagekit.service
sudo systemctl disable --now packagekit-offline-update.service
sudo systemctl disable --now update-notifier.service
sudo systemctl disable --now update-notifier-crash.service
sudo systemctl disable --now apport.service
sudo systemctl mask apport.service
```

这些服务会在 Jetson（特别是 Ubuntu 22.04 + JetPack 6）中反复报错并写 log。

</details>

<details>
  <summary>5. 卸载 Jetson 上已知会引发 syslog 风暴的 Chromium（官方确认）</summary>

```
sudo snap remove chromium
```

原因：在 Jetson Orin 上 Chromium 频繁出现：

* `zygote_linux.cc` 错误
* 权限 setcap 失败
* 内部 crash → syslog 疯狂刷屏

官方建议 Jetson 使用 Firefox，而不是 Chromium。

</details>

<details>
  <summary>6. 弹出 SSD、装回 Jetson，系统成功恢复开机</summary>

清理 syslog＋禁用问题服务后，系统顺利恢复正常运行。

</details>

---

📚 **出处**:

* [syslog 爆炸导致 Ubuntu 系统崩溃](https://askubuntu.com/questions/1103137/huge-syslog-file-crashing-system)
* [zygote error 导致 Linux syslog 被写满](https://www.reddit.com/r/discordapp/comments/1o55chc/zygote_linuxcc_error_filling_syslog/)
* [Jetson 官方确认：Chromium 在 Orin 上突然坏掉并写爆系统](https://jetsonhacks.com/2025/07/12/why-chromium-suddenly-broke-on-jetson-orin-and-how-to-bring-it-back/#:~:text=Here%20is%20the%20NVIDIA%20Jetson,set%20capabilities:%20Operation%20not%20permitted)

---

🔑 **关键词**: iTerm2 Cmd+点击文件路径用 VS Code 打开而非 Xcode

⚠️ **问题出现**: 在 iTerm2 中 Cmd+点击 Claude Code 输出的文件路径（如 `docs/research_summary.md`），默认用 Xcode 打开而非 VS Code，因为 macOS 将 `.md` 等文件类型关联到了 Xcode。

✅ **解决方案**: 在 iTerm2 中配置 Semantic History：
- **Preferences (Cmd+,) → Profiles → Advanced** → 滚到底部找到 **Semantic History**
- 下拉选择 **"Run command..."**
- 填入: `/usr/local/bin/code --goto \1:\2`
- 其中 `\1` 是 iTerm2 自动替换的文件路径，`\2` 是行号（如路径含 `:42` 格式），`--goto` 让 VS Code 打开并跳转到指定行

💡 **额外推荐**: 在 VS Code `settings.json` 中加入以下配置，让 `.md` 文件默认以预览模式打开：
```json
"workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
}
```

📚 **出处**: [Claude]

💡 **额外排查**: 如果配置正确但 Cmd+Click 仍不生效（尤其是相对路径如 `docs/xxx.md`），检查 iTerm2 Shell Integration 是否安装。没有 shell integration，iTerm2 无法获取终端的当前工作目录（CWD），无法将相对路径解析为绝对路径。

诊断：
- 检查文件是否存在: `ls ~/.iterm2_shell_integration.zsh`
- 检查 `.zshrc` 是否 source 了它: `grep iterm2_shell_integration ~/.zshrc`

修复：
```bash
curl -L https://iterm2.com/shell_integration/zsh -o ~/.iterm2_shell_integration.zsh
echo 'source ~/.iterm2_shell_integration.zsh' >> ~/.zshrc
source ~/.iterm2_shell_integration.zsh
```
或通过菜单: **iTerm2 → Install Shell Integration**

📚 **出处**: [Claude]

---

🔑 **关键词**: Vast.ai SSH Key 团队共享限制
⚠️ **问题出现**: 在 Vast.ai 租用 GPU 服务器后，SSH Key 只能通过个人账户在网页端上传。团队成员无法共享已上传的 SSH Key，每个人需要各自手动设置。
✅ **解决方案**: 每位团队成员需登录自己的 Vast.ai 账户，在网页端 **Account → SSH Keys** 单独上传自己的公钥。或者在实例启动后，手动将团队成员的公钥追加到 `~/.ssh/authorized_keys`：
```bash
# 在已启动的实例上执行
echo "ssh-ed25519 AAAA... teammate@email" >> ~/.ssh/authorized_keys
```
📚 **出处**: [实践经验]

---

🔑 **关键词**: macOS diskutil 格式化外接硬盘为 exFAT (Linux/Mac 通用)
⚠️ **问题出现**: 需要将 NTFS 格式的 6TB 外接硬盘格式化为 Linux 和 macOS 都能原生读写的格式
✅ **解决方案**:
<details><summary>diskutil 格式化流程</summary>

1. 确认磁盘编号：`diskutil list`
2. 卸载磁盘：`diskutil unmountDisk /dev/diskN`
3. 格式化为 exFAT：`diskutil eraseDisk ExFAT 卷名 GPT /dev/diskN`
4. 验证：`diskutil info /dev/diskNs2`

选 exFAT 是因为 Mac 和 Linux 都原生读写，无需额外驱动。GPT 分区表是现代标准。

</details>

📚 **出处**: [Apple diskutil man page](https://ss64.com/mac/diskutil.html) / [Claude]

---

🔑 **关键词**: diskutil rename 外接硬盘改名, exFAT 卷名限制
⚠️ **问题出现**: `diskutil rename` 改名时报 `does not appear to be a valid volume name`，原因是名字含下划线 `_` 等特殊字符
✅ **解决方案**: exFAT 卷名避免特殊字符（下划线、空格等），使用纯字母数字组合。命令：`diskutil rename /Volumes/旧名 "新名"`
📚 **出处**: [Claude]

---

🔑 **关键词**: tar 打包大文件夹到外接硬盘, macOS COPYFILE_DISABLE, zstd 并行压缩
⚠️ **问题出现**: Finder 拖拽大量小文件（如 H36M 数据集）到外接硬盘极慢（预估 3 小时），需要更快的方式
✅ **解决方案**:
<details><summary>三种 tar 方案</summary>

**不压缩（最快，本地传输用）：**
```bash
COPYFILE_DISABLE=1 tar cf /Volumes/Disk/H36M.tar -C /path/to Downloads H36M
```

**gzip 压缩（通用）：**
```bash
COPYFILE_DISABLE=1 tar czf /Volumes/Disk/H36M.tar.gz -C /path/to Downloads H36M
```

**zstd 压缩（推荐，速度快 3-5x）：**
```bash
brew install zstd
COPYFILE_DISABLE=1 tar --use-compress-program='zstd -T0' -cf /Volumes/Disk/H36M.tar.zst -C /path/to Downloads H36M
```

- `COPYFILE_DISABLE=1` 防止 macOS 塞 `._` 垃圾文件（Linux 解压会出问题）
- `-T0` 用所有 CPU 核心并行压缩
- 加 `-v` 看逐文件进度

</details>

📚 **出处**: [GNU tar manual](https://www.gnu.org/software/tar/manual/) / [Zstandard](https://facebook.github.io/zstd/) / [Claude]

---

🔑 **关键词**: rsync 暂停/恢复/续传, SIGSTOP/SIGCONT
⚠️ **问题出现**: rsync 大量文件传输到 HDD 过程中需要暂停（如检查 USB 口速度）
✅ **解决方案**:
- 暂停：`pkill -STOP rsync`（SIGSTOP，进程冻结但不退出）
- 恢复：`kill -CONT $(pgrep rsync)`
- 彻底停掉：`kill $(pgrep rsync)`，重跑同一条 rsync 命令会**跳过已传完的文件**自动续传
📚 **出处**: [rsync man page](https://download.samba.org/pub/rsync/rsync.1) / [Claude]

---

🔑 **关键词**: USB 传输速度慢, HDD 实际写入 vs 接口速度, system_profiler 检测 USB 版本
⚠️ **问题出现**: WD Elements 6TB 标称 10 Gbps (USB 3.2 Gen 2)，实测 rsync 只有 ~29 MB/s，疑似降到 USB 2.0
✅ **解决方案**:
- 接口速度 ≠ 盘速度：机械盘实际写入 100-150 MB/s，但 29 MB/s 说明可能是 USB 2.0 (480 Mbps ≈ 35 MB/s 上限)
- 检测命令：`system_profiler SPUSBDataType 2>/dev/null | grep -A5 "Elements"`，看 Speed 行
- `Up to 5 Gb/s` = USB 3.0 ✅ | `Up to 480 Mb/s` = USB 2.0 ❌
- 解决：直插 Mac USB-C/Thunderbolt 口，避免劣质 hub/转接头降速
📚 **出处**: [Apple Support - USB](https://support.apple.com/en-us/102567) / [Claude]

---
