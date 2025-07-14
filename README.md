# DXScanGo v1.6.8 - 自动化XSS扫描框架

## 📋 项目简介

DXScanGo 是一款基于 Go 语言开发的高性能、全自动 XSS 漏洞扫描框架。集成了多种爬虫技术、AST 语法验证、智能探测等先进技术，可以高效准确地发现 Web 应用中的跨站脚本（XSS）漏洞。

## ✨ 核心特性

### 🕷️ 多引擎爬虫系统
- **Colly 爬虫**: 高性能网页抓取 + 智能目录遍历
- **Katana 爬虫**: 深度 JavaScript 分析和表单处理
- **GAU 引擎**: 历史 URL 数据挖掘（Wayback、CommonCrawl、OTX、URLScan）

### 🔍 智能检测技术
- **AST 语法验证**: 基于抽象语法树的精确上下文分析
- **智能无害探测**: 减少误报的渐进式检测策略
- **上下文感知**: 精确识别 HTML、JavaScript、CSS 等执行环境

### 🛠️ 高级功能
- **目录遍历扫描**: 智能字典选择 + 技术栈识别
- **JavaScript 分析**: 敏感信息提取 + API 端点发现
- **实时报告生成**: Markdown/HTML多格式输出
- **参数模糊测试**: 智能参数发现和反射验证
- **被动扫描**: 解决cookie token问题(测试阶段)
- **端口扫描**: 全端口扫描(测试阶段)

### 🚀 性能优化
- **并发扫描**: 可配置并发数，充分利用系统资源
- **智能去重**: 避免重复扫描相同目标
- **缓存机制**: 提升重复检测效率
- **超时控制**: 防止长时间阻塞

## 📦 安装配置

### 系统要求
- Go 1.19 或更高版本
- Windows/Linux/macOS 系统
- 至少 2GB 可用内存

## 📦 基础演示
```bash
.\dxscango.exe crawl -u https://example.com
```
爬虫+xss
<img width="1440" height="593" alt="image" src="https://github.com/user-attachments/assets/be75855d-f74f-4856-ab0a-2ca5ef591577" />

```bash
.\dxscango.exe -h
```
参数帮助
<img width="1029" height="252" alt="image" src="https://github.com/user-attachments/assets/006409a5-bc43-44fc-846d-3ca6a2fed83b" />

```bash
.\dxscango.exe xss -u https://example.com
```
单独运行xss
<img width="1010" height="333" alt="image" src="https://github.com/user-attachments/assets/6fc6e267-397c-45a6-ba84-6513051f49f8" />

报告生成
<img width="829" height="472" alt="image" src="https://github.com/user-attachments/assets/7aea92e8-ecf1-4fcf-a75a-dcf159bd664a" />

```bash
.\dxscango.exe dir -u https://example.com -e php
```
单独运行目录遍历
<img width="1442" height="740" alt="image" src="https://github.com/user-attachments/assets/5b6e7f03-325a-4bc9-bbf9-8522d7318b4a" />

报告生成
<img width="1367" height="947" alt="image" src="https://github.com/user-attachments/assets/f81a3fd6-258e-4400-a33a-d18526ec150c" />

```bash
.\dxscango.exe js -u https://example.com
```
单独运行js分析
<img width="1464" height="907" alt="image" src="https://github.com/user-attachments/assets/bbfe8144-50d6-419f-a5cf-6edf44708c6a" />
<img width="1317" height="942" alt="image" src="https://github.com/user-attachments/assets/82109193-e24d-4e0a-8523-094dabbe025e" />



### 注意
```bash
- 本程序为go编译的二进制,不要双击运行会闪退,命令行运行 dxscango.exe -h (win)
```

### 初始配置
1. **许可证激活**（首次运行）：
```bash
./dxscango crawl -u http://example.com（linux）
dxscango.exe crawl -u http://example.com (win)
# 按提示输入激活码：XXXX-XXXX-XXXX-XXXX
```

2. **license文件**：
程序会自动生成 `dxscango.license` license文件。 (不要删除,后续新版本直接复制同步即可)

## 🚀 快速开始

### 基础扫描
```bash
# 扫描单个URL
./dxscango crawl -u https://example.com (linux)
dxscango.exe crawl -u https://example.com (win)

# 从文件批量扫描
./dxscango crawl -f targets.txt (linux)
dxscango.exe crawl -f targets.txt(win)
```

### 被动扫描(测试阶段)
```bash
dxscango.exe proxy -p 9090 (win)(不指定-p 则默认为8080端口)
```
### 端口扫描(测试阶暂不支持C段)
```bash
dxscango.exe port -u ip/domain -p 1-65535 (全端口)
dxscango.exe port -f ip.txt -p 1-65535 (全端口)
-p 参数: 1-65535全端口 top1000只扫top场景端口 22,80,443,3389只扫指定端口
```

### 独立模块使用
```bash
# 纯XSS扫描（无爬虫）
./dxscango xss -u https://example.com/search?q=test
./dxscango xss -f targets.txt

# 目录遍历扫描
./dxscango dir -u https://example.com -e php(linux) / -e 指定语言类型
./dxscango dir -f targets.txt -e all (linux) / all 表示默认不指定全量
dxscango.exe dir -u https://0zqq.com -e php(win)

# JavaScript分析
./dxscango js -u https://example.com/app.js
./dxscango js -f targets.tx
```

