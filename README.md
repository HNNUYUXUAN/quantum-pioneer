# 量子先锋：安徽创新之路 - 量子计算科普网站

## 项目简介
这是一个基于React+TypeScript的量子计算科普网站，展示安徽省在量子科技领域的创新成果，包含量子计算基础知识、量子门游戏和安徽量子科技成就展示等功能。

## 技术栈
- 前端：React 18, TypeScript, Tailwind CSS
- 构建工具：Vite
- 图表库：Recharts
- 动画库：Framer Motion

## 宝塔面板部署指南 (CentOS)

### 1. 服务器准备
1. 购买云服务器(CentOS 7/8)
2. 通过SSH连接服务器
3. 更新系统：
   ```bash
   yum update -y
   ```

### 2. 安装宝塔面板
1. 执行安装命令：
   ```bash
   yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
   ```
2. 安装完成后记录面板地址、用户名和密码
3. 登录宝塔面板，安装推荐套件(Nginx、MySQL等)

### 3. 环境配置
1. 在宝塔面板"软件商店"中安装：
   - Nginx (最新版)
   - Node.js (建议版本16+)
   - PM2管理器

2. 通过SSH安装项目依赖：
   ```bash
   # 安装pnpm
   npm install -g pnpm
   ```

### 4. 项目部署
1. 将项目代码上传到服务器(如/www/wwwroot/quantum)
2. 安装项目依赖：
   ```bash
   cd /www/wwwroot/quantum
   pnpm install
   ```
3. 构建生产环境代码：
   ```bash
   pnpm build
   ```
4. 构建完成后，文件会生成在dist目录

### 5. Nginx配置
1. 在宝塔面板添加站点
2. 配置域名和SSL证书
3. 修改Nginx配置：
   ```nginx
   server {
       listen 80;
       server_name yourdomain.com;
       root /www/wwwroot/quantum/dist;
       index index.html;
       
       location / {
           try_files $uri $uri/ /index.html;
       }
   }
   ```
4. 重启Nginx服务

### 6. 使用PM2管理进程
1. 通过PM2启动服务：
   ```bash
   pm2 serve /www/wwwroot/quantum/dist 3000 --spa
   ```
2. 设置开机启动：
   ```bash
   pm2 startup
   pm2 save
   ```

### 7. 安全优化
1. 配置防火墙规则
2. 设置定期备份
3. 配置HTTPS强制跳转
4. 启用Gzip压缩

### 8. 日常维护
1. 项目更新流程：
   ```bash
   git pull origin main
   pnpm install
   pnpm build
   pm2 restart all
   ```
2. 设置日志轮转
3. 监控服务器资源使用情况

## 常见问题

### 1. 访问显示空白页
- 检查Nginx配置是否正确
- 确认dist目录下有index.html
- 查看浏览器控制台是否有错误

### 2. 接口请求失败
- 检查API地址配置
- 确认跨域设置
- 查看网络连接

### 3. 性能优化建议
- 启用Nginx缓存
- 使用CDN加速静态资源
- 优化图片资源

## 项目结构
```
├── src
│   ├── components      # 公共组件
│   ├── pages           # 页面组件
│   ├── hooks           # 自定义Hook
│   └── styles          # 全局样式
├── public              # 静态资源
└── dist                # 构建输出
```

## 开发指南
1. 安装依赖：
   ```bash
   pnpm install
   ```
2. 启动开发服务器：
   ```bash
   pnpm dev
   ```
3. 访问 http://localhost:3000

## 贡献指南
欢迎提交Pull Request，请遵循现有代码风格。
