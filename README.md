# Resolution Display Tool - 分辨率展示工具

## Overview - 概述
This Resolution Display Tool is developed based on the Pygame library, specifically designed for the Windows operating system. It aims to visually demonstrate the display effects of various common resolutions on the current screen, while providing detailed information such as aspect ratio, screen occupancy ratio, and zoom factor of each resolution. The tool also addresses high-DPI scaling issues to ensure accurate display across different system scaling settings.

该分辨率展示工具基于 Pygame 库开发，专为 Windows 操作系统设计。其核心目标是直观展示多种常见分辨率在当前屏幕上的显示效果，同时提供各分辨率的长宽比、屏幕占比、放大倍数等详细信息。工具还针对高 DPI 缩放问题进行了适配，确保在不同系统缩放设置下均能精准显示。

## Key Features - 核心特性
1. High-DPI Adaptation: Retrieves the system DPI value and calculates the scaling factor to adjust font sizes and UI elements dynamically, ensuring proper display on high-resolution screens with system scaling enabled.

1. 高 DPI 适配：获取系统 DPI 值并计算缩放比例，动态调整字体大小和 UI 元素，确保在开启系统缩放的高分辨率屏幕上正常显示。

2. Comprehensive Resolution Information: Calculates and displays the aspect ratio (simplified to the smallest integer ratio) of each resolution, as well as the horizontal and vertical occupancy ratio relative to the full screen and the corresponding zoom factor.

2. 全面的分辨率信息：计算并展示每个分辨率的长宽比（简化为最小整数比），以及相对于全屏的水平占比、垂直占比和对应的放大倍数。

3. Dual Display Modes: Supports two display modes for the resolution preview area: top-left alignment and center alignment, switchable via keyboard operation.

3. 双显示模式：分辨率预览区域支持两种显示模式——左上角对齐和居中对齐，可通过键盘操作切换。

4. Interactive Control: Allows users to navigate through the resolution list using keyboard keys, with real-time visual feedback for the currently selected resolution.

4. 交互式控制：用户可通过键盘方向键浏览分辨率列表，当前选中的分辨率会提供实时视觉反馈。

5. Frame Rate Control: Limits the frame rate to 60 FPS to ensure smooth operation and reduce resource consumption.

5. 帧率控制：将帧率限制为 60 FPS，保证工具运行流畅且降低资源消耗。

6. User-Friendly UI: Displays a clear list of resolutions (with highlighted current selection), operation hints, and display mode information for easy usability.

6. 友好的用户界面：清晰展示分辨率列表（高亮当前选中项）、操作提示和显示模式信息，提升易用性。

## Environment Requirements - 环境要求
- Operating System: Windows (the tool uses the `user32.dll` library via ctypes, which is exclusive to Windows).

- 操作系统：Windows（工具通过 ctypes 调用 `user32.dll` 库，该库为 Windows 系统专属）。

- Python Version: Compatible with Python 3.x (tested on Python 3.11.9).

- Python 版本：兼容 Python 3.x（已在 Python 3.11.9 版本测试）。

- Dependencies: Requires the Pygame library to be installed. Install it via the following command:

- 依赖库：需安装 Pygame 库，可通过以下命令安装：

  ```bash
  pip install pygame
  ```

## Usage Instructions - 使用说明
1. Ensure the required environment and dependencies are installed as specified in the "Environment Requirements" section.

1. 按照“环境要求”部分的说明，确保安装所需的操作系统、Python 版本和依赖库。

2. Save the script file (e.g., [`draw_resolutions.py`](draw_resolutions.py)) to a local directory. Or clone the entire project repository `git clone https://github.com/MinMax-imum/Resolution-Display-Tool.git`.

2. 将脚本文件（如 [`draw_resolutions.py`](draw_resolutions.py)）保存到本地目录。或克隆整个项目仓库 `git clone https://github.com/MinMax-imum/Resolution-Display-Tool.git`。

3. Run the following script using Python, or execute the startup script [`run draw_resolutions.bat`](<run draw_resolutions.bat>) or debugging script [`debug draw_resolutions.bat`](<debug draw_resolutions.bat>).

3. 使用 Python 运行以下脚本，或运行启动脚本 [`run draw_resolutions.bat`](<run draw_resolutions.bat>) 或调试脚本 [`debug draw_resolutions.bat`](<debug draw_resolutions.bat>)。

   ```bash
   python draw_resolutions.py
   ```

4. The startup script [`run draw_resolutions.bat`](<run draw_resolutions.bat>) will run in `pythonw` without displaying the command line window, while the debugging script [`debug draw_resolutions.bat`](<debug draw_resolutions.bat>) will display the command line window to facilitate viewing debugging information.

