# 字体授权说明 / Font License

本补丁在游戏内置字体图集（SDF 字体图集）中注入了日文显示所需的字形。用于生成这些字形的字体为：

- **字体名称**：文泉驿点阵宋体 12px / WenQuanYi Bitmap Song 12px
- **版本**：v1.0.0-RC1
- **作者 / 版权人**：文泉驿信任委员会（Board of Trustees）、FangQ、Firefly；
  本 TTF 转换版由 AmusementClub（娱乐部）制作
- **许可协议**：GNU General Public License v2
  （**附加文泉驿字体文档嵌入例外条款** / GPL v2 with the WenQuanYi font-embedding exception）
- **上游来源 / Upstream**：
  - https://github.com/AmusementClub/Wenquanyi-Bitmap-Song-TTF
  - http://wenq.org/wqy2/index.cgi?BitmapSong

## 本补丁如何使用该字体（合规性说明）

- 字体的 TTF 文件 **仅作为构建期工具** 使用（位于仓库 `tools/wqy.ttf`），
  用于在打包阶段把假名与所需汉字 **光栅化（rasterize）** 到游戏自身的字体图集内。
- 分发给玩家的补丁包（`JapanesePatch/files/`）**不包含字体 TTF 文件本身**，
  只含已渲染好的 SDF 字图集（写入 `sharedassets0.assets` 与本地化 bundle）。
- 这正是 GPL 字体「文档嵌入例外条款」所允许的用法：字体被嵌入到文档 / 资源中，
  而不以独立字体文件的形式随闭源程序再分发。
- 因此，本补丁对字体的使用符合上述 **GPL v2 + 字体嵌入例外条款**。

如需查看完整许可证文本，见上游仓库的 LICENSE 文件：
https://github.com/AmusementClub/WenQuanYi-Bitmap-Song-TTF/blob/master/LICENSE

---

# Font license (English)

The font used to generate the Japanese glyphs embedded in this patch:

- **Font**: WenQuanYi Bitmap Song 12px (文泉驿点阵宋体 12px), v1.0.0-RC1
- **Copyright**: Board of Trustees of WenQuanYi, FangQ, Firefly;
  this TTF conversion by AmusementClub.
- **License**: GNU General Public License v2 **with the WenQuanYi font-embedding exception**.
- **Source**: https://github.com/AmusementClub/Wenquanyi-Bitmap-Song-TTF

This patch only rasterizes glyphs from the font at build time; the distributed
package contains the rendered SDF atlas, not the font binary itself, which is
permitted under the font-embedding exception of the GPL.
