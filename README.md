# 🏋️ 训练计划 - 膝盖调整版

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/tetokai/workout-planner)](https://github.com/tetokai/workout-planner)
[![GitHub forks](https://img.shields.io/github/forks/tetokai/workout-planner)](https://github.com/tetokai/workout-planner)

一个专为膝盖康复设计的智能训练计划网页应用，具有精确计时、自动休息提醒和训练日志功能。

## ✨ 核心功能

- ⏱️ **精确计时系统**
  - 自动计时 + 组间休息
  - 倒计时/开始/暂停蜂鸣提示
  - 训练总时长追踪

- 📊 **智能进度管理**
  - 实时进度条显示
  - 组数/轮次显示
  - 动作完成状态追踪

- 📝 **训练日志**
  - 自动保存训练记录
  - 训练数据趋势图
  - 完成训练时记录步数、骑行、疲劳、睡眠、RIR和身体反馈
  - 按现有 Excel“训练日志”字段导出 UTF-8 CSV
  - JSON 日志备份和恢复

- ✏️ **在线编辑**
  - 轻松修改训练计划
  - 添加/删除训练日
  - 自定义动作参数

- 📥📤 **数据管理**
  - JSON 导入/导出
  - 云端同步支持
  - 完整的数据备份

- 🧩 **自定义训练**
  - 独立的“自定义训练”页面
  - 动作库按训练部位分组下拉选择，也可填写自定义动作
  - 分别设置动作组数、次数和倒计时时长
  - 保存后直接使用现有计时流程

- 💾 **数据持久化**
  - localStorage 自动保存进度
  - IndexedDB 日志存储
  - 离线模式支持

- 🔄 **循环训练支持**
  - 多轮训练循环
  - 轮间休息管理
  - 智能进度恢复

- 📱 **完全响应式**
  - 手机友好设计
  - 横屏竖屏适配
  - 触摸优化

- 🚀 **渐进式应用**
  - PWA 支持
  - 离线可用
  - 应用安装

## 🎯 训练安排

| 日期 | 内容 |
|------|------|
| 周一 | 上肢推力日 |
| 周三 | 下肢日 |
| 周四 | 背+核心日 |
| 周六 | 全身循环（3轮） |

## 🚀 快速开始

### 在线使用

访问 [GitHub Pages](https://tetokai.github.io/workout-planner) 直接使用（无需本地部署）

### 本地开发

**前置要求：**
- Node.js 16+
- npm 或 yarn

**安装步骤：**

```bash
# 1. 克隆仓库
git clone https://github.com/tetokai/workout-planner.git
cd workout-planner

# 2. 安装依赖
npm install

# 3. 启动开发服务器
npm run dev

# 4. 打开浏览器访问
# http://localhost:8000
```

### 一键部署

点击下方按钮可直接部署到 Vercel：

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/tetokai/workout-planner)

## 📖 使用指南

### 基础使用

1. **选择训练日**
   - 点击顶部标签选择要进行的训练日

2. **开始训练**
   - 点击"开始"按钮启动计时器
   - 点击"暂停"按钮暂停计时

3. **完成动作**
   - 计时器自动倒数
   - 动作完成后自动到下一个动作
   - 组间休息时可调整休息时间

4. **查看日志**
   - 点击"📓 训练日志"查看历史记录
   - 查看训练数据趋势

### 自定义计划

#### 编辑现有计划

1. 点击"✏️ 编辑"按钮
2. 修改计划名称或动作参数
3. 点击"💾 保存"保存更改

#### 导入自定义计划

1. 点击"📥 导入"按钮
2. 选择 JSON 格式的计划文件
3. 系统自动加载新计划

#### 导出计划

1. 点击"📤 导出"按钮
2. 下载 JSON 文件备份

### JSON 计划格式

```json
{
  "name": "我的训练计划",
  "notes": [
    { "label": "膝盖状态", "value": "右膝半月板损伤" },
    { "label": "注意事项", "value": "避免深蹲" }
  ],
  "days": {
    "周一": {
      "rounds": 1,
      "exercises": [
        {
          "name": "动作名称",
          "phase": "热身",
          "sets": "3组x10",
          "duration": 0,
          "weight": "8kg",
          "rest": 30,
          "groupRest": 60,
          "tips": "保持背部挺直",
          "demo": "https://www.youtube.com/watch?v=..."
        }
      ]
    }
  }
}
```

**字段说明：**

| 字段 | 类型 | 说明 |
|------|------|------|
| name | string | 计划名称 |
| notes | array | 重要提醒（可选） |
| days | object | 训练日数据 |
| phase | string | 动作阶段：热身/正式/循环/拉伸/休息 |
| sets | string | 组数和次数，如"3组x10" |
| duration | number | 动作时长（秒），为0则按sets计算 |
| weight | string | 使用的重量 |
| rest | number | 组间休息时间（秒） |
| groupRest | number | 动作间休息时间（秒） |
| tips | string | 动作技巧提示 |
| demo | string | 动作示范视频链接 |

## 🛠️ 开发指南

### 项目结构

```
workout-planner/
├── index.html           # 主页面
├── style.css           # 样式表
├── script.js           # 业务逻辑
├── sw.js               # Service Worker
├── manifest.json       # PWA配置
├── plans/              # 训练计划文件
│   └── default.json    # 默认计划
├── README.md           # 项目文档
├── CONTRIBUTING.md     # 贡献指南
├── DEVELOPMENT.md      # 开发指南
└── package.json        # 项目配置
```

### 命令行工具

```bash
# 启动开发服务器
npm run dev

# 代码检查
npm run lint

# 代码格式化
npm run format

# 构建（静态站点无需构建）
npm run build
```

### 代码风格

- 使用 ESLint 检查代码质量
- 使用 Prettier 格式化代码
- 遵循 Conventional Commits 提交规范

详见 [CONTRIBUTING.md](CONTRIBUTING.md) 和 [DEVELOPMENT.md](DEVELOPMENT.md)

## 🌍 浏览器支持

| 浏览器 | 版本 | 状态 |
|--------|------|------|
| Chrome | 90+ | ✅ 完全支持 |
| Firefox | 88+ | ✅ 完全支持 |
| Safari | 14+ | ✅ 完全支持 |
| Edge | 90+ | ✅ 完全支持 |
| IE | 11 | ❌ 不支持 |

## 📱 移动应用

### 安装为应用

1. 在手机浏览器打开本应用
2. 点击浏览器菜单→"安装应用"或"添加到主屏幕"
3. 应用会像原生应用一样运行

### 离线使用

- 应用首次加载后可离线使用
- 所有数据保存在本地设备上
- 支持后台运行

## 📊 训练数据

### 日志内容

每条日志记录包含：
- 日期、星期和日类型
- 训练内容、计划时长和实际时长
- 步数、骑行公里和完成度
- 疲劳、睡眠和 RIR/主观余力
- 训练后总体感受和备注

### 数据导出

- “导出 Excel 兼容 CSV”使用与项目 Excel“训练日志”相同的14列字段和顺序。
- 同一天有多次训练时，CSV 会合并为一天一行。
- CSV 使用 UTF-8 BOM，方便 Excel 直接打开中文。
- “备份 JSON”用于在设备之间迁移网页版原始日志，旧版日志仍可导入和显示。

## 🔒 隐私和数据安全

- ✅ 所有数据保存在本地设备上
- ✅ 不会向服务器上传任何个人数据
- ✅ 完全离线可用
- ✅ 用户完全控制自己的数据

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

### 贡献步骤

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

详见 [CONTRIBUTING.md](CONTRIBUTING.md)

## 📝 更新日志

### v1.0.0 (2024-01-15)
- ✨ 初始版本发布
- ✅ 完整计时功能
- ✅ 训练日志记录
- ✅ PWA离线支持
- ✅ 计划导入导出

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE)

## 🙏 致谢

- 感谢所有为项目做出贡献的开发者
- 感谢使用本应用的所有用户

## 📧 联系方式

- GitHub Issues: [提交问题](https://github.com/tetokai/workout-planner/issues)
- GitHub Discussions: [讨论区](https://github.com/tetokai/workout-planner/discussions)

---

**Made with ❤️ for fitness enthusiasts**

⭐ 如果对本项目有帮助，请给个Star！
