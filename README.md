# 智能减肥追踪系统 - 项目文档

## 📋 项目概述

一个基于纯前端的减肥追踪应用，支持本地存储和云端同步，帮助用户记录每日饮食、运动，科学管理体重。

**项目地址：** https://github.com/xxyysss/my-web-site
**在线演示：** https://xxyysss.github.io/my-web-site/
**本地文件：** `C:\Users\Public\index.html`

---

## 🎯 核心功能

### 1. 用户权限管理
- **只读模式（访客）**：默认模式，只能查看数据，无法编辑
- **主人模式**：可以添加、修改、删除所有数据
- **切换方法**：在浏览器控制台执行 `localStorage.setItem('isOwner', 'true'); location.reload();`

### 2. 个人信息管理
- 记录身高、体重、年龄、性别、目标体重
- 自动计算 BMI 指数和基础代谢率（BMR）
- 使用 Mifflin-St Jeor 公式计算 BMR

### 3. 饮食记录
- 内置 60+ 常见中国食物热量数据库
- 支持搜索食物自动计算热量
- 支持手动输入热量
- 分类记录：早餐、午餐、晚餐、加餐

### 4. 运动记录
- 多种运动类型：步行、跑步、骑行、游泳、瑜伽、力量训练
- 根据体重、运动类型和时长自动计算消耗
- 步行模式支持步数输入
- 支持手动输入消耗热量

### 5. 数据统计
- 今日热量摄入/消耗/净热量统计
- 热量摄入进度条
- 历史记录表格（按日统计）
- 自动判断每日减肥/增重/维持状态
- 累计统计数据（8个关键指标）

### 6. 云端同步（Firebase）
- 数据自动保存到 Firebase Realtime Database
- 多设备实时同步
- 数据持久化存储

---

## 🛠️ 技术栈

### 前端技术
- **HTML5** - 页面结构
- **CSS3** - 样式设计（渐变色、响应式布局）
- **Vanilla JavaScript** - 业务逻辑（无框架）

### 数据存储
- **localStorage** - 本地浏览器存储
- **Firebase Realtime Database** - 云端数据库

### 部署平台
- **GitHub Pages** - 静态网页托管

---

## ⚙️ Firebase 配置

### 项目信息
- **项目名称：** weight-tracker-xyz123
- **数据库位置：** asia-southeast1（新加坡）
- **数据库地址：** https://weight-tracker-xyz123-default-rtdb.asia-southeast1.firebasedatabase.app/

### 配置代码
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyBPIIYcArUWGYtYmcH-GHA4iXkX5u3zl_g",
  authDomain: "weight-tracker-xyz123.firebaseapp.com",
  databaseURL: "https://weight-tracker-xyz123-default-rtdb.asia-southeast1.firebasedatabase.app/",
  projectId: "weight-tracker-xyz123",
  storageBucket: "weight-tracker-xyz123.firebasestorage.app",
  messagingSenderId: "1094474791239",
  appId: "1:1094474791239:web:74d7df7eb65ba5c15bf462"
};
```

### 数据库安全规则
```javascript
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

---

## 📂 文件结构

```
C:\Users\Public\
├── index.html              # 主程序文件（完整应用）
├── README.md              # 项目说明文档（本文件）
├── weight-loss-tracker.html # 原始文件（已重命名为 index.html）
└── 部署相关文件...
```

---

## 🔑 重要代码片段

### 1. 切换主人模式
```javascript
// 在浏览器控制台执行
localStorage.setItem('isOwner', 'true');
location.reload();
```

### 2. 切换回访客模式
```javascript
localStorage.removeItem('isOwner');
location.reload();
```

### 3. 清除所有本地数据（谨慎使用）
```javascript
localStorage.clear();
location.reload();
```

---

## 🐛 常见问题排查

### 问题 1：数据刷新后丢失

**症状：** 添加数据后，刷新页面数据消失

**可能原因：**
- Firebase 连接失败
- 数据库规则限制

**解决方法：**
1. 打开浏览器控制台（F12），查看是否有错误信息
2. 检查 Firebase 数据库规则是否允许读写
3. 确认 databaseURL 配置正确

### 问题 2：Firebase 连接失败

**症状：** 控制台提示 "Firebase 初始化失败"

**解决方法：**
1. 检查 firebaseConfig 配置是否完整
2. 确认 Firebase 项目已启用 Realtime Database
3. 检查数据库 URL 是否正确

### 问题 3：多设备数据不同步

**症状：** 电脑录入的数据，手机上看不到

**可能原因：**
- 使用了不同的用户账号
- Firebase 数据未正确保存

**解决方法：**
1. 确保所有设备使用同一个网站地址
2. 检查控制台是否有数据同步错误
3. 确认 master 用户账号固定

### 问题 4：控制台报错 "Cannot read properties of undefined"

**症状：** 添加数据时报错

**解决方法：**
- 这是已修复的问题，确保使用最新代码
- 检查 Firebase 返回的数据格式

---

## 📊 数据结构

### 用户信息
```javascript
{
  name: "姓名",
  gender: "male", // 或 "female"
  age: 25,
  height: 170,
  weight: 65,
  targetWeight: 60
}
```

