# 🚨 代码上传说明

## 主要文件状态

✅ **package.json** - 已上传完成  
✅ **package-lock.json** - 已上传完成  
✅ **README.md** - 已上传完成  

⚠️ **zhaobiaowang_spider_js.js** - 需要手动上传

## 主文件说明

`zhaobiaowang_spider_js.js` 是一个包含 **1790行代码** 的完整招标信息自动抓取系统，包含以下核心功能：

### 🎯 主要特性
- **无头浏览器自动化**: 基于Playwright，适合服务器环境
- **AI验证码识别**: 集成SiliconFlow大模型API (72B + 7B双模型备用)
- **智能分页爬取**: 自动识别翻页按钮，完整抓取所有结果
- **SFTP自动上传**: 直接上传到静态站点，支持去重检查
- **增强重试机制**: 指数退避算法，确保稳定性
- **串行上传保证**: 避免并发冲突，确保不遗漏

### 🔧 技术架构

#### 核心类和方法
```javascript
class ServerZhaobiaoSpider {
    // 浏览器管理
    async initBrowser()
    async autoLogin()
    async handleCaptchaAndLogin()
    
    // AI验证码识别 (多模型重试)
    async recognizeCaptchaWithAI()
    
    // 爬取核心功能
    async processCondition()
    async scrapeResults()
    async goToNextPage()
    async extractSearchResults()
    
    // SFTP上传管理
    async getRemoteFileList()
    async uploadContentToRemote()
    async testSFTPUpload()
}
```

#### 配置系统
```javascript
const ServerConfig = {
    LOGIN_CONFIG: { /* 登录配置 */ },
    CAPTCHA_CONFIG: { /* AI验证码配置 */ },
    TARGET_CONDITIONS: { /* 目标条件配置 */ },
    UPLOAD_CONFIG: { /* SFTP/FTP上传配置 */ },
    BROWSER_CONFIG: { /* 浏览器配置 */ }
}
```

### 📋 关键功能实现

1. **验证码识别增强**: 
   - 优先使用Qwen2.5-VL-72B模型
   - 失败时自动切换到7B模型
   - 3次递归重试机制
   - 填写后等待5秒稳定时间

2. **分页爬取智能化**:
   - 自动识别多种分页按钮样式
   - 最大10页限制（可配置）
   - 容错机制确保已抓取数据不丢失

3. **SFTP上传优化**:
   - 文件列表缓存减少查询
   - 指数退避重试策略
   - 串行上传避免冲突
   - 上传验证确保完整性

4. **服务器环境适配**:
   - 强制无头模式
   - 详细日志输出
   - 青龙面板优化
   - 内存去重机制

### 💡 手动上传步骤

由于GitHub API限制，请手动完成最后一步：

1. 下载本地的 `zhaobiaowang_spider_js.js` 文件
2. 在GitHub仓库中点击 "Add file" → "Upload files"
3. 拖拽上传该JavaScript文件
4. 提交信息：`🚀 上传主要爬虫脚本 - 完整功能实现`

### 🎉 完成后的项目结构

```
zhaobiaowang_spider_js/
├── README.md              # 项目说明文档
├── package.json           # 项目配置和依赖
├── package-lock.json      # 依赖锁定文件
├── zhaobiaowang_spider_js.js  # 主要爬虫脚本 (需手动上传)
└── CODE_UPLOAD.md         # 本文件 (上传说明)
```

### 🔗 相关链接

- **仓库地址**: https://github.com/wenwenba2020/zhaobiaowang_spider_js
- **技术栈**: Node.js + Playwright + SiliconFlow AI + SFTP
- **适用环境**: 青龙面板、服务器定时任务

---

*本项目已通过MCP GitHub工具自动创建和部分上传完成* ✨