4. 启动脚本 [`run draw_resolutions.bat`](<run draw_resolutions.bat>) 使用 pythonw 运行而不显示命令行窗口，调试脚本 [`debug draw_resolutions.bat`](<debug draw_resolutions.bat>) 则会显示命令行窗口以方便查看调试信息。

5. The tool will launch in a borderless full-screen window (matching the current screen resolution), displaying the default resolution (1920×1080, or the first resolution in the list if 1920×1080 is not included).

5. 工具将以无边框全屏窗口（匹配当前屏幕分辨率）启动，默认显示 1920×1080 分辨率（若列表中无此分辨率，则显示列表第一个）。

## Code Explanation - 代码说明

### Core Functions - 核心函数
- `get_aspect_ratio(width, height)`: Uses the `Fraction` class to calculate the simplified aspect ratio of a resolution (e.g., 1920×1080 is simplified to 16:9) by limiting the denominator to the smallest integer.

- `get_aspect_ratio(width, height)`：利用 `Fraction` 类计算分辨率的简化长宽比（例如 1920×1080 简化为 16:9），通过限制分母为最小整数实现比例简化。

- `get_scale_info(width, height)`: Computes the horizontal and vertical occupancy ratio of the resolution relative to the full screen (as a percentage) and the zoom factor required to fit the resolution to the full screen (as a percentage).

- `get_scale_info(width, height)`：计算分辨率相对于全屏的水平占比和垂直占比（以百分比表示），以及将该分辨率适配到全屏所需的放大倍数（以百分比表示）。

### Main Logic - 主逻辑
- **Initialization**: Initializes Pygame, handles high-DPI scaling, retrieves the actual screen resolution, and sets up fonts (adjusted for scaling) and the display window (borderless full-screen).

- **初始化**：初始化 Pygame，处理高 DPI 缩放，获取实际屏幕分辨率，设置适配缩放比例的字体和显示窗口（无边框全屏）。

- **Event Handling**: Listens for keyboard events to switch resolutions (Up or Down keys), toggle display modes (Space key), and exit the tool (`ESC` key or `QUIT` event).

- **事件处理**：监听键盘事件，实现分辨率切换（上下方向键）、显示模式切换（空格键）以及工具退出（`ESC` 键或 `QUIT` 事件）。

- **UI Rendering**: Draws the resolution preview area (with white border and light gray fill), displays detailed resolution information, a list of all resolutions (with highlighted current selection), operation hints, and display mode status.

- **UI 渲染**：绘制分辨率预览区域（白色边框配浅灰色填充），展示详细的分辨率信息、所有分辨率列表（高亮当前选中项）、操作提示和显示模式状态。

- **Frame Rate Control**: Uses `pygame.time.Clock` to limit the frame rate to 60 FPS, ensuring smooth rendering.

- **帧率控制**：通过 `pygame.time.Clock` 将帧率限制为 60 FPS，保证渲染流畅。

## Operation Guide - 操作指南
- **Up Arrow Key**: Switch to the previous resolution in the list (circular navigation).

- **向上方向键**：切换到列表中的上一个分辨率（循环切换）。

- **Down Arrow Key**: Switch to the next resolution in the list (circular navigation).

- **向下方向键**：切换到列表中的下一个分辨率（循环切换）。

- **Space Bar**: Toggle between center alignment and top-left alignment for the resolution preview area.

- **空格键**：切换分辨率预览区域的显示模式（居中对齐或左上角对齐）。

- **`ESC` Key**: Exit the tool immediately.

- **`ESC` 键**：立即退出工具。

## Notes - 注意事项
- The resolution list is pre-defined in the script; users can modify the `resolutions` list to add or remove custom resolutions as needed.

- 分辨率列表在脚本中预定义，用户可根据需要修改 `resolutions` 列表，添加或删除自定义分辨率。

- The tool uses the "SimHei" font to ensure proper display of Chinese characters; if this font is not available on the system, replace it with another Chinese-supported font (e.g., "Microsoft YaHei").

- 工具使用黑体 `SimHei` 字体保证中文字符正常显示；若系统无此字体，需替换为其他支持中文的字体（如微软雅黑 `Microsoft YaHei`）。

- The borderless full-screen mode is used by default (instead of true full-screen) to avoid issues with system display settings; modify the `pygame.display.set_mode` parameter if true full-screen is required.

- 工具默认使用无边框全屏模式（而非真正的全屏模式），以避免系统显示设置相关问题；若需启用真正的全屏模式，可修改 `pygame.display.set_mode` 的参数。

---

**The document is generated by DouBao AI, and is modified and improved manually**
**文档由豆包 AI 生成，经人工修改完善**

---

Last Update: January 13, 2026  
最后更新：2026-01-13