### 饮食记录
```javascript
{
  foods: [
    {
      id: 1712345678901,
      name: "米饭",
      amount: 100,
      calories: 116,
      mealType: "lunch", // breakfast/lunch/dinner/snack
      timestamp: "2026-03-30T10:00:00.000Z"
    }
  ]
}
```

### 运动记录
```javascript
{
  exercises: [
    {
      id: 1712345678902,
      type: "步行",
      duration: 30,
      calories: 100,
      steps: 3000,
      timestamp: "2026-03-30T12:00:00.000Z"
    }
  ]
}
```

---

## 🧮 计算公式

### BMI 计算
```
BMI = 体重 / (身高/100)²
```

### BMI 状态
- < 18.5：偏瘦
- 18.5 - 24：正常
- 24 - 28：偏胖
- ≥ 28：肥胖

### 基础代谢率（BMR）- Mifflin-St Jeor 公式
```
男性：BMR = 10 × 体重 + 6.25 × 身高 - 5 × 年龄 + 5
女性：BMR = 10 × 体重 + 6.25 × 身高 - 5 × 年龄 - 161
```

### 净热量
```
净热量 = 摄入热量 - 运动消耗 - 基础代谢
```

### 预计体重变化
```
体重变化 = 净热量 / 7700  （7700 kcal ≈ 1 kg 脂肪）
```

### 运动消耗计算
```
消耗 = 运动系数 × 时长 × 体重
```

**运动系数：**
- 步行：0.045 kcal/分钟/kg
- 跑步：0.12 kcal/分钟/kg
- 骑行：0.08 kcal/分钟/kg
- 游泳：0.11 kcal/分钟/kg
- 瑜伽：0.04 kcal/分钟/kg
- 力量训练：0.06 kcal/分钟/kg

---

## 🔄 如何更新代码

### 方法一：修改本地文件后推送
```bash
cd C:\Users\Public
# 修改 index.html
git add index.html
git commit -m "描述你的修改"
git push
```

### 方法二：直接在 GitHub 网页编辑
1. 打开 https://github.com/xxyysss/my-web-site
2. 点击 `index.html` 文件
3. 点击右上角铅笔图标编辑
4. 修改完成后提交

GitHub Pages 会自动重新部署（1-2分钟生效）

---

## 📱 使用建议

### 主人模式使用流程
1. 打开网站
2. F12 打开控制台
3. 粘贴：`localStorage.setItem('isOwner', 'true'); location.reload();`
4. 填写个人信息
5. 开始记录饮食和运动
6. 数据自动保存到云端

### 访客模式使用流程
1. 打开网站
2. 默认就是访客模式
3. 只能查看数据
4. 无法编辑

### 多设备使用
- **电脑录入**：用主人模式添加数据
- **手机查看**：用访客模式查看数据
- **数据自动同步**：无需手动操作

---

## 🔒 隐私说明

- 所有数据存储在 Firebase 云端（Google）
- 使用 HTTPS 加密传输
- 浏览器本地也有数据缓存
- 建议定期备份 Firebase 数据库
- 主人模式修改数据需要浏览器控制台（隐藏入口）

---

## 📞 获取帮助时提供的信息

如果需要后续帮助，请提供以下信息：

### 基础信息
```
项目名称：智能减肥追踪系统
文件位置：C:\Users\Public\index.html
GitHub仓库：https://github.com/xxyysss/my-web-site
在线地址：https://xxyysss.github.io/my-web-site/
```

### 遇到的问题
- 描述具体症状
- 提供浏览器控制台的错误信息（如果有）
- 提供操作步骤

---

## 🎓 技术参考

### Firebase SDK
```html
<!-- Firebase App SDK -->
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
<!-- Firebase Realtime Database -->
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
```

### Firebase 控制台
- 项目地址：https://console.firebase.google.com
- 项目名称：weight-tracker-xyz123
- 数据库地址：https://weight-tracker-xyz123-default-rtdb.asia-southeast1.firebasedatabase.app/

---

## 📝 更新日志

### 2026-03-30
- ✅ 添加 Firebase 云端同步功能
- ✅ 实现只读/主人权限控制
- ✅ 修复数据加载时的 undefined 错误
- ✅ 完善项目文档

### 初始版本
- ✅ 基础功能：饮食记录、运动记录
- ✅ BMI 和 BMR 计算
- ✅ 本地存储（localStorage）
- ✅ 历史数据统计
- ✅ 响应式设计

---

## 🚀 部署信息

### GitHub Pages
- **仓库：** https://github.com/xxyysss/my-web-site
- **分支：** main
- **源目录：** root (/)
- **部署地址：** https://xxyysss.github.io/my-web-site/

### 自动部署
- 推送代码到 GitHub main 分支后
- GitHub Pages 自动检测并部署
- 通常 1-2 分钟生效

---

## 📚 相关资源

- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [Firebase Realtime Database 文档](https://firebase.google.com/docs/database)
- [MDN Web 开发文档](https://developer.mozilla.org/zh-CN/docs/Web)

---

**文档创建时间：** 2026-03-30
**最后更新：** 2026-03-30