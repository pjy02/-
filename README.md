# 🚀 网站性能检测工具

一个功能全面的网站性能检测工具，支持测试任意域名的连接类型、CDN状态、多地Ping检测、SSL证书和服务器性能分析。具备智能DNS服务器排序、优化检测速度和完善的部署支持。

## ✨ 主要功能

### 🎯 核心特性
- **智能连接类型检测**: 准确识别直连、CDN加速、代理、混合连接类型
- **多地Ping检测**: 全球40+个地区的DNS服务器并发检测，分析CDN地理覆盖
- **自定义域名测试**: 支持测试任意域名，无需固定配置
- **详细性能分析**: 提供DNS解析、TCP连接、SSL握手、TTFB等详细时间分析
- **SSL证书检测**: 获取SSL证书的详细信息，智能格式化域名范围显示
- **多界面支持**: Web界面、命令行工具、API接口三种使用方式

### 🔍 智能检测能力
- **CDN提供商识别**: 支持15+主流CDN服务商自动识别
- **连接类型分析**: 区分直连、CDN、代理、混合连接类型
- **置信度评估**: 提供高、中、低三级检测置信度
- **代理头检测**: 识别各种代理服务器和负载均衡器特征
- **地理分布分析**: 基于多地DNS检测结果分析CDN覆盖范围
- **智能排序**: 中国地区DNS服务器优先显示，失败服务器置底

### 📊 测试指标
- **DNS解析时间**: 域名解析到IP地址的时间
- **TCP连接时间**: 建立TCP连接的时间
- **SSL握手时间**: SSL/TLS握手时间（HTTPS）
- **首字节时间(TTFB)**: Time to First Byte
- **内容下载时间**: 下载响应内容的时间
- **总响应时间**: 完整的请求响应时间
- **服务器信息**: 服务器软件、响应头、状态码等
- **连接类型**: CDN加速、直连、代理、混合连接
- **SSL证书**: 证书颁发机构、有效期、域名范围
- **多地Ping**: 全球40+地区DNS解析结果和IP一致性分析

### 🛠️ 技术栈
- **前端**: Next.js 15 + TypeScript + Tailwind CSS + shadcn/ui
- **后端**: Next.js API Routes + Node.js
- **检测引擎**: 自定义HTTP请求库 + DNS解析 + 多维度特征分析
- **实时通信**: Socket.IO + WebSocket
- **数据库**: Prisma ORM + SQLite（可选）
- **界面组件**: Lucide图标 + Framer Motion动画

## 🚀 快速开始

### 环境要求
- **Node.js**: >= 18.0.0
- **npm**: >= 8.0.0
- **内存**: >= 512MB
- **存储**: >= 1GB

### 安装和运行

```bash
# 克隆项目
git clone <repository-url>
cd website-performance-tester

# 安装依赖
npm install

# 初始化数据库（如果使用Prisma）
npx prisma generate
npx prisma db push

# 启动开发服务器
npm run dev
```

