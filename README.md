# Auto-Tutor: 一键批量套磁
一键向目标导师群发送陶瓷邮件，邮件内容基于你的简历和导师的介绍由LLM生成，支持任意LLMs服务商的api，推荐白嫖硅基流动的免费api！

您可以随时提交您的改进版本进main分支，欢迎共创，共同打造智能化学术申请！

## 更新日志
- `2025.9.5` 新增代理，支持科学上网，便于使用谷歌邮箱
- `2025.9.4` 支持Gemini API接口

## 常见担心
**您可能的担心1：使用门槛？**

零代码即可使用！直接在前端点点点即可！

![前端示意图](https://github.com/Zhanli-Li/Auto-Tutor/blob/main/preview.png)
**您可能的担心2：害怕生成的陶瓷信有问题？**

可进行复核编辑！

![可进行人工复核](https://github.com/Zhanli-Li/Auto-Tutor/blob/main/edit.png)

**您可能的担心3：找不到套磁记录？**

本地自动存套磁记录log！

![log](https://github.com/Zhanli-Li/Auto-Tutor/blob/main/email_log.png)

**您可能的担心4：想自定义提示词实现一些套磁信的风格和内容？**

支持自定义语言风格提示词！

![自定义语言风格](https://github.com/Zhanli-Li/Auto-Tutor/blob/main/info.png)

如果您觉得有用，可以点亮star支持一下！

## 快速启动服务

### 一键启动（推荐）
```bash
# 转到你系统上项目地址
cd project_path

# 安装最新版本的multer
npm install multer@latest

# 然后安装其他依赖
npm install

#启动服务
npm start
```
启动脚本会自动完成：
- 检查 Node/npm
- 安装依赖（触发 postinstall 的 install.js）
- 生成 .env（若不存在则从 .env.example 复制）
- 创建 uploads 与 log 目录
- 以生产模式启动服务（默认端口 3000）

### 启动成功标志
```
[2024-01-XX] [INFO] 服务器启动成功
[2024-01-XX] [INFO] 端口: 3000
[2024-01-XX] [INFO] 环境: production
[2024-01-XX] [INFO] 日志级别: info
[2024-01-XX] [INFO] 上传目录: uploads
[2024-01-XX] [INFO] 速率限制: 10 requests per 900000ms
[2024-01-XX] [INFO] 服务器运行在 http://localhost:3000
```

### 访问系统
```bash
# 在浏览器中打开
http://localhost:3000/tutor_email_system.html
```
## 维护团队
我们团队来自于北京大学,清华大学,中国科学院大学自动化所,中国科学技术大学,南京大学,福州大学,大连海事大学,中南财经政法大学.

他们分别是:
- [李展利 中南财经政法大学](https://zhanli-li.github.io/)
- [刘朝阳 大连海事大学](https://github.com/NanaseAsahi/)
- [杨鹏晖 清华大学](https://github.com/yph22/)
- [华英凡 中国科学技术大学](https://sui1234bian.github.io/)
- [汤家福 南京大学](https://github.com/kevin236-max)
- [赵俊杰 合肥工业大学](https://k5urum1z3.github.io/)
- 更新中...

## SMTP邮箱配置（以下非开发者可以不用看，直接在前文启动web中点点点）

### QQ邮箱配置（推荐）

1. **开启SMTP服务**
```
登录 https://mail.qq.com
设置 → 账户 → POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务
开启 "IMAP/SMTP服务"
```

2. **获取授权码**
```
点击 "生成授权码"
发送短信验证
保存16位授权码（非QQ密码）
```

3. **配置参数**
```
SMTP服务器: smtp.qq.com
SMTP端口: 587
加密方式: STARTTLS
用户名: 完整QQ邮箱地址
密码: 16位授权码
```

### 其他邮箱配置

#### 163邮箱
```
SMTP服务器: smtp.163.com
SMTP端口: 25 (非加密) / 465 (SSL) / 994 (SSL)
用户名: 完整163邮箱地址
密码: 邮箱授权码
```

#### Gmail
```
SMTP服务器: smtp.gmail.com
SMTP端口: 587 (TLS) / 465 (SSL)
用户名: 完整Gmail地址
密码: 应用专用密码
注意: 需要开启两步验证并生成应用密码
```

#### Outlook/Hotmail
```
SMTP服务器: smtp-mail.outlook.com
SMTP端口: 587
加密方式: STARTTLS
用户名: 完整Outlook邮箱地址
密码: 邮箱密码或应用密码
```

#### 企业邮箱
```
# 腾讯企业邮箱
SMTP服务器: smtp.exmail.qq.com
SMTP端口: 587 / 465

# 阿里云企业邮箱
SMTP服务器: smtp.mxhichina.com
SMTP端口: 25 / 465
```

## 系统变量配置（可不设置）

### 编辑.env文件

```bash
# 使用文本编辑器打开.env文件
nano .env
# 或者
vim .env
# 或者使用任何文本编辑器
```

### 关键配置项说明

```env
# 服务器端口（默认3000）
PORT=3000

# 运行环境（development/production）
NODE_ENV=production

# 速率限制：15分钟内最多10次请求
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=10

# 文件上传限制：最大10MB
MAX_FILE_SIZE_MB=10
ALLOWED_FILE_TYPES=application/pdf

# 邮件内容限制
MAX_EMAIL_CONTENT_LENGTH=50000
MAX_EMAIL_SUBJECT_LENGTH=200

# 网页抓取超时：30秒
FETCH_TIMEOUT_MS=30000
MAX_CONTENT_SIZE_MB=5

# 日志级别：error/warn/info/debug
LOG_LEVEL=info
```


## 核心功能

- **邮件发送**: 基于SMTP协议的安全邮件发送，支持附件
- **导师管理**: 单个添加和CSV批量导入导师信息
- **网页抓取**: 自动获取导师个人主页内容
- **文件上传**: PDF简历附件上传（最大10MB）
- **日志系统**: 四级日志（error/warn/info/debug）

## 系统要求

- **Node.js**: >= 14.0
- **npm**: >= 6.0
- **内存**: >= 512MB
- **磁盘**: >= 100MB可用空间
- **网络**: 需要访问SMTP服务器和目标网站

## 项目结构

```
tutor-email-system/
├── tutor_email_system.html    # 前端界面文件
├── email_server.js            # Express后端服务器
├── package.json               # 项目依赖和脚本配置
├── install.js                 # 自动安装脚本
├── .env.example              # 环境变量配置模板
├── uploads/                  # 文件上传目录（自动创建）
└── README.md                 # 项目文档
```

## 系统说明

### API接口说明

#### 1. 邮件发送接口
```http
POST /api/send-email
Content-Type: application/json

{
  "to": "professor@university.edu",
  "subject": "邮件主题",
  "body": "邮件正文",
  "senderEmail": "your@email.com",
  "senderPassword": "授权码",
  "smtpServer": "smtp.qq.com",
  "smtpPort": "587",
  "attachment": "base64编码的文件内容（可选）",
  "attachmentName": "resume.pdf（可选）"
}
```

#### 2. 网页内容抓取接口
```http
POST /api/fetch-website
Content-Type: application/json

{
  "url": "https://professor-homepage.com"
}
```

#### 3. 文件上传接口
```http
POST /api/upload
Content-Type: multipart/form-data

file: [PDF文件]
```

### 前端操作流程

#### 1. 邮箱配置
```javascript
// 在前端界面填写SMTP配置
const smtpConfig = {
  senderEmail: 'your@qq.com',
  senderPassword: '16位授权码',
  smtpServer: 'smtp.qq.com',
  smtpPort: '587'
};
```

#### 2. 导师信息管理

**单个添加**：
- 姓名：导师真实姓名
- 邮箱：有效的学术邮箱地址
- 学校：完整的学校名称
- 个人主页：可访问的URL（用于内容抓取）

**CSV批量导入格式**：
```csv
姓名,邮箱,学校,个人主页
Dr. Zhang,zhang@tsinghua.edu.cn,清华大学,https://www.tsinghua.edu.cn/zhang
Prof. Li,li@pku.edu.cn,北京大学,https://www.pku.edu.cn/li
```

#### 3. 文件上传要求
- **格式限制**：仅支持PDF格式
- **大小限制**：最大10MB
- **命名建议**：使用英文文件名，避免特殊字符

#### 4. 邮件发送流程
1. **配置验证**：系统自动验证SMTP连接
2. **内容抓取**：获取导师主页内容（超时30秒）
3. **邮件组装**：合并个人信息、抓取内容和附件
4. **批量发送**：遵循速率限制（15分钟内最多10封）
5. **状态反馈**：实时显示发送结果和错误信息

## 故障排除

### 环境问题

#### 1. Node.js安装问题
```bash
# 检查Node.js是否正确安装
node --version
npm --version

# 如果提示"命令未找到"或"不是内部命令"
# Windows: 重新安装Node.js并确保添加到PATH
# macOS/Linux: 检查环境变量
echo $PATH | grep node
```

#### 2. 依赖安装失败
```bash
# 清理npm缓存
npm cache clean --force

# 删除node_modules重新安装
rm -rf node_modules package-lock.json
npm install

# 使用淘宝镜像（中国用户）
npm config set registry https://registry.npmmirror.com
npm install
```

#### 3. 端口占用问题
```bash
# 检查端口占用
# Windows
netstat -ano | findstr :3000
taskkill /PID <进程ID> /F

# macOS/Linux
lsof -ti:3000
kill -9 $(lsof -ti:3000)

# 或者修改.env文件使用其他端口
PORT=3001
```

### 服务器问题

#### 4. 服务器启动失败
```bash
# 检查错误日志
node email_server.js

# 常见错误及解决方案：
# Error: Cannot find module 'xxx'
npm install

# Error: EADDRINUSE (端口占用)
# 修改PORT环境变量或杀死占用进程

# Error: EACCES (权限不足)
# Linux/macOS: sudo node email_server.js
# 或修改端口到1024以上
```

#### 5. 文件上传问题
```bash
# 检查uploads目录权限
ls -la uploads/

# 创建目录并设置权限
mkdir -p uploads
chmod 755 uploads

# Windows用户检查目录是否存在
dir uploads
md uploads
```

### 邮件发送问题

#### 6. SMTP认证失败
```javascript
// 常见错误码及解决方案
// 535 Authentication failed
// - 检查邮箱地址和授权码
// - 确认SMTP服务已开启

// 550 Mailbox not found
// - 检查收件人邮箱地址
// - 确认邮箱域名正确

// 421 Too many connections
// - 降低发送频率
// - 检查速率限制配置
```

#### 7. 网页抓取失败
```bash
# 测试网络连接
curl -I https://target-website.com

# 检查DNS解析
nslookup target-website.com

# 常见问题：
# - 网站需要登录：无法抓取受保护内容
# - 反爬虫机制：网站阻止自动访问
# - 网络超时：增加FETCH_TIMEOUT_MS值
# - SSL证书问题：检查HTTPS网站证书
```

### 性能优化

#### 8. 内存使用优化
```bash
# 监控内存使用
# Linux/macOS
top -p $(pgrep node)

# Windows
tasklist | findstr node.exe

# 优化建议：
# - 限制并发邮件发送数量
# - 定期清理临时文件
# - 调整LOG_LEVEL为warn或error
```

#### 9. 网络性能优化
```env
# 调整超时设置
FETCH_TIMEOUT_MS=15000
MAX_CONTENT_SIZE_MB=2

# 限制请求频率
RATE_LIMIT_WINDOW_MS=600000
RATE_LIMIT_MAX_REQUESTS=5
```

### 调试技巧

#### 10. 启用详细日志
```env
# 修改.env文件
LOG_LEVEL=debug
NODE_ENV=development
```

#### 11. 手动测试API
```bash
# 使用curl测试邮件发送
curl -X POST http://localhost:3000/api/send-email \
  -H "Content-Type: application/json" \
  -d '{
    "to": "test@example.com",
    "subject": "测试邮件",
    "body": "这是一封测试邮件",
    "senderEmail": "your@qq.com",
    "senderPassword": "授权码",
    "smtpServer": "smtp.qq.com",
    "smtpPort": "587"
  }'

# 测试网页抓取
curl -X POST http://localhost:3000/api/fetch-website \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com"}'
```

## 安全配置

### 1. 环境变量安全
```env
# .env文件权限设置
# Linux/macOS
chmod 600 .env

# 不要将.env文件提交到版本控制
echo ".env" >> .gitignore
```

### 2. SMTP凭据保护
```javascript
// 使用授权码而非登录密码
const smtpConfig = {
  user: process.env.SMTP_USER,
  pass: process.env.SMTP_AUTH_CODE, // 16位授权码
  host: process.env.SMTP_HOST,
  port: process.env.SMTP_PORT,
  secure: false, // 使用STARTTLS
  requireTLS: true
};
```

### 3. 文件上传安全
```javascript
// 服务器端文件类型验证
const allowedMimeTypes = ['application/pdf'];
const maxFileSize = 10 * 1024 * 1024; // 10MB

// 文件名安全处理
const sanitizeFilename = (filename) => {
  return filename.replace(/[^a-zA-Z0-9.-]/g, '_');
};
```

### 4. 速率限制配置
```env
# 防止滥用的速率限制
RATE_LIMIT_WINDOW_MS=900000  # 15分钟
RATE_LIMIT_MAX_REQUESTS=10   # 最多10次请求
```

### 5. 网络安全建议
- 仅在可信网络环境下运行
- 使用防火墙限制访问端口
- 定期更新Node.js和依赖包
- 监控系统日志异常活动


## 许可证

MIT License

## 免责声明

本系统仅供学术交流和研究使用。使用者应当：

1. 遵守相关法律法规和学术道德规范
2. 尊重邮件接收者的隐私权
3. 避免发送垃圾邮件或进行骚扰行为
4. 对使用本系统产生的任何后果承担责任

开发者不对使用本系统造成的任何直接或间接损失承担责任。
