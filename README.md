# 招标信息自动抓取系统 - Node.js服务器版本

## 🚀 功能特点

- ✅ **无头浏览器模式**: 基于Playwright，适合服务器环境运行
- ✅ **AI验证码识别**: 集成SiliconFlow大模型API自动识别验证码
- ✅ **SFTP自动上传**: 直接上传到静态站点，无需本地存储
- ✅ **智能去重机制**: 检查SFTP服务器文件，避免重复上传
- ✅ **智能分页爬取**: 自动识别翻页，完整抓取所有搜索结果
- ✅ **串行上传保证**: 确保每个文件都成功上传，不遗漏
- ✅ **增强重试机制**: 网络不稳定时自动重试，指数退避算法
- ✅ **服务器环境优化**: 适配无图形界面服务器和定时任务

## 📋 配置要求

### 必须配置的参数

1. **登录信息** (ServerConfig.LOGIN_CONFIG)
   ```javascript
   username: 'your_username',  // 招标网用户名
   password: 'your_password',  // 招标网密码
   ```

2. **AI验证码识别** (ServerConfig.CAPTCHA_CONFIG)
   ```javascript
   api_key: 'your_siliconflow_api_key',  // SiliconFlow API密钥
   ```

### 已配置的SFTP信息

```javascript
UPLOAD_CONFIG: {
    sftp: {
        host: '82.157.174.111',
        port: 2022,
        username: 'wenwenba2020_ftp',
        password: 'buyaolianQ10',
        remote_path: '/zhaobiaowang_filtered_pages/',
        web_base_url: 'http://82.157.174.111:10000/zhaobiaowang_filtered_pages/'
    }
}
```

## 🛠️ 使用方法

### 安装依赖
```bash
npm install playwright axios ssh2-sftp-client crypto
```

### 测试SFTP上传功能
```bash
node zhaobiaowang_spider_js.js --test-sftp
```

### 运行完整爬虫
```bash
node zhaobiaowang_spider_js.js
```

## 📊 处理流程

1. **初始化SFTP去重检查** - 获取服务器现有文件列表
2. **启动无头浏览器** - Playwright自动化控制
3. **自动登录** - AI识别验证码，自动填写表单
4. **导航到定制页面** - 进入个性化项目定制
5. **处理目标条件** - 默认处理条件04和05
6. **设置搜索时间** - 自动设置最近7天范围
7. **分页爬取结果** - 自动翻页，提取所有招标信息
8. **串行上传文件** - 逐个上传，确保不遗漏

## 🔧 高级配置

### 目标条件配置
```javascript
TARGET_CONDITIONS: {
    condition_ids: [4, 5],      // 要处理的定制条件编号
    search_days_back: 3,        // 搜索最近N天的数据
    pagination: {
        enabled: true,          // 是否启用分页爬取
        max_pages: 10,          // 最大分页数限制
        page_delay: 3000        // 页面间隔时间（毫秒）
    }
}
```

### 重试机制配置  
```javascript
UPLOAD_CONFIG: {
    max_retries: 5,             // 最大重试次数
    retry_delay: 2000,          // 重试间隔（毫秒）
    sftp: {
        upload_timeout: 60000,  // 上传超时时间
    }
}
```

## 📁 文件结构

爬取的文件将按以下格式命名：
```
{信息类型}_{发布日期}_{项目标题前30字符}_{序号}.html
```

## 🔍 故障排除

### SFTP连接失败
- 检查网络连接  
- 确认SFTPGo服务器地址和端口(2022)
- 验证用户名密码
- 检查SFTPGo用户权限设置

### 验证码识别失败  
- 检查SiliconFlow API密钥
- 确认API配额是否充足
- 网络连接是否稳定

### 登录失败
- 检查招标网用户名密码
- 确认账号状态正常
- 验证网站是否有变更

## 🎯 注意事项

1. **分页爬取**: 系统自动识别"下一页"按钮，完整抓取所有页面数据
2. **串行上传**: 系统确保文件逐个上传，避免并发冲突
3. **去重机制**: 自动跳过已存在的文件，节省时间和带宽
4. **错误恢复**: 单个文件失败不影响整体流程
5. **日志详细**: 提供详细的执行日志，便于调试

### 分页爬取功能

- **自动翻页**: 智能识别多种分页按钮样式（"下一页"、">"、数字链接等）
- **分页限制**: 默认最多爬取10页，可配置调整
- **容错机制**: 分页失败不影响已抓取数据的处理
- **统计信息**: 显示总页数、总条目数和处理成功率

## 📈 性能优化

- 使用文件列表缓存减少SFTP查询
- 指数退避算法优化重试策略
- 智能超时设置适应不同网络环境
- 内存去重减少重复处理