访问 [http://localhost:3000](http://localhost:3000) 查看Web界面。

## 🐳 Docker 部署（推荐）

本项目提供完整的 Docker 部署方案，支持 GitHub Actions 自动构建和推送到 Docker Hub。

### 快速部署

```bash
# 克隆项目
git clone https://github.com/233bit/website-performance-tool.git
cd website-performance-tool

# 启动生产环境
docker-compose -f docker-compose.prod.yml up -d

# 访问应用
# 浏览器打开: http://localhost:3000
```

### GitHub Actions 自动化

项目配置了 GitHub Actions，实现：

- ✅ 自动构建 Docker 镜像
- ✅ 自动推送到 Docker Hub (`233bit/website-performance-tool`)
- ✅ 支持多平台构建（linux/amd64, linux/arm64）
- ✅ 自动标签管理（latest, 版本号等）

### 直接使用 Docker Hub 镜像

```bash
# 拉取镜像
docker pull 233bit/website-performance-tool:latest

# 运行容器
docker run -d \
  --name website-performance-tool \
  -p 3000:3000 \
  --restart unless-stopped \
  233bit/website-performance-tool:latest
```

### 管理命令

```bash
# 查看状态
docker-compose -f docker-compose.prod.yml ps

# 查看日志
docker-compose -f docker-compose.prod.yml logs -f

# 停止服务
docker-compose -f docker-compose.prod.yml down

# 重启服务
docker-compose -f docker-compose.prod.yml restart

# 更新服务
docker-compose -f docker-compose.prod.yml pull
docker-compose -f docker-compose.prod.yml up -d --force-recreate
```

## 📋 详细文档

- [🐳 Docker 部署指南](./DOCKER-DEPLOYMENT.md)
- [🚀 快速开始指南](./QUICK-START.md)

## 🎯 使用方法

### Web 界面使用

#### 1. 基本测试
- 打开浏览器访问 `http://localhost:3000`
- 在输入框中输入要测试的域名（如：example.com）
- 点击"开始测试"按钮

#### 2. 自动测试
- 输入域名后点击"自动测试"按钮
- 系统会每5秒自动测试一次
- 再次点击可停止自动测试

#### 3. 查看详细结果
- **概览面板**: 关键指标快速查看
- **性能面板**: 详细的性能分析
- **多地Ping面板**: 全球40+地区DNS检测结果
- **CDN分析面板**: 连接类型和CDN检测详情
- **优化建议面板**: 分级优化建议
- **服务器面板**: 服务器信息和响应头
- **SSL证书面板**: SSL证书详细信息
- **历史记录面板**: 测试历史记录

### 命令行工具使用

```bash
# 基本测试（默认域名）
node domain-test-cli.js

# 测试指定域名
node domain-test-cli.js --domain example.com
# 或
node domain-test-cli.js -d example.com

# 批量测试
node domain-test-cli.js --domain example.com --count 10
# 或
node domain-test-cli.js -d example.com -c 10

# 自定义测试间隔
node domain-test-cli.js --domain example.com --count 5 --interval 2000
# 或
node domain-test-cli.js -d example.com -c 5 -i 2000

# 自定义API地址
node domain-test-cli.js --domain example.com --api-url http://your-server:3000/api/test-domain
# 或
node domain-test-cli.js -d example.com -a http://your-server:3000/api/test-domain

# 查看帮助
node domain-test-cli.js --help
# 或
node domain-test-cli.js -h
```

### API 接口使用

```bash
# GET 请求
curl "http://localhost:3000/api/test-domain?domain=example.com"

# POST 请求
curl -X POST "http://localhost:3000/api/test-domain" \
  -H "Content-Type: application/json" \
  -d '{"domain": "example.com"}'

# 查看响应头
curl -I "http://localhost:3000/api/test-domain?domain=example.com"
```

## 🔍 多地Ping检测详解

### 检测原理
工具通过全球40+个地区的DNS服务器并发查询目标域名，分析：

1. **DNS解析结果**: 不同地区返回的IP地址
2. **响应时间**: 各地区DNS查询的响应速度
3. **IP一致性**: 检测是否使用CDN的地理分布
4. **健康状态**: DNS服务器的可用性

### DNS服务器来源
- **国际公共DNS**: Google DNS (8.8.8.8), Cloudflare DNS (1.1.1.1), Quad9 (9.9.9.9)
- **中国ISP DNS**: 阿里云DNS (223.5.5.5), 腾讯云DNS (119.29.29.29), 中国电信114DNS (114.114.114.114)
- **亚太地区**: 日本、韩国、新加坡、泰国、印尼、菲律宾、澳洲等
- **欧美地区**: 英国、法国、德国、荷兰、瑞典、俄罗斯、美国、加拿大等

### 智能排序机制
1. **成功的中国DNS服务器**（优先显示）
2. **成功的其他地区DNS服务器**
3. **失败的中国DNS服务器**
4. **失败的其他地区DNS服务器**（置底显示）

### 地理分布分析
- **全球覆盖**: 80%以上地区有响应
- **广泛覆盖**: 60-80%地区有响应
- **中等覆盖**: 40-60%地区有响应
- **有限覆盖**: 低于40%地区有响应

## 🔧 故障排除

### 常见问题

#### 1. 安装依赖失败
```bash
# 清除缓存重新安装
npm cache clean --force
rm -rf node_modules package-lock.json
npm install

# Linux 下缺少编译工具
# Ubuntu/Debian
sudo apt install build-essential python3

# CentOS/RHEL
sudo yum groupinstall "Development Tools"
sudo yum install python3
```

#### 2. 端口占用
```bash
# 查看端口占用
# Linux/macOS
sudo lsof -i :3000
sudo netstat -tulpn | grep :3000

# Windows
netstat -ano | findstr :3000

# 结束进程
# Linux/macOS
sudo kill -9 <PID>

# Windows
taskkill /PID <PID> /F
```

#### 3. DNS解析失败
- 检查域名是否正确
- 检查网络连接
- 检查DNS服务器设置
- 检查防火墙是否阻止DNS查询

#### 4. 连接超时
- 检查目标服务器是否可访问
- 检查防火墙设置
- 增加超时时间配置
- 检查网络稳定性

#### 5. SSL证书错误
- 检查证书是否有效
- 检查系统时间是否正确
- 检查证书链是否完整
- 更新根证书库

#### 6. 权限问题
```bash
# Linux 下修改文件权限
sudo chown -R $USER:$USER /path/to/project
chmod -R 755 /path/to/project

# 创建专用用户运行服务
sudo useradd -r -s /bin/false domain-test
sudo chown -R domain-test:domain-test /var/www/domain-test
```

### 调试模式

```bash
# 查看详细日志
tail -f dev.log

# PM2 调试
pm2 logs domain-test
pm2 monit

# 系统服务调试
sudo journalctl -u domain-test -f

# Docker 调试
docker-compose logs -f domain-test

# 网络调试
curl -v "http://localhost:3000/api/test-domain?domain=example.com"
```

### 性能问题

#### 1. 检测速度慢
- 检查网络延迟
- 优化DNS服务器列表
- 调整并发查询数量
- 启用缓存机制

#### 2. 内存使用过高
```bash
# 查看内存使用
free -h
htop

# PM2 内存限制
pm2 start server.ts --max-memory-restart 500M

# 系统级别内存优化
echo 'vm.swappiness=10' >> /etc/sysctl.conf
sysctl -p
```

#### 3. CPU 使用率高
- 检查是否有死循环
- 优化算法复杂度
- 增加缓存机制
- 考虑负载均衡

## 📁 项目结构

```
website-performance-tool/
├── src/
│   ├── app/                          # Next.js App Router
│   │   ├── api/                      # API 路由
│   │   │   ├── test-domain/          # 域名测试 API
│   │   │   ├── cdn-latency/          # CDN 延迟测试 API
│   │   │   └── health/               # 健康检查 API
│   │   ├── page.tsx                  # 主页面
│   │   ├── layout.tsx                # 布局组件
│   │   └── globals.css               # 全局样式
│   ├── components/                   # React 组件
│   │   └── ui/                       # shadcn/ui 组件
│   ├── hooks/                        # 自定义 hooks
│   └── lib/                          # 工具库
│       ├── utils.ts                  # 通用工具函数
│       ├── db.ts                     # 数据库配置
│       └── socket.ts                 # WebSocket 配置
├── prisma/
│   └── schema.prisma                 # 数据库模式
├── public/                           # 静态资源
├── examples/
│   └── websocket/                    # WebSocket 示例
├── .github/
│   └── workflows/
│       └── docker-publish.yml        # GitHub Actions 工作流
├── domain-test-cli.js               # 命令行测试工具
├── server.ts                        # 服务器入口文件
├── Dockerfile                        # 生产环境 Docker 镜像
├── Dockerfile.dev                    # 开发环境 Docker 镜像
├── docker-compose.prod.yml           # 生产环境编排
├── docker-compose.dev.yml            # 开发环境编排
├── .env.prod                         # 环境变量模板
├── .dockerignore                     # Docker 构建排除
├── docker-manager.sh                 # Docker 管理脚本
├── DOCKER-DEPLOYMENT.md             # Docker 部署指南
├── QUICK-START.md                   # 快速开始指南
├── next.config.ts                   # Next.js 配置
├── tailwind.config.ts              # Tailwind CSS 配置
├── tsconfig.json                    # TypeScript 配置
├── package.json                     # 项目依赖
└── README.md                        # 项目文档
```

## 🔄 更新日志

### v3.0.0 (当前版本)
- ✅ 完整的 Docker CI/CD 方案
- ✅ GitHub Actions 自动构建和推送到 Docker Hub
- ✅ 多平台支持（linux/amd64, linux/arm64）
- ✅ 优化的多阶段 Docker 镜像构建
- ✅ 完整的部署文档和管理脚本
- ✅ 项目精简和重构

### v2.3.0
- ✅ 修复中国地区DNS服务器排序问题，确保优先显示
- ✅ 优化检测速度，实现并发处理和超时控制
- ✅ 替换失效的DNS服务器（澳门、雅加达、马尼拉、悉尼）
- ✅ 修复SSL证书域名范围排版问题，支持智能分组显示
- ✅ 增加完整的部署指南，支持Windows和Linux多平台部署
- ✅ 完善README文档，添加详细的故障排除和性能优化

### v2.2.0
- ✅ 重构工具名称为"网站性能检测工具"
- ✅ 完善连接类型检测逻辑，支持CDN、直连、代理、混合类型
- ✅ 增加15+主流CDN提供商识别
- ✅ 添加检测置信度评估
- ✅ 提供详细的分析结果和建议
- ✅ 更新命令行工具和文档

### v2.1.0
- ✅ 修复SSL证书获取问题
- ✅ 修复性能时间分析统计缺陷
- ✅ 完善时间测量逻辑（DNS、TCP、SSL、TTFB、下载）
- ✅ 更新README为中文版本

### v2.0.0
- ✅ 支持自定义域名测试
- ✅ 增加更多检测数据（DNS、TCP、SSL、TTFB等）
- ✅ 重新设计Web界面，增加8个分析面板
- ✅ 更新命令行工具，支持更多参数
- ✅ 修复CDN检测逻辑，提高准确性
- ✅ 增加SSL证书信息检测
- ✅ 增加性能评级功能

### v1.0.0
- ✅ 基础CDN检测功能
- ✅ Web界面测试
- ✅ 命令行工具
- ✅ API接口

## 🤝 贡献

欢迎提交Issue和Pull Request来改进这个项目！

### 贡献指南
1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

### 开发规范
- 遵循 TypeScript 严格模式
- 使用 ESLint 和 Prettier 格式化代码
- 编写清晰的注释和文档
- 确保所有测试通过

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 📞 支持

如果您在使用过程中遇到问题或有改进建议，请：

1. 查看[故障排除](#-故障排除)部分
2. 查看 [Docker 部署指南](./DOCKER-DEPLOYMENT.md)
3. 搜索现有的 [GitHub Issues](https://github.com/233bit/website-performance-tool/issues)
4. 创建新的 Issue 描述问题

---

**项目地址**: https://github.com/233bit/website-performance-tool  
**Docker 镜像**: 233bit/website-performance-tool

---

**⭐ 如果这个项目对您有帮助，请给个 Star！**

---

**免责声明**: 本工具仅供学习和测试使用，请勿用于非法用途。使用者需自行承担使用风险。