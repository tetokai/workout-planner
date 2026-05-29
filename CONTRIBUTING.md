# 贡献指南

感谢你对「🏋️ 训练计划」项目的兴趣！本文档将帮助你参与项目开发。

## 开发环境设置

### 1. 克隆仓库
```bash
git clone https://github.com/tetokai/workout-planner.git
cd workout-planner
```

### 2. 安装依赖
```bash
npm install
```

### 3. 启动本地开发服务器
```bash
npm run dev
```
然后访问 `http://localhost:8000`

## 项目结构

```
workout-planner/
├── index.html           # 主页面（包含HTML结构）
├── style.css           # 样式表
├── script.js           # 业务逻辑脚本
├── sw.js               # Service Worker（离线支持）
├── manifest.json       # PWA配置
├── plans/
│   └── default.json    # 默认训练计划
├── README.md           # 项目文档
├── CONTRIBUTING.md     # 本文件
├── DEVELOPMENT.md      # 开发指南
├── package.json        # 项目配置
├── .editorconfig       # 编辑器配置
├── .prettierrc         # 代码格式化配置
├── .eslintrc.json      # 代码检查配置
└── .gitignore          # Git忽略文件
```

## 代码规范

### JavaScript
- 使用单引号 `''`
- 每行代码最多 100 个字符
- 使用 `const` 和 `let`，避免 `var`
- 为所有函数添加注释说明其用途

### CSS
- 使用 2 空格缩进
- 相关选择器分组
- 按照 BEM 方法命名类名

### HTML
- 使用语义化标签
- 添加必要的 ARIA 属性
- 确保移动设备兼容性

### 代码检查
```bash
npm run lint      # 检查代码
npm run format    # 自动格式化
```

## 功能开发流程

1. **创建 Issue**
   - 描述功能需求或bug
   - 提供相关的上下文

2. **创建特性分支**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **提交更改**
   ```bash
   git add .
   git commit -m "feat: 功能描述"
   ```

4. **推送分支**
   ```bash
   git push origin feature/your-feature-name
   ```

5. **创建 Pull Request**
   - 清晰描述你的更改
   - 链接相关的 Issue
   - 确保没有冲突

## Commit 消息规范

使用约定式提交（Conventional Commits）：

- `feat:` 新功能
- `fix:` 修复bug
- `docs:` 文档变更
- `style:` 代码风格调整（不改变逻辑）
- `refactor:` 代码重构
- `perf:` 性能优化
- `test:` 测试变更

示例：
```
feat: 添加暗黑模式支持
fix: 修复计时器在iOS上的问题
docs: 更新README中的屏幕截图
```

## 测试

- 在多个浏览器上测试（Chrome、Firefox、Safari、Edge）
- 在移动设备上测试响应式设计
- 测试离线功能（PWA）
- 测试localStorage数据持久化

## 报告问题

提交Issue时，请包含：
- 问题描述
- 复现步骤
- 预期行为
- 实际行为
- 浏览器版本和操作系统
- 截图或录屏

## 性能注意事项

- 最小化DOM操作
- 使用事件委托
- 避免强制重排（layout thrashing）
- 使用requestAnimationFrame处理动画
- 定期测试 Lighthouse 性能评分

## 安全考虑

- 验证所有用户输入
- 使用HTTPS
- 避免将敏感数据存储在localStorage
- 定期更新依赖

## 获得帮助

- 查看 [DEVELOPMENT.md](DEVELOPMENT.md) 获取深度开发文档
- 在 Issues 中提问
- 查看现有的代码注释

---

感谢你的贡献！🎉
