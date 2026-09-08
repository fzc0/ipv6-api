# IPv6 归属离线库测试（国际库）

基于 **DB-IP Lite**（免费、每月更新、CC BY 4.0）构建的 IPv6 国家归属查询，数据文件随项目部署，查询在浏览器本地完成，不依赖任何在线接口。

## 文件

- `index.html` — 查询页面：输入 IPv6，二分查找命中网段并显示国家
- `data/v6-country.json.gz` — IPv6 国家归属数据（360k 条网段，gzip 后约 2.3MB）

## 部署

### 方式一：EdgeOne Pages（推荐，仓库可私有）

1. EdgeOne 控制台 → 站点 → Pages → 创建项目，关联本仓库和 `main` 分支；
2. 框架预设留空，构建命令留空，输出目录填 `.`；
3. 部署后访问 Pages 域名即可。

### 方式二：GitHub Pages（需仓库公开）

仓库 Settings → Pages → Source 选 `main` / root，即可访问 `https://<用户名>.github.io/ipv6-api/`。

## 每月更新数据

```bash
# 1) 下载当月国家库
curl -LO https://download.db-ip.com/free/dbip-country-lite-$(date +%Y-%m).csv.gz
# 2) 过滤 IPv6 行并转成十六进制范围 JSON（保留起止网段 + 国家码）
# 3) gzip -9 压缩后替换 data/v6-country.json.gz
# 4) git add/commit/push，Pages 自动重新部署
```

转换脚本参考 `../work/dbcheck/build-country.mjs`。

## 数据署名

数据来源：DB-IP Lite，许可 CC BY 4.0。页面底部保留来源链接即可免费使用。

## 后续计划

- 城市级 IPv6 库（体积较大，需合并相邻网段压缩后接入）
- 提供 `/api/ipv6?ip=...` 形式的查询接口（边缘函数）
