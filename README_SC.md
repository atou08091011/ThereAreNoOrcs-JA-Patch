# 《There Are No Orcs》日语本地化补丁

民间（非官方）日语本地化补丁，由社区制作，与游戏官方无关。
在游戏左下角的语言切换区 **新增一个日本国旗图标**，点击即可切换为日语，**不占用原有的中文 / English 语言槽位**。

> 本补丁修复了日文显示常见的「渗色」问题：日文采用与中文一致的白色笔画 + 黑色 Underlay 描边，边缘干净无白雾。所有翻译字符串（共 1956 条）均已完整译出，富文本占位符 `<color>`、`{0}`、换行均正确保留。

---

## 一、功能特性

- **标题界面一键切换日语**：左下角语言区新增日本国旗按钮，克隆自英文按钮，拥有相同的点击 / 高亮 / 悬停行为。
- **不破坏原有语言**：中文、English 原样保留，新增 ja 槽位，互不影响。
- **完整日文翻译**：1956 条 UI 字符串全部译出，含系统设定、菜单、剧情提示等。
- **日文显示修复**：字体图集注入平假名 / 片假名 / 日文标点 / 全角字符 / 译文所需汉字，并修正渗色，效果与中文一致。
- **双语安装器**：图形安装器界面支持 **中文 / 日本語** 一键切换，提示与日志均本地化。
- **自动检索游戏目录**：自动从 Steam 卸载注册表与 `libraryfolders.vdf` 定位游戏，找不到时可手动浏览。
- **可安全回退**：安装前自动备份原文件，随时一键还原到未打补丁状态。

---

## 二、文件清单（大小与用途）

解压后得到 `ThereAreNoOrcs_JA_Patch_v1.0.0` 文件夹，结构如下。

### 顶层

| 文件 / 目录 | 大小 | 用途 |
|---|---|---|
| `JaInstaller.exe` | 2.2 MB | 图形安装器主程序（中 / 日双语界面）。 |
| `_internal/` | ~25 MB | 安装器自带的运行环境（Python 3.14 运行时 + tkinter GUI 库）。**无需用户安装 Python**，双击即可运行。 |
| `files/` | ~144 MB | 补丁实际文件，**安装时由安装器复制到游戏目录**。 |
| `README.md` | —— | 本说明文档。 |
| `FONT_LICENSE.md` | —— | 所用字体的授权与合规说明。 |
| `install.bat` | —— | 无图形界面的安装脚本（备选方案）。 |
| `uninstall.bat` | —— | 无图形界面的卸载脚本（备选方案）。 |

### `files/` 内的补丁文件

| 路径（相对 `files/`） | 大小 | 用途 |
|---|---|---|
| `sharedassets0.assets` | 71 MB | **主字体资产 + SDF 图集**（含注入的日文字形）。游戏实际读取的就是这一份。 |
| `StreamingAssets/aa/StandaloneWindows64/localization-assets-shared_assets_all.bundle` | 71 MB | 同一字体图集的**第二副本**（Addressables 加载所需），已同样注入字形。 |
| `StreamingAssets/aa/catalog.json` | 1.7 MB | 资源地址表，负责注册新增的 bundle / 资产。 |
| `Managed/Assembly-CSharp.dll` | 496 KB | IL 注入：在标题界面生成日本国旗按钮，并让语言切换逻辑支持 `ja`。 |
| `Managed/JaHooks.dll` | 12 KB | 上述 hook 的实现代码（补丁必需，**请勿单独删除**）。 |
| `StreamingAssets/aa/StandaloneWindows64/localization-string-tables-japanese(ja)_assets_all.bundle` | 44 KB | 日语字符串表（翻译内容，1956 条）。 |
| `StreamingAssets/aa/StandaloneWindows64/localization-locales_assets_all.bundle` | 4 KB | 新增 `Japanese (ja)` Locale 资产。 |
| `StreamingAssets/aa/StandaloneWindows64/localization-asset-tables-japanese(ja)_assets_all.bundle` | 4 KB | 日语资产表（字体引用）。 |

---

## 三、关于体积（为什么会这么大）

整个文件夹约 **171 MB**，但其中约 **142 MB 是两份 8192×8192 的 SDF 字体图集**（`sharedassets0.assets` 与那个 71 MB 的 `.bundle`）。

- **为什么这么大**：Unity 的 SDF 字体图集要求以**未压缩**形式存放，且图集虽是 8192×8192，但绝大多数像素是空白（只有被用到的字形区域有内容）。所以文件体积大、但内容稀疏。
- **上传时会大幅缩小**：因为空白像素多、压缩率高，用 zip / 7z 等压缩后体积会显著下降。读者下载到的是压缩包，解压后即还原为上面的文件夹，游戏读取不受影响。
- **`_internal/` 的 25 MB 是什么**：那是安装器自带的 Python 运行时（为了让安装器能在没有 Python 的用户电脑上直接运行而打包进来），不属于游戏补丁本身。

---

## 四、系统要求

