# 开发指南

本文档提供深度的开发指导和架构说明。

## 架构概览

### 模块化设计

项目采用模块化架构，分为以下部分：

1. **UI 层** (`style.css`)
   - 响应式设计
   - 深色模式
   - 动画和过渡效果

2. **业务逻辑** (`script.js`)
   - 计时器管理
   - 状态管理
   - 数据持久化

3. **离线支持** (`sw.js`)
   - Service Worker
   - 缓存策略

## 关键模块说明

### 1. 计划管理 (Plan Storage)

```javascript
// 加载计划
const plan = loadPlan();

// 保存计划
savePlan();

// 加载默认计划
const defaultPlan = await loadDefaultPlan();
```

**数据结构：**
```json
{
  "name": "膝盖调整版训练计划",
  "days": {
    "周一": {
      "rounds": 1,
      "exercises": [
        {
          "name": "动作名称",
          "phase": "热身|正式|循环|拉伸|休息",
          "sets": "3组x10",
          "duration": 0,
          "weight": "8kg",
          "rest": 30,
          "tips": "动作技巧",
          "demo": "https://example.com/video"
        }
      ]
    }
  }
}
```

### 2. 计时器系统 (Timer System)

**三层计时：**
1. **训练总时长** - 整个训练过程计时
2. **动作计时** - 单个动作的时间
3. **组间休息** - 组与组之间的休息时间

**状态机：**
```
[初始] 
  ↓
[运行] → [计时中] → [倒计时] → [完成]
  ↓
[暂停]
```

### 3. 状态管理 (State Management)

**关键状态变量：**

```javascript
let currentDay = '';        // 当前训练日
let currentIndex = 0;       // 当前动作索引
let currentSet = 1;         // 当前组数
let totalSets = 1;          // 总组数
let currentRound = 1;       // 当前轮数
let totalRounds = 1;        // 总轮数
let timerRunning = false;   // 计时器是否运行
let doneExercises = Set();  // 已完成的动作
```

### 4. 数据持久化

**LocalStorage：**
- 训练计划
- 当前训练状态（4小时过期）
- 进度数据

**IndexedDB：**
- 训练日志（最多100条）
- 允许大容量存储
- 支持离线访问

### 5. 离线支持 (PWA)

**Service Worker 功能：**
- 缓存所有资源
- 离线页面
- 后台同步

## API 文档

### 核心函数

#### 计划管理

```javascript
// 加载用户自定义计划或默认计划
loadPlan() : Plan | null

// 保存当前计划
savePlan() : void

// 从服务器加载默认计划
async loadDefaultPlan() : Promise<Plan | null>
```

#### 计时器控制

```javascript
// 开始或暂停计时
toggleTimer() : void

// 启动计时器
startTimer() : void

// 停止计时器
stopTimer() : void

// 处理阶段完成
handlePhaseComplete() : void
```

#### UI 更新

```javascript
// 渲染标签
renderTabs() : void

// 渲染动作卡片
renderExercises() : void

// 更新控制按钮状态
updateControls() : void

// 更新进度条
updateProgress() : void
```

#### 日志管理

```javascript
// 获取所有日志
async getLogs() : Promise<LogEntry[]>

// 添加日志
async addLog(entry: LogEntry) : Promise<void>

// 导出日志
async exportLogs() : Promise<void>

// 导入日志
async importLogsFile() : Promise<void>
```

## 事件流

### 用户启动训练

```
1. 选择训练日 → switchDay()
2. 点击"开始" → toggleTimer()
3. 加载计划 → loadPlan()
4. 渲染UI → renderExercises()
5. 启动计时 → startTimer()
```

### 完成一个动作

```
1. 计时器倒数到0 → handlePhaseComplete()
2. 检查是否有多组 → 如是，显示休息
3. 组间休息完成 → 继续下一组
4. 全部组完成 → completeExercise()
5. 继续下一动作 → navExercise(1)
```

### 训练完成

```
1. 最后一个动作完成 → showComplete()
2. 用户输入训练日志
3. 保存日志 → addLog()
4. 重置状态 → resetAll()
```

## 性能优化

### 已实现的优化

1. **虚拟列表** - 只渲染可见的动作卡片
2. **防抖** - 定时保存状态（每30秒）
3. **缓存** - Service Worker缓存静态资源
4. **懒加载** - 动作详情按需展开
5. **事件委托** - 使用事件冒泡简化事件处理

### 可进一步优化的方向

- 使用 Web Workers 处理复杂计算
- 图表渲染优化
- 内存泄漏检测
- 长列表虚拟滚动

## 浏览器兼容性

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ⚠️ IE 11 不支持

## 测试清单

### 功能测试

- [ ] 计时器准确度
- [ ] 组间休息功能
- [ ] 轮次循环
- [ ] 日志保存和导出
- [ ] 计划导入/导出
- [ ] 离线模式

### 兼容性测试

- [ ] Desktop 浏览器
- [ ] Mobile 浏览器
- [ ] 平板设备
- [ ] 不同分辨率

### 性能测试

- [ ] Lighthouse 分数 > 90
- [ ] 首屏加载时间 < 2s
- [ ] 计时器延迟 < 100ms
- [ ] 内存使用稳定

## 常见问题

### Q: 如何添加新的训练日？
A: 点击"编辑"按钮，使用"添加训练日"功能。

### Q: 如何导入自定义训练计划？
A: 点击"导入"按钮，选择JSON文件。

### Q: 日志存储在哪里？
A: 日志存储在 IndexedDB 中，支持100条历史记录。

### Q: 如何实现响应式设计？
A: 使用 CSS Media Queries 和 flexbox/grid 布局。

## 调试技巧

### 查看存储的数据

```javascript
// 查看计划
console.log(JSON.parse(localStorage.getItem('knee_workout_plan')))

// 查看状态
console.log(JSON.parse(localStorage.getItem('knee_workout_state')))

// 查看IndexedDB
db.transaction('logs').objectStore('logs').getAll()
```

### 清空所有数据

```javascript
localStorage.clear()
indexedDB.deleteDatabase('knee_workout_db')
```

## 贡献流程

1. Fork 项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

---

祝开发愉快！如有问题，欢迎提交 Issue。
