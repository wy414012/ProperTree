# 它是什么？

ProperTree 是使用 Python *（兼容 2.x 和 3.x）* 和 Tkinter 编写的跨平台 GUI plist 编辑器。

## 特征

- [x] 跨平台 - 应该在 python 和 tkinter 的任何地方工作
- [x] 基于文档支持多窗口
- [x] 节点拖放以重新排序
- [x] 复制和粘贴
- [x] 查找/替换 - 允许搜索键或值
- [x] 有序 - 或无序 - 字典支持
- [x] 完整的撤消重做堆栈
- [x] 在 python 2 中支持二进制属性列表和 unicode
- [x] 扩展整数转换以允许在 xml `<integer>` 标签中使用十六进制整数（例如 `0xFFFF`）
- [x] 上下文感知右键菜单，包括 OpenCore 或 Clover config.plist 文件的模板信息
- [x] OC (Clean) Snapshot 来遍历 OpenCore config.plist 文件的 ACPI、驱动程序、Kexts 和工具的内容
- [x] 支持 Base64、Hex、Ascii 和 Decimal 的值转换器

***

## 获得 ProperTree

### 将存储库下载为 ZIP 文件

在任何系统上，您都可以选择绿色的“代码”按钮，然后选择“下载 ZIP”按钮（或单击 [此处](https://github.com/corpnewt/ProperTree/archive/refs/heads/master.zip) ) 将整个 repo 下载为 zip 文件（注意，这不允许您通过 `git pull` 进行更新 - 任何更新都需要您以相同的方式再次下载 repo）。

### 通过 Git 克隆存储库

#### 在 unix 系统:

```bash
git clone https://github.com/corpnewt/ProperTree
python ./ProperTree/ProperTree.py
- or -
python3 ./ProperTree/ProperTree.py
```

\* 在 macOS 上，您只需在克隆后双击“ProperTree.command”即可启动。

#### 在Windows系统:

```
git clone https://github.com/corpnewt/ProperTree
./ProperTree/ProperTree.bat
```

***

## FAQ

* **ProperTree 在 macOS Monterey (12.x) 上打开一个黑色窗口**

  macOS Monterey 附带的默认 tk 实现似乎无法正确显示。 一种解决方法是从 python.org（找到 [here](https://www.python.org/downloads/macos/)）下载并安装最新版本的 python 3，它捆绑了兼容的 tk，然后使用` buildapp-select.command 位于 ProperTree 的 `Scripts` 目录中，用于构建针对已安装 python 路径的应用程序包。 然后，您可以利用它创建的 `ProperTree.app` 包。
  
* **ProperTree 无法在 macOS Monterey (12.x) 上打开或保存 plist 文件**

 这似乎是内置 tk 以及来自 python.org 的早期“通用”安装程序的问题。 至少在 python 3.10.2 中，此问题已在通用版本中得到解决。 您可以在 [这里](https://www.python.org/downloads/macos/) 获取最新的 python 3 安装程序。 安装后，使用位于 ProperTree 的 `Scripts` 目录中的 `buildapp-select.command` 来构建针对已安装 python 路径的应用程序包。 然后，您可以利用它创建的 `ProperTree.app` 包。

* **双击 .plist 文件时如何打开 ProperTree？**

 在 macOS 上，您可以运行位于 ProperTree 的 `Scripts` 目录中的 `buildapp-select.command` 来构建可以与 .plist 文件关联的应用程序包。
  
在 Windows 上，您可以运行位于 ProperTree 的 `Scripts` 目录中的 `AssociatePlistFiles.bat` 以将 .plist 文件与 `ProperTree.bat` 关联，并在右键单击时在上下文菜单中添加 `Open with ProperTree` 选项。 plist 文件。 这种方法取决于位置，移动您的 ProperTree 副本将需要您重新运行“AssociatePlistFiles.bat”。

* **当我尝试运行 ProperTree 时，我得到 `[ModuleNotFoundError: No module name 'tkinter']`**

  这是因为 ProperTree 所依赖的图形界面库不存在或无法检测到，您需要从包管理器中安装 `tkinter`。

  要在 Ubuntu（和基于 Ubuntu 的发行版）上安装它，您可以运行 `sudo apt-get install python3-tk -y`

* **ProperTree 无法运行，因为它没有权限，这是什么原因？**

这不应该发生，建议您仅从官方的 ProperTree 存储库下载，但如果您对自己的源代码有信心，那么运行 `chmod +x ProperTree.command` 应该可以解决问题

* **我在 macOS 上使用国际键盘布局，并且某些键使用 `NSRangeException' 使 ProperTree 崩溃，原因：'-[__NSCFConstantString characterAtIndex:]: Range or index out of bounds**

这是 macOS 上 Tcl/Tk 的 Cocoa 实现中的一个错误（在 [此处](https://bugs.python.org/issue22566) 进行了讨论）。 来自 [python.org](https://www.python.org/downloads/release/python-2718/) 的最新 python 2 安装程序附带并使用已修复此问题的 Tcl/Tk 8.6.8。 鉴于 `ProperTree.command` 中的 shebang 利用了 `#!/usr/bin/env python` - 应该使用找到的第一个 python 2 二进制文件。 ProperTree 的 `Scripts` 目录中的 `buildapp-select.command` 可用于将特定的 python 安装路径硬编码到 .app 包的可执行文件中。
  
* **ProperTree 在 Big Sur (macOS 11) 上崩溃**

  __As of macOS 11.2 (20D5029f), the system's `tk` installation appears to be fixed, and works correctly.  As such, it should not require an external python version to function.__

 这是因为 macOS 上的默认 python 安装利用了较旧的 `tk` 版本——它缺乏对 macOS 11 的支持。要解决这个问题，您可以从 https://www.python.org/ 下载并安装最新的 python 3 版本 downloads/mac-osx/（注意：目前“通用”3.9.1 安装程序会导致主题问题，不应使用）然后利用 ProperTree 的 `Scripts` 目录中的 `buildapp-select.command` 构建一个 .app 包 将利用该 python 版本。
  
如果您已经通过 `brew` 或其他包管理器安装了 python 3 - 它可能仍然链接到系统 `tk` 版本，除非链接到较新版本，否则它仍然会出现问题。

* **`buildapp-select.command` 用法**

`buildapp-select.command` 的输出示例如下所示。 它将遍历 `which python` 和 `which python3` 的输出，然后尝试加载 `tk` 接口，同时跟踪哪些工作和哪些失败。 下面的示例来自 macOS 11.2 (20D4029f)，系统版本为 python 2 和 3，以及从 python.org 安装的 python 3.9.1。 如果 `Scripts` 文件夹上方的目录中存在现有的 `ProperTree.app`，则该应用程序的 shebang 将被定位并作为 `C. 当前`选项。 在下面的菜单中，我会选择选项 `3` 或 `C` 来使用非系统 python 安装。

```bash
 - Currently Available Python Versions -

1. /usr/bin/python 2.7.16 - tk 8.5 (8.6+ recommended)
2. /usr/bin/python3 3.8.2 - tk 8.5 (8.6+ recommended)
3. /Library/Frameworks/Python.framework/Versions/3.9/bin/python3 3.9.1 - tk 8.6
4. /usr/bin/env python
5. /usr/bin/env python3

C. Current (/Library/Frameworks/Python.framework/Versions/3.9/bin/python3)
Q. Quit

Please select the python version to use:  
```