### 2. 代码审计辅助
```bash
# 分析JavaScript文件中的敏感信息
./dxscango js -u https://app.com/assets/app.js 

# 目录遍历发现隐藏文件
./dxscango dir -u https://app.com -e all
```

### 3. 持续安全检测
```bash
# 定期扫描脚本
#!/bin/bash
./dxscango crawl -f production_urls.txt
# 结合CI/CD流程进行自动化检测
```

### 4. 漏洞验证
```bash
# 针对特定参数验证XSS
./dxscango xss -u "https://site.com/search?q=test&category=all"
```

### 1. 性能优化
```yaml
# 高性能配置示例
crawler:
  concurrency: 1000          # 提高并发数
colly:
  rate_limit:
    enable: false            # 关闭速率限制
gau:
  max_results_per_source: 5000 # 增加结果数量
```

### 2. 精度调优
```yaml
# 高精度配置
xss:
  min_confidence_score: 0.8   # 提高置信度阈值
param_fuzzing:
  enable: true                # 启用fuzz

```

### 3. 自定义字典
```bash
# 编辑参数字典
vim dicts/fuzz.txt
# 添加业务相关参数
echo "user_input" >> dicts/fuzz.txt
echo "search_term" >> dicts/fuzz.txt
```

### 4. 结果分析
```bash
# 提取高危漏洞
grep "Critical\|High" reports/xss_realtime_*.md

# 统计漏洞数量
grep "🚨 漏洞 #" reports/xss_realtime_*.md | wc -l

# 查看特定类型漏洞
grep "javascript" reports/xss_realtime_*.md
```

## ⚠️ 注意事项

### 法律合规
- ✅ 仅对授权目标进行扫描
- ✅ 遵守相关法律法规
- ❌ 禁止用于未授权渗透测试
- ❌ 禁止用于恶意攻击

### 技术限制
- 部分 WAF 可能阻拦扫描请求
- 复杂 JavaScript 应用可能需要人工验证
- 网络环境可能影响爬虫效果
- 大型站点建议分批扫描

### 性能建议
- 合理设置并发数避免目标服务器过载
- 使用代理池分散请求来源
- 定期清理临时文件和缓存
- 监控系统资源使用情况


📝 更新日志

v1.6.8

🛠️优化线程池
🛠️优化cookie注入

v-1.6-1.6.7

🔥新增被动扫描模式,(测试阶段)
🔥新增端口扫描模式(测试阶段)
🔥新增数据清洗功能
🔥优化xss ast抽象树分析

v1.5.1-1.6

🗂️目录遍历更新:
搭配XSS以及单独运行模式,字典自动选择,使用xss_dirs.txt
发现的路径自动加入XSS扫描队列,使用common_dirs.txt
专注于目录遍历漏洞发现并生成生成完整HTML报告
🛠️ xss引擎重大更新降低误报
🎯 colly爬虫优化,将会取更多url参数

v1.5.1

🛠️ 修复探测证据：只取核心证据
🔥 优化 JavaScript 引号逃逸检测
🎯 不同参数 XSS 去重避免报告重复

v1.5 

🚀 整体调试编译发布内测版
📋 持续收集用户意见进行优化

v1.4.9

🗂️ 优化目录遍历功能

v1.4.8

🎯 新增 JavaScript 深度分析器

v1.4.7

🧠 XSS 引擎 AST 语法全面优化

v1.4.6

🔧 XSS 引擎架构全量升级重构

v1.4.5

🚀 爬虫框架性能深度优化

v1.4.4

🎯 参数提取器集成 Fuzz 测试功能

v1.4.3

📝 新增调试日志配置
🧠 XSS 引擎智能探测升级
📊 报告输出优化

v1.4.2

🔧 爬虫输出智能管理
⚡ GAU 功能重构
📋 配置文件统一优化

v1.4.1

🎯 加入目录遍历功能
🗂️ 支持独立目录扫描
📚 字典检测优化

v1.4

🌟 置信度阈值系统重大更新
🔧 支持多场景配置

v1.3

🌟 XSS 引擎工作流程全新升级
🔍 多维度检测机制

v1.2.1

⚡ 评分规则算法更新
📊 报告输出详细化

v1.2

🎯 JS AST 分析功能上线
🔍 XSS 引擎独立运行

v1.1.1

🌟 XSS 引擎语义分析重大升级
🛡️ 无害探测机制

v1.0

🚀 四大爬虫框架完成
🔍 XSS 引擎扫描上线
📊 实时报告生成

## 📄 许可证

本项目采用商业许可证，使用前请确保已获得有效授权。

---

## 📄 关于开源
当版本更新幅度过大时,会选择性开源低版本供用户使用。

---

## 📊  查询授权

跳转:https://0zqq.com/dxscango
<img width="1052" height="502" alt="image" src="https://github.com/user-attachments/assets/a2e6f1fe-e2ff-4f29-b48f-5c05c8ab8bd7" />

---

**⚡ DXScanGo - 让XSS扫描更智能、更高效！**