- Windows 7 或更高版本（仅支持 Windows / Steam 版 / `StandaloneWindows64` 构建）。
- 需要 **管理员权限**（安装器要向游戏安装目录写入文件，已内嵌 UAC 清单会自动请求提权）。
- 建议先通过 Steam 正常启动过一次游戏，确保游戏目录完整。

---

## 五、安装方法

### 方式一：图形安装器（推荐）

1. 解压得到 `ThereAreNoOrcs_JA_Patch_v1.0.0` 文件夹。
2. **右键 `JaInstaller.exe` →「以管理员身份运行」**。
3. 安装器会**自动检索 Steam 游戏目录**；若未找到，点「浏览」手动选择包含 `There are no Orcs_Data` 的文件夹。
4. 点「安装补丁」即可。安装前会自动备份原文件（备份在游戏目录旁的 `ja_patch_backup/`）。
5. 安装完成后启动游戏，见下方「如何使用」。

### 方式二：脚本（install.bat / uninstall.bat）

适合不想用图形界面的用户，同样需要**管理员权限**运行。

- 安装：右键 `install.bat` → 以管理员身份运行（自动备份到 `backup/`）。
- 卸载：右键 `uninstall.bat` → 以管理员身份运行。

> ⚠️ **重要**：安装与卸载请使用**同一种方式**（都用 exe，或都用 .bat）。两者的备份目录不同（`ja_patch_backup/` vs `backup/`），混用会导致无法正确还原。

---

## 六、如何使用（切换为日语）

1. 通过 Steam 正常启动游戏。
2. 在标题 / 主界面**左下角**的语言切换区域，会看到新增的**日本国旗图标**（位于原有语言图标上方）。
3. 点击该国旗图标，游戏切换为日语；再次点击其它语言图标可切回。
4. 首次切换后的选择会被游戏记住（写入注册表 `languageID_h3590701050`）。

> 若启动后没有出现日本国旗图标，请确认补丁已成功安装（见下方 FAQ）。

---

## 七、卸载 / 回退

- **图形安装器**：打开 `JaInstaller.exe` → 点「卸载 / 还原」，会依据 `ja_patch_backup/install_manifest.json` 还原备份并删除补丁新增的文件。
- **脚本**：运行 `uninstall.bat`（管理员）。

两种方式都会把游戏恢复到未打补丁时的原始状态。

---

## 八、字体授权

补丁在游戏内置字体图集中注入了日文显示所需的字形。生成这些字形的字体为：

- **字体**：文泉驿点阵宋体 12px / WenQuanYi Bitmap Song 12px (v1.0.0-RC1)
- **许可**：GNU GPL v2 **+ 文泉驿字体文档嵌入例外条款**
- **上游**：https://github.com/AmusementClub/Wenquanyi-Bitmap-Song-TTF

该字体的 TTF **仅作为构建期光栅化工具**使用；分发的补丁包**不包含字体文件本身**，只含已渲染好的 SDF 字图集，符合上述「字体嵌入例外条款」。完整说明见 `FONT_LICENSE.md`。

---

## 九、已知事项 / 兼容性

- 标题界面的日语 Logo 图目前暂用英文标题占位，待有图后可自动替换生效。
- 补丁未做签名校验对抗；**游戏本体更新后需重新制作补丁**，旧补丁可能失效。
- 仅适用于 **Windows / Steam / StandaloneWindows64** 版本，不支持其它平台或构建。

---

## 十、常见问题（FAQ）

**Q：杀毒软件报毒 / 安装器无法启动？**
A：`_internal/` 里的 Python 运行时偶尔会被第三方杀软误报（误判为打包型可执行程序）。请将 `JaInstaller.exe` 加入白名单，或从官方来源重新获取压缩包后重试。

**Q：安装器找不到游戏目录？**
A：确认游戏已通过 Steam 安装并能正常启动；或点「浏览」手动指定包含 `There are no Orcs_Data` 的文件夹（通常在 `…\steamapps\common\There Are No Orcs\There Are No Orcs\` 下）。

**Q：安装成功但游戏里没有日本国旗图标？**
A：请确认是以**管理员身份**运行的安装器，且目标路径指向正确的游戏目录；必要时先「卸载 / 还原」再重装一次。也可检查游戏目录下 `ja_patch_backup/` 是否生成，以确认备份与写入是否发生。

**Q：解压后 `files/` 里 71MB 的文件是不是损坏了？**
A：不是。那是 8192×8192 的 SDF 字体图集，未压缩存放、含大量空白像素，体积大属正常；用压缩包分发时会被大幅压缩。

**Q：可以把这个补丁用于其它游戏吗？**
A：不可以，本补丁**仅针对《There Are No Orcs》**的指定版本构建。

---

## 十一、来源与致谢

- 翻译：社区志愿翻译（1956 条 UI 字符串）。
- 字体：文泉驿点阵宋体（WenQuanYi Bitmap Song，GPL v2 + 字体嵌入例外）。
- 本补丁为爱好者非官方作品，与游戏开发商 / 发行商无隶属关系。
