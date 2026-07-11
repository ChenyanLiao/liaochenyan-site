# Photography 照片维护说明

本目录只存放会公开部署的摄影图片。私人原图、手机照片源和带有 EXIF/GPS 的文件不得放在这里。

## 添加照片

1. 只复制原图，不移动或覆盖原文件。
2. 把待挑选的私人照片放到项目根目录的 `assets-private/photography-inbox/`；该目录已被 `.gitignore` 排除，永远不会部署。
3. 在 `work/image-edits/` 中制作发布副本，先清除 EXIF、GPS、设备与创建时间信息。
4. 把完成清理与压缩的发布副本放入本目录的 `gallery/`。
5. 在 `content/photography.json` 中添加对应记录，完成中英文标题、地点与 alt 后再预览。

## 文件命名

使用小写英文、数字和连字符，例如：

`2026-kunming-forest-canopy.webp`

缩略图在文件名末尾添加 `-thumb`：

`2026-kunming-forest-canopy-thumb.webp`

不要在文件名中写入完整住址、姓名、设备序列号或其他私人信息。

## photography.json 字段

- `id`：稳定且唯一的英文标识。
- `src`：大图路径，例如 `/media/photography/nature/example.webp`。
- `thumbnail`：缩略图路径。
- `title.en` / `title.zh`：中英文标题。
- `year`：经过确认的拍摄年份；不确定时先留空，不要猜测。
- `location.en` / `location.zh`：只写适合公开的地点粒度。
- `category`：`nature`、`field`、`research`、`places` 或 `everyday`。
- `alt.en` / `alt.zh`：描述画面内容和必要语境，不写“图片”或文件名。
- `featured`：是否优先展示。

## 推荐尺寸与格式

- 大图长边建议 1600–2400 px。
- 缩略图长边建议 640–900 px。
- 优先使用 WebP；需要进一步压缩且已完成浏览器核验时，可增加 AVIF。
- 不放大低分辨率原图，不使用强 HDR、过度锐化或破坏性压缩。
- 大图与缩略图必须是两个独立文件。

## 生成 WebP

可以使用本机 `cwebp` 从工作副本生成发布文件：

`cwebp -q 82 input.jpg -o output.webp`

发布前再次确认输出文件不含 EXIF/GPS。原始文件始终保留在私人源目录或原下载位置。

## 预览

1. 更新 `content/photography.json`。
2. 在项目根目录运行现有开发预览。
3. 检查英文 `/` 与中文 `/zh`。
4. 检查缩略图、alt、点击大图、Escape 关闭、左右键和移动端触控。
5. 运行 `npm run build`，确认没有图片 404。

## 撤回照片

1. 先从 `content/photography.json` 删除或注释对应记录并预览。
2. 确认页面不再引用后，把公开图片移回 `work/image-edits/withdrawn/` 归档，不要删除原图。
3. 重新构建并检查页面与社交预览中没有残留。

## 哪些目录会公开

- `public/media/photography/` 中的图片会随网站部署。
- `content/photography.json` 中的元数据会进入网站代码。

## 哪些目录永远不应公开

- `assets-private/photography-inbox/`
- `work/image-edits/` 中的源文件、拒绝版本和撤回版本
- Downloads 中的原始照片
- 任何仍含 EXIF、GPS、设备信息、私人住址或敏感研究内容的文件

## 当前临时图片

`gallery/` 中以 `study` 命名的图片是生成式临时视觉习作，页面会明确标注，并不会冒充 Liao 的个人实拍。挑选好真实照片后，以相同文件名替换发布副本并同步更新 `content/photography.json` 即可。
