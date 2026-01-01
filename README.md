# Netronome - 懒猫应用

基于懒猫应用发布技能生成的 Netronome 应用配置。

## 📱 应用简介

**Netronome** 是一个现代化的网络速度测试和监控工具，基于 Go 和 React 构建。

- 🏠 **应用名称**: Netronome
- 📦 **包名**: `cloud.lazycat.app.netronome`
- 🎯 **子域名**: `netronome`
- 🔗 **访问地址**: `https://netronome.your-box.lazycat.cloud`
- 💾 **存储路径**: `/lzcapp/var/netronome`
- 🖼️ **端口**: 7575

## 🚀 快速开始

### 方式一：从懒猫应用商店安装（推荐）

1. 打开懒猫应用商店
2. 搜索 "Netronome"
3. 点击安装
4. 根据向导完成配置
5. 启动应用

### 方式二：手动安装

```bash
# 1. 下载 lpk 包
# (从发布页面或构建获取)

# 2. 安装应用
lzc-cli app install netronome-1.0.0.lpk

# 3. 启动应用
lzc-cli app start cloud.lazycat.app.netronome

# 4. 访问应用
# 打开浏览器访问: https://netronome.your-box.lazycat.cloud
```

## 🛠️ 本地构建

如果您需要修改配置或从源码构建：

### 前置要求

- LazyCat CLI (`lzc-cli`)
- Docker 环境
- 512x512 PNG 应用图标 (`icon.png`)

### 构建步骤

```bash
# 1. 克隆或下载本项目
cd netronome-lzcapp

# 2. 准备应用图标
# 确保 icon.png 存在 (512x512 PNG)

# 3. 使用自动化脚本
./build.sh

# 4. 选择构建选项
# 选择 1 - 构建应用

# 5. 安装测试
lzc-cli app install cloud.lazycat.app.netronome-1.0.0.lpk
```

## 📁 项目结构

```
netronome-lzcapp/
├── lzc-manifest.yml      # 应用主配置文件
├── lzc-build.yml         # 构建配置
├── build.sh              # 自动化构建脚本
├── icon.png              # 应用图标 (512x512 PNG)
└── README.md             # 本说明文件
```

## 🔧 配置说明

### lzc-manifest.yml

```yaml
# 应用基础信息
name: Netronome
package: cloud.lazycat.app.netronome
version: 1.0.0
min_os_version: 1.3.8

# 应用配置
application:
  subdomain: netronome
  upstreams:
    - location: /
      backend: http://netronome:7575/

# 服务配置
services:
  netronome:
    image: ghcr.io/autobrr/netronome:latest
    binds:
      - /lzcapp/var/netronome:/data
    cpu_shares: 512
    mem_limit: 512M
    restart: unless-stopped
```

### 配置特点

✅ **智能优化**:
- 无需用户配置参数（零配置应用）
- 自动映射存储路径到 `/lzcapp/var/netronome`
- 合理的资源限制（512MB 内存）
- HTTP 路由自动配置

✅ **安全配置**:
- 使用官方镜像源 `ghcr.io/autobrr/netronome`
- 无敏感环境变量
- 无特权模式

## 📊 资源需求

| 资源类型 | 配置 | 说明 |
|---------|------|------|
| CPU | 512 shares | 基础配置 |
| 内存 | 512 MB | 推荐配置 |
| 存储 | 100 MB | 应用数据 |
| 网络 | HTTP 7575 | Web 界面 |

## 🔗 访问方式

### Web 界面
- **URL**: `https://netronome.your-box.lazycat.cloud`
- **端口**: 7575 (内部)
- **协议**: HTTP/HTTPS

### 网络访问
- **内部服务**: `http://netronome:7575`
- **外部访问**: 通过子域名自动代理

## 📦 版本历史

### v1.0.0 (当前)
- ✅ 基础功能集成
- ✅ 懒猫应用配置
- ✅ 自动化构建脚本
- ✅ 完整文档

## 🔄 更新应用

### 方式一：通过懒猫应用商店
1. 检查应用商店更新
2. 一键升级

### 方式二：手动更新
```bash
# 1. 下载新版本 lpk
# 2. 更新应用
lzc-cli app update cloud.lazycat.app.netronome new-version.lpk
```

## 🛡️ 故障排除

### 问题：应用无法访问

