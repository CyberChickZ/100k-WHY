# Essentially a Learning Log

Inspired by [Taeyoung96](https://github.com/Taeyoung96/Troubleshooting-Note)'s repo.  
This project is where I systematically document problems and solutions I encounter while learning, developing, or using AI.

I don't have a blog yet — this repo is my central troubleshooting hub.  
I hope it helps fellow **beginners** learn more easily from the internet and AI.  
Knowledge **distilled** from experience will be recorded here.  
Larger topics get their own `.md` file.

**Updated irregularly**

---

## Entry Format

🔑 **Keywords**:  
⚠️ **Problem**:  
✅ **Solution**:  
📚 **Source**:  

---

🔑 **Keywords**: How to add line breaks in `.md`  
⚠️ **Problem**: When using blank lines between paragraphs in `README`, there's always an extra empty line.  
✅ **Solution**: Use `<br>` at end of line, or add two trailing spaces.  
📚 **Source**: [GitHub Flavored Markdown Spec](https://github.github.com/gfm/#paragraphs)

---

🔑 **Keywords**: Hidden/spoiler text in `.md`  
⚠️ **Problem**: Wanted to create `████████` redacted text that reveals on hover.  
✅ **Solution**: Markdown doesn't natively support this. Two workarounds:

<details>
  <summary>1. Hover tooltip: <span title="secret message">this text looks normal</span></summary>

  ```html
  <span title="secret message">this text looks normal</span>
  ```
</details>

<details>
  <summary>2. Use &lt;details&gt; tag</summary>
  
  ```html
  <details>
    <summary>Title</summary>
    Hidden content goes here.
  </details>
  ```
</details>

📚 **Source**: [GPT]

---

🔑 **Keywords**: Display triple backticks ``` in `.md`  
⚠️ **Problem**: Need to show backticks inside a code block.  
✅ **Solution**:  
* Wrap with more backticks (e.g., `~~~~` around ```).
* Or use HTML entities: `&#96;&#96;&#96;`

📚 **Source**: [GitHub Docs – Writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

🔑 **Keywords**: Display `<`, `>`, special characters in `.md`  
⚠️ **Problem**: Writing `<details>`, `<div>` in README gets parsed as HTML.  
✅ **Solution**: Use HTML entity escaping: `<` → `&lt;`, `>` → `&gt;`  
📚 **Source**: [GitHub Flavored Markdown Spec – HTML blocks](https://github.github.com/gfm/#html-blocks)

---

🔑 **Keywords**: Code blocks inside `<details>` in `.md`  
⚠️ **Problem**: Code blocks with ``` inside `<details>` tags fail to render.  
✅ **Solution**: Add a **blank line** between the closing tag and the code block.  
📚 **Source**: [GitHub Flavored Markdown Spec – HTML blocks](https://github.github.com/gfm/#html-blocks)

---

🔑 **Keywords**: Display triple backticks ``` literally in `.md`  
⚠️ **Problem**: Triple backticks get interpreted as code fence delimiters.  
✅ **Solution**: Wrap with more backticks (e.g., `~~~~` around ```), or use HTML entities `&#96;&#96;&#96;`.  
📚 **Source**: [GitHub Docs – Writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

🔑 **Keywords**: Ubuntu 24 Docker install (NO_PUBKEY error)  
⚠️ **Problem**: `get.docker.com` script fails with "NO_PUBKEY" error.  
✅ **Solution**: Use the official APT source + GPG keyring method to add and install Docker.  
📚 **Source**: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

---

🔑 **Keywords**: Install `livox_ros_driver2` on Ubuntu 24.04 + ROS 2 Jazzy  
⚠️ **Problem**: Officially supports Foxy/Humble; on Jazzy, missing `package.xml`, interface path/SDK compatibility errors.  
✅ **Solution**: Build and install Livox-SDK2 locally first, then build `livox_ros_driver2` in workspace (copy `package_ROS2.xml` to `package.xml`, `colcon build --cmake-args -DROS_EDITION=ROS2 -DCMAKE_BUILD_TYPE=Release -DHUMBLE_ROS=humble`).  
📚 **Source**: <https://github.com/Livox-SDK/livox_ros_driver2/issues/131>

---

🔑 **Keywords**: Temporary passwordless sudo (extend auth cache)  
⚠️ **Problem**: Frequent `sudo` password prompts slow down development.  
✅ **Solution**: Set `timestamp_timeout` for the current user in `/etc/sudoers.d/` (e.g., 60 minutes), verify with `visudo -c`.  
📚 **Source**: `man sudoers` (`timestamp_timeout`)

---

🔑 **Keywords**: Create ROS 2 Python package (ament_python)  
⚠️ **Problem**: After creation, `ros2 run` can't find or import — forgot to mark directory as Python package.  
✅ **Solution**: Always include `__init__.py` in the package's Python directory (even if empty), register executable entry points in `setup.py`'s `entry_points`; use `--symlink-install` for faster dev iteration.  
📚 **Source**: ROS 2 ament_python template / practice

---

🔑 **Keywords**: ROS 2 Dummy Node (simulate D455 depth point cloud)  
⚠️ **Problem**: Device not available but need point cloud input for debugging.  
✅ **Solution**: Create an `rclpy` node publishing `sensor_msgs/PointCloud2` with fields `x,y,z,intensity,rgb`; view in RViz with `RGB8` color mode.  
📚 **Source**: Custom example / practice

---

🔑 **Keywords**: RViz "Missing transform"  
⚠️ **Problem**: Point cloud display reports missing TF (e.g., `map -> camera_link`).  
✅ **Solution**: Use `static_transform_publisher` to publish static TF; or broadcast appropriate parent-child frames within the node.  
📚 **Source**: ROS 2 TF2 practice

---

🔑 **Keywords**: `static_transform_publisher` new-style parameters  
⚠️ **Problem**: Old-style parameter call shows "Old-style arguments are deprecated".  
✅ **Solution**: Use new-style named parameters: `--x --y --z --roll --pitch --yaw --frame-id --child-frame-id`.  
📚 **Source**: ROS 2 TF2 docs / CLI help

---

🔑 **Keywords**: `camera_link` vs `camera_depth_optical_frame`  
⚠️ **Problem**: Point cloud orientation doesn't match camera intuition, hard to tell "camera forward".  
✅ **Solution**: Optical frame uses `x-right, y-down, z-forward`, consistent with imaging/depth projection; if using `map` as fixed frame, add static TF `map -> camera_depth_optical_frame` (or `camera_link -> camera_depth_optical_frame`).  
📚 **Source**: ROS REP-103 / Intel RealSense coordinate conventions

---

🔑 **Keywords**: `ip -a` doesn't work  
⚠️ **Problem**: Running `ip -a` on Ubuntu returns nothing useful.  
✅ **Solution**: Correct command is `ip a` or `ip addr`; use `ip link`, `ip route` for interfaces and routing.  
📚 **Source**: `iproute2` common commands

---

🔑 **Keywords**: What is `--symlink-install`  
⚠️ **Problem**: Python packages require rebuild after every source change, slow iteration.  
✅ **Solution**: `colcon build --symlink-install` installs via symlinks — Python source changes take effect without rebuild (still need rebuild + `source` after modifying `setup.py`/`package.xml`).  
📚 **Source**: colcon docs / practice

---

🔑 **Keywords**: `setup.py` build error `NameError: name 'dummy_camera' is not defined`  
⚠️ **Problem**: Building `ament_python` package throws this error.  
✅ **Solution**: `packages=[...]` in `setup.py` should use string or variable (e.g., `packages=[package_name]` or `['dummy_camera']`), not an undefined variable name.  
📚 **Source**: Python setuptools rules / practice

---

🔑 **Keywords**: Runtime `PackageNotFoundError: dummy-camera`  
⚠️ **Problem**: `ros2 run` fails — entry script exists but distribution metadata not found.  
✅ **Solution**: Rebuild and `source` after modifying `setup.py`/`package.xml`; verify `__init__.py`, `resource/<pkg>`, and `*.dist-info` install artifacts exist.  
📚 **Source**: ament_python packaging flow / practice

---

🔑 **Keywords**: PointCloud2 field explanation  
⚠️ **Problem**: Unclear about `fields/point_step/row_step/data` meaning and alignment.  
✅ **Solution**: `fields` defines per-point structure (e.g., `x,y,z,intensity,rgb`); `point_step` = bytes per point; `row_step` = bytes per row; `data` = binary concatenation; `is_dense` indicates whether NaN values exist.  
📚 **Source**: `sensor_msgs/PointCloud2` message definition

---

🔑 **Keywords**: Depth point cloud looks like a "box" instead of camera view  
⚠️ **Problem**: Uniform random `x,y,z` sampling makes point cloud look like a box, not a camera perspective.  
✅ **Solution**: Use camera intrinsics to project `(u,v,depth)` to 3D: `x=(u-cx)/fx*z`, `y=(v-cy)/fy*z`, `z=depth`; use `camera_depth_optical_frame`.  
📚 **Source**: Pinhole camera model / RealSense projection formulas

---

🔑 **Keywords**: `Unknown license 'TODO: License declaration'` warning  
⚠️ **Problem**: License placeholder warning during package build.  
✅ **Solution**: Change `<license>` in `package.xml` to an actual license (e.g., `MIT`), add a `LICENSE` file to package root.  
📚 **Source**: ROS 2 package spec / practice

---

🔑 **Keywords**: AutoDesk Fusion login verification email not received  
⚠️ **Problem**: Registered with school email (auto-verified student Access), but after install got "recently changed email, need email link verification" — email never arrives.  
✅ **Solution**: Register a new account, join the old account's `team`, then in old account's **Settings → User Management**, disable your own `Fusion Access` and `Assign` it to the new account.  
📚 **Source**: [Difficulty with Changing Autodesk Registration Email - Reddit](https://www.reddit.com/r/AutoCAD/comments/1hcpx4m/difficulty_with_changing_autodesk_registration/)

---

🔑 **Keywords**: Jetson Orin Nano boot failure, syslog explosion, Chromium crash, PackageKit loop  
⚠️ **Problem**:  
During development on Jetson Orin Nano (2TB SSD), a popup warned disk was full. Attempted to delete `/var/log` files, but giant `syslog` couldn't be properly deleted. Rebooted directly — system failed to boot.

Root cause: **syslog was written to tens of GB**, filling the root partition, causing Jetson to fail on reboot.

Triggered by known Jetson bugs:
* Chromium (snap) has zygote errors on Jetson, **flooding syslog**
* PackageKit / update-notifier loops endlessly checking for updates
* Default logrotate **doesn't limit syslog max size**
* NVIDIA has officially acknowledged Chromium + PackageKit crash issues

✅ **Solution**:

<details>
  <summary>1. Mount Jetson SSD on another Linux machine, find the giant syslog</summary>

```
ls -lh /media/xxx/ROOTFS/var/log
```

You'll see `syslog` at **20GB-80GB**.

</details>

<details>
  <summary>2. Delete corrupted/oversized syslog, recreate empty log file</summary>

```
sudo rm /media/.../var/log/syslog
sudo touch /media/.../var/log/syslog
sudo chown syslog:adm /media/.../var/log/syslog
sudo chmod 640 /media/.../var/log/syslog
```

</details>

<details>
  <summary>3. Fix logrotate to limit syslog max size</summary>

Edit:
```
/etc/logrotate.d/rsyslog
```

Add:
```
size 100M
rotate 4
compress
```

</details>

<details>
  <summary>4. Disable services that commonly cause syslog explosion on Jetson</summary>

```
sudo systemctl disable --now packagekit.service
sudo systemctl disable --now packagekit-offline-update.service
sudo systemctl disable --now update-notifier.service
sudo systemctl disable --now update-notifier-crash.service
sudo systemctl disable --now apport.service
sudo systemctl mask apport.service
```

</details>

<details>
  <summary>5. Uninstall Chromium (officially confirmed to cause syslog storms on Jetson)</summary>

```
sudo snap remove chromium
```

Known issues on Jetson Orin:
* `zygote_linux.cc` errors
* setcap permission failures
* Internal crashes flooding syslog

Official recommendation: use Firefox instead of Chromium on Jetson.

</details>

<details>
  <summary>6. Eject SSD, reinstall in Jetson — system boots successfully</summary>

After cleaning syslog + disabling problematic services, system recovers normally.

</details>

---

📚 **Source**:
* [syslog explosion crashing Ubuntu](https://askubuntu.com/questions/1103137/huge-syslog-file-crashing-system)
* [zygote error filling Linux syslog](https://www.reddit.com/r/discordapp/comments/1o55chc/zygote_linuxcc_error_filling_syslog/)
* [NVIDIA confirms: Chromium broke on Jetson Orin](https://jetsonhacks.com/2025/07/12/why-chromium-suddenly-broke-on-jetson-orin-and-how-to-bring-it-back/#:~:text=Here%20is%20the%20NVIDIA%20Jetson,set%20capabilities:%20Operation%20not%20permitted)

---

🔑 **Keywords**: iTerm2 Cmd+Click opens files in Xcode instead of VS Code

⚠️ **Problem**: Cmd+clicking file paths in iTerm2 (e.g., `docs/research_summary.md` from Claude Code output) opens Xcode instead of VS Code, because macOS associates `.md` files with Xcode.

✅ **Solution**: Configure Semantic History in iTerm2:
- **Preferences (Cmd+,) → Profiles → Advanced** → scroll to **Semantic History**
- Select **"Run command..."** from dropdown
- Enter: `/usr/local/bin/code --goto \1:\2`
- `\1` is the file path (auto-substituted by iTerm2), `\2` is the line number (from `:42` format), `--goto` makes VS Code open and jump to the specified line

💡 **Extra tip**: Add this to VS Code `settings.json` to open `.md` files in preview mode by default:
```json
"workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
}
```

📚 **Source**: [Claude]

💡 **Troubleshooting**: If configured correctly but Cmd+Click still doesn't work (especially for relative paths like `docs/xxx.md`), check if iTerm2 Shell Integration is installed. Without shell integration, iTerm2 can't determine the terminal's current working directory (CWD), so it can't resolve relative paths to absolute paths.

Diagnosis:
- Check if file exists: `ls ~/.iterm2_shell_integration.zsh`
- Check if `.zshrc` sources it: `grep iterm2_shell_integration ~/.zshrc`

Fix:
```bash
curl -L https://iterm2.com/shell_integration/zsh -o ~/.iterm2_shell_integration.zsh
echo 'source ~/.iterm2_shell_integration.zsh' >> ~/.zshrc
source ~/.iterm2_shell_integration.zsh
```
Or via menu: **iTerm2 → Install Shell Integration**

📚 **Source**: [Claude]

---

🔑 **Keywords**: Vast.ai SSH Key team sharing limitation
⚠️ **Problem**: After renting a GPU server on Vast.ai, SSH keys can only be uploaded via personal account on the web UI. Team members cannot share uploaded SSH keys — each person must set up individually.
✅ **Solution**: Each team member must log into their own Vast.ai account and upload their public key at **Account → SSH Keys**. Alternatively, after the instance starts, manually append team members' public keys to `~/.ssh/authorized_keys`:
```bash
# Run on the started instance
echo "ssh-ed25519 AAAA... teammate@email" >> ~/.ssh/authorized_keys
```
📚 **Source**: [Practical experience]

---

🔑 **Keywords**: macOS diskutil format external drive to exFAT (Linux/Mac universal)
⚠️ **Problem**: Need to format a 6TB NTFS external hard drive to a format that both Linux and macOS can natively read and write
✅ **Solution**:
<details><summary>diskutil formatting workflow</summary>

1. Identify disk number: `diskutil list`
2. Unmount disk: `diskutil unmountDisk /dev/diskN`
3. Format as exFAT: `diskutil eraseDisk ExFAT VolumeName GPT /dev/diskN`
4. Verify: `diskutil info /dev/diskNs2`

exFAT is chosen because both Mac and Linux natively read/write it without extra drivers. GPT partition table is the modern standard.

</details>

📚 **Source**: [Apple diskutil man page](https://ss64.com/mac/diskutil.html) / [Claude]

---

🔑 **Keywords**: diskutil rename external drive, exFAT volume name restrictions
⚠️ **Problem**: `diskutil rename` fails with `does not appear to be a valid volume name` because the name contains underscores `_` or other special characters
✅ **Solution**: Avoid special characters (underscores, spaces, etc.) in exFAT volume names — use alphanumeric characters only. Command: `diskutil rename /Volumes/OldName "NewName"`
📚 **Source**: [Claude]

---

🔑 **Keywords**: tar archive large folders to external drive, macOS COPYFILE_DISABLE, zstd parallel compression
⚠️ **Problem**: Dragging many small files (e.g., H36M dataset) to an external drive via Finder is extremely slow (estimated 3 hours) — need a faster method
✅ **Solution**:
<details><summary>Three tar approaches</summary>

**No compression (fastest, for local transfers):**
```bash
COPYFILE_DISABLE=1 tar cf /Volumes/Disk/H36M.tar -C /path/to Downloads H36M
```

**gzip compression (universal):**
```bash
COPYFILE_DISABLE=1 tar czf /Volumes/Disk/H36M.tar.gz -C /path/to Downloads H36M
```

**zstd compression (recommended, 3-5x faster):**
```bash
brew install zstd
COPYFILE_DISABLE=1 tar --use-compress-program='zstd -T0' -cf /Volumes/Disk/H36M.tar.zst -C /path/to Downloads H36M
```

- `COPYFILE_DISABLE=1` prevents macOS from adding `._` junk files (causes issues when extracting on Linux)
- `-T0` uses all CPU cores for parallel compression
- Add `-v` to see per-file progress

</details>

📚 **Source**: [GNU tar manual](https://www.gnu.org/software/tar/manual/) / [Zstandard](https://facebook.github.io/zstd/) / [Claude]

---

🔑 **Keywords**: rsync pause/resume/continue transfer, SIGSTOP/SIGCONT
⚠️ **Problem**: Need to pause rsync during a large file transfer to HDD (e.g., to check USB port speed)
✅ **Solution**:
- Pause: `pkill -STOP rsync` (SIGSTOP — process freezes but doesn't exit)
- Resume: `kill -CONT $(pgrep rsync)`
- Kill completely: `kill $(pgrep rsync)`, then re-run the same rsync command — it will **skip already-transferred files** and resume automatically
📚 **Source**: [rsync man page](https://download.samba.org/pub/rsync/rsync.1) / [Claude]

---

🔑 **Keywords**: Slow USB transfer speed, HDD actual write vs interface speed, system_profiler detect USB version
⚠️ **Problem**: WD Elements 6TB rated at 10 Gbps (USB 3.2 Gen 2), but rsync only achieves ~29 MB/s — suspected USB 2.0 fallback
✅ **Solution**:
- Interface speed ≠ drive speed: mechanical HDDs write at 100-150 MB/s, but 29 MB/s suggests USB 2.0 (480 Mbps ≈ 35 MB/s ceiling)
- Detection command: `system_profiler SPUSBDataType 2>/dev/null | grep -A5 "Elements"`, check the Speed line
- `Up to 5 Gb/s` = USB 3.0 ✅ | `Up to 480 Mb/s` = USB 2.0 ❌
- Fix: plug directly into Mac USB-C/Thunderbolt port, avoid cheap hubs/adapters that cause speed downgrade
📚 **Source**: [Apple Support - USB](https://support.apple.com/en-us/102567) / [Claude]

---

🔑 **Keywords**: HDD slow with many small files, random write vs sequential write, tar packing optimization
⚠️ **Problem**: rsync transferring 14825 small files to HDD — speed fluctuates 40-86 MB/s, far below HDD sequential write theoretical max (~150 MB/s)
✅ **Solution**:
- Cause: each small file triggers HDD head seek (~10ms/seek), random writes are much slower than sequential writes
- Optimization (requires enough SSD space): `tar cf` on SSD first into one large file, then `cp` to HDD (single file sequential write, saturates bandwidth)
- If SSD space is insufficient: rsync is the best option — let it run, it supports resuming after interruption
- rsync resume: re-run the same command after interruption, it skips already-transferred files
📚 **Source**: [Claude]

---
