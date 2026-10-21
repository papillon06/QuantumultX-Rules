# QuanX 自定义规则

维护者：[@zhyio](https://github.com/zhyio)。高德规则与脚本基于 [@ddgksf2013](https://github.com/ddgksf2013) 的作品，保留原作者署名。

## 高德地图

当前自定义版初始只开启两条开屏规则（01、12）。原版的其余 16 条重写规则完整保留，均已注释，方便逐项选择。天气、附近、打车、首页、搜索框等过滤项初始停用；实际广告效果仍需按你的 App 版本验证。

### 添加到 Quantumult X

在「重写 → 规则资源 → ＋」中添加以下地址，资源标签可填写「高德自定义」，资源解析器关闭，保存、更新并启用。保持重写、MitM 与 QuanX 总开关开启。

```text
https://raw.githubusercontent.com/zhyio/QuantumultX-Rules/main/AdBlock/AmapAds.conf
```

**停用此前添加的原版高德净化资源**。若同时开启，原版仍可能过滤其他内容。其他综合净化资源若也包含高德规则，也可能影响最终效果。

### 自己修改屏蔽内容

1. 打开 [高德规则编辑页](https://github.com/zhyio/QuantumultX-Rules/edit/main/AdBlock/AmapAds.conf)，登录自己的 GitHub。
2. 根据中文说明找到目标项。只修改下面实际的规则行：删除最前面的 `# ` 即开启；添加 `# ` 即停用。不要删除上面的说明注释。
3. 点击 GitHub 的「Commit changes」保存到 `main`。
4. 回 QuanX 手动更新「高德自定义」规则资源，再从后台彻底退出高德后重开。GitHub 原始文件有缓存，未看到改动时稍后再更新。

例如，18 是「左下天气」，保持下面这样即可停用该过滤项：

```text
# ^https?:\/\/.*\.amap\.com\/ws\/valueadded\/weather url reject-dict
```

「初始开启 / 停用」只是发布时的说明。后续以规则行是否带 `#` 为准；你改动后也可以同步修改说明。

| 编号 | 原版规则项目 | 初始设置 |
| --- | --- | --- |
| 00 | 广告域名直连辅助项（分流项，不是拦截） | 停用 |
| 01 | 开屏请求 | 开启 |
| 02 | 首页底部信息流 | 停用 |
| 03 | amdc处理 | 停用 |
| 04 | 底部tab栏角标 | 停用 |
| 05 | 路线规划下方广告 | 停用 |
| 06 | 首页右中广告 | 停用 |
| 07 | 附近页面 | 停用 |
| 08 | 打车页面处理 | 停用 |
| 09 | Tip请求 | 停用 |
| 10 | 首页底部处理 | 停用 |
| 11 | 通用广告请求 | 停用 |
| 12 | 开屏广告 | 开启 |
| 13 | 首页顶部推广 | 停用 |
| 14 | 我的页面 | 停用 |
| 15 | 搜索框热词 | 停用 |
| 16 | 搜索框scene | 停用 |
| 17 | 首页左上角gif | 停用 |
| 18 | 左下天气 | 停用 |

03 为原版 AMDC 处理辅助项，会影响命中的相关应用 HTTPDNS 响应，需要时再自行开启。

### 文件与维护

- [AdBlock/AmapAds.conf](AdBlock/AmapAds.conf)：QuanX 实际订阅、自定义的文件。
- [Scripts/amap.js](Scripts/amap.js)：原版高德响应体脚本快照，供相关规则调用。
- [Scripts/amdc.js](Scripts/amdc.js)：原版 AMDC 辅助脚本快照，默认不启用对应规则。
- [upstream/AmapAds.original.conf](upstream/AmapAds.original.conf)：原版文件完整备份，用于对照，不作为订阅。
- [upstream/SOURCES.md](upstream/SOURCES.md)：来源、版本和校验信息。

本仓库不自动同步上游，自己的改动不会被上游更新覆盖。两份 JS 保留上游原始内容和署名，其中 `amap.js` 是混淆脚本；日常选择过滤项目只需改配置文件。若需更改某条响应体规则的内部逻辑，可进一步修改对应 JS。

已检查规则保留完整、初始启用范围和 JS 语法；未在手机上的 Quantumult X / 高德 App 实测。已有广告缓存可能影响结果，先尝试 App 内清缓存；不必为了首次测试直接卸载。

## 来源与署名

- 高德规则原作者：@ddgksf2013。[原版规则](https://github.com/ddgksf2013/Rewrite/blob/master/AdBlock/AmapAds.conf)。
- [原版高德脚本](https://github.com/ddgksf2013/Scripts/blob/master/amap.js)、[原版 AMDC 脚本](https://github.com/ddgksf2013/Scripts/blob/master/amdc.js)。
- 本仓库调整了配置的初始开关、添加中文编号说明，并将脚本引用指向本仓库；不将原作者作品重新声明为本仓库维护者原创，也不另行授予原作品许可。