**检查清单**:
1. ✅ 应用是否已启动: `lzc-cli app status cloud.lazycat.app.netronome`
2. ✅ 端口是否正常: 检查 7575 端口监听
3. ✅ 存储权限: 确认 `/lzcapp/var/netronome` 可写
4. ✅ 日志检查: `lzc-cli app logs cloud.lazycat.app.netronome`

### 问题：数据丢失

**解决方案**:
- 数据存储在 `/lzcapp/var/netronome`
- 备份此目录即可保存所有数据
- 重装应用后，恢复此目录数据

### 问题：镜像拉取失败

**解决方案**:
```bash
# 手动测试镜像
docker pull ghcr.io/autobrr/netronome:latest

# 如果失败，检查网络或镜像源
```

## 📞 支持

- **应用源码**: https://github.com/autobrr/netronome
- **懒猫文档**: https://developer.lazycat.cloud
- **问题反馈**: 通过懒猫社区或 GitHub Issues

## 📄 许可证

- **应用**: MIT License (Netronome)
- **配置**: MIT License

## 🎯 技术细节

### 智能分析结果

**服务类型**: 外部服务（有 HTTP 端口）
**配置复杂度**: 简单（零配置需求）
**依赖关系**: 无内部依赖
**健康检查**: 未配置（可选）

### 转换规则应用

| Docker Compose | 懒猫配置 | 说明 |
|---------------|---------|------|
| `ports: "7575:7575"` | `upstreams: / → http://netronome:7575/` | HTTP 路由 |
| `volumes: ./netronome:/data` | `binds: /lzcapp/var/netronome:/data` | 存储映射 |
| `restart: unless-stopped` | `restart: unless-stopped` | 重启策略 |
| `image: ghcr.io/...` | `image: ghcr.io/...` | 镜像保持 |

### 优化改进

✅ **相比原始配置的改进**:
1. **存储路径标准化**: 使用 `/lzcapp/var` 确保数据持久化
2. **资源限制**: 添加合理的 CPU/内存限制
3. **HTTP 代理**: 通过懒猫内置代理访问，无需手动配置端口
4. **自动化**: 提供完整的构建和发布脚本

## 📝 发布流程

### 完整发布步骤

```bash
# 1. 准备环境
# - 安装 lzc-cli
# - 登录懒猫应用商店: lzc-cli appstore login

# 2. 一键发布
./build.sh
# 选择 4 - 一键构建+镜像复制+发布

# 3. 等待审核
# - 审核时间: 1-3 天
# - 审核通过后，应用将出现在商店

# 4. 用户安装
# - 在懒猫应用商店搜索 "Netronome"
# - 点击安装即可
```

### 手动发布步骤

```bash
# 1. 构建应用
./build.sh
# 选择 1 - 构建应用

# 2. 复制镜像（如果需要）
./build.sh
# 选择 2 - 镜像复制到懒猫仓库

# 3. 发布应用
./build.sh
# 选择 3 - 发布到应用商店
```

## 💡 使用技巧

### 1. 数据备份
```bash
# 备份数据
tar -czf netronome-backup.tar.gz /lzcapp/var/netronome

# 恢复数据
tar -xzf netronome-backup.tar.gz -C /
```

### 2. 日志查看
```bash
# 实时日志
lzc-cli app logs -f cloud.lazycat.app.netronome

# 历史日志
lzc-cli app logs --tail 100 cloud.lazycat.app.netronome
```

### 3. 性能监控
```bash
# 查看资源使用
lzc-cli app stats cloud.lazycat.app.netronome

# 查看运行状态
lzc-cli app status cloud.lazycat.app.netronome
```

## 🎉 特性优势

### 懒猫应用发布技能优势

✅ **智能分析**:
- 自动识别服务类型
- 优化配置参数
- 减少用户配置负担

✅ **自动化流程**:
- 一键构建+发布
- 镜像自动管理
- 版本控制

✅ **最佳实践**:
- 符合懒猫应用规范
- 安全的默认配置
- 完整的文档支持

### Netronome 应用优势

✅ **现代化工具**:
- 基于 Go 和 React 构建
- 现代化 UI 设计
- 高性能网络测试

✅ **功能强大**:
- 网络速度测试
- 实时监控
- 详细报告

✅ **易于使用**:
- Web 界面操作
- 无需命令行
- 直观的数据展示

---

**生成时间**: 2026-01-01
**生成工具**: 懒猫应用发布技能 v1.0
**应用版本**: 1.0.0
