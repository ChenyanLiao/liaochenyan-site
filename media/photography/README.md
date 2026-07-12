# Photography 照片维护说明

本目录只存放会公开部署的摄影发布副本。私人原图、手机源文件和带有 EXIF/GPS 的文件不得放在这里。

## 当前状态

- `gallery/` 现有 18 幅个人摄影作品，每幅包含大图与 `-thumb` 缩略图，共 36 个 WebP 文件。
- 首页从 18 幅作品中选取 5 幅展示，移动端显示其中 3 幅；完整图库仍可浏览全部作品。
- 所有标题、摘要、完整描述、地点粒度与替代文本均由 `content/photography.json` 管理。
- 旧的生成式临时习作已移入 `work/archived-public-assets/20260712-photography-placeholders-retired/`，不再公开部署。

## 添加或替换照片

1. 只复制原图，不移动或覆盖原文件。
2. 把私人照片放入 `assets-private/photography-inbox/`；该目录由 `.gitignore` 排除，不会部署。
3. 在忽略的 `assets-private/media-source-catalog.private.json` 中记录源文件与公开英文标识，不把私人文件名写入公开代码。
4. 在 `content/photography.json` 中填写中英文标题、摘要、完整描述、公开地点粒度、替代文本和尺寸。
5. 运行 `npm run prepare:media` 生成清除元数据的 WebP 大图与缩略图。
6. 检查英文 `/`、中文 `/zh`、首页换一组、完整图库、键盘操作和移动端布局。
7. 运行 `npm test`，确认构建与公开边界测试通过。

## photography.json 字段

- `id`：稳定且唯一的英文标识。
- `src`：公开大图路径。
- `thumbnail`：公开缩略图路径。
- `title.en` / `title.zh`：中英文标题。
- `summary.en` / `summary.zh`：首页使用的一句简短描述。
- `description.en` / `description.zh`：大图浏览器中的完整描述。
- `year`：经过确认的拍摄年份；不确定时留空。
- `location.en` / `location.zh`：只写适合公开的地点粒度。
- `category`：作品类别。
- `alt.en` / `alt.zh`：如实描述画面内容，不写文件名或私人信息。
- `featured`：初始展示优先级。

## 发布规格

- 大图长边上限为 2600 px，缩略图宽度上限为 1200 px、竖图高度上限为 900 px。
- 发布格式为 WebP；不放大低分辨率原图，不做破坏性锐化或过度 HDR。
- `scripts/prepare-public-media.mjs` 会重新编码图像并检查 EXIF、XMP 与 IPTC 字段。
- 原始照片始终保留在私人目录；网页只使用尺寸优化、元数据清理后的发布副本。

## 撤回照片

1. 先从 `content/photography.json` 移除对应记录并预览。
2. 确认页面不再引用后，把公开副本移入 `work/image-edits/withdrawn/` 归档，不直接删除。
3. 重新构建，并检查页面、图片清单与社交预览没有残留引用。

## 绝不公开

- `assets-private/photography-inbox/`
- `assets-private/media-source-catalog.private.json`
- `work/` 中的原图、拒绝版本、撤回版本与归档版本
- 任何仍含 EXIF、GPS、设备信息、私人住址、电话号码或敏感研究内容的文件
