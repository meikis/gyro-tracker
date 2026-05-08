# Gyro Tracker — 运动姿态监测

一个纯前端 H5 应用，利用手机降罢仪（Gyroscope）和加速度计（Accelerometer）实时监测手机的运动轨迹、姿态角度与估算移动距离，并以动画方式可视化展示。

---

## 预览

- **设计风格**：暗色科幻 HUD 风格，采用 `Orbitron` + `JetBrains Mono` 字体组合
- **3D 姿态模型**：CSS 3D 手机实时跟随降罢仪旋转
- **轨迹地图**：Canvas 绘制俯视图运动轨迹，带网格与发光路径
- **实时数据**：加速度、旋转速率、方向角、估算速度与距离
- **波形可视化**：各数据面板底部带动态条

---

## 功能特性

| 功能 | 说明 |
|------|------|
| 实时姿态 | 通过 `DeviceOrientationEvent` 获取 alpha / beta / gamma 三轴角度 |
| 加速度监测 | 通过 `DeviceMotionEvent` 获取线性加速度（不含重力） |
| 惯性导航 | 对加速度二次积分估算位移，带阈值过滤与速度衰减抑制漂移 |
| 轨迹绘制 | Canvas 绘制实时运动轨迹，带指向箭头 |
| 零点校准 | 一键扣除静态偏移，减少待机漂移 |
| 一键重置 | 清空轨迹与积分数据 |
| iOS 兼容 | 自动调用 `DeviceOrientationEvent.requestPermission()` |

---

## 技术栈

- **HTML5** — 结构与语义化标签
- **CSS3** — 暗色主题、CSS 变量、3D 变换、动画
- **Vanilla JavaScript** — 无框架依赖，直接调用浏览器原生 API
- **Canvas 2D** — 轨迹绘制与数据可视化

---

## 文件结构

```
gyro-tracker/
├── index.html    # 单文件完整应用（HTML + CSS + JS）
└── README.md     # 项目说明
```

---

## 本地运行

由于降罢仪 API 需要安全上下文（HTTPS 或 localhost），本地测试建议使用 HTTPS 或在支持的环境下运行。

### 方式一：直接打开（可能受限于浏览器安全策略）

直接用浏览器打开 `index.html`。

### 方式二：本地 HTTP 服务

```bash
# 进入项目目录
cd gyro-tracker

# 启动本地服务
python3 -m http.server 8765
```

然后在同一局域网的手机上访问：`http://<电脑IP>:8765`

> 注意：iOS Safari 可能要求 HTTPS 才能授权传感器。

---

## 部署

推荐部署到以下静态托管平台（免费、自动 HTTPS）：

- [GitHub Pages](https://pages.github.com/)
- [Vercel](https://vercel.com/)
- [Netlify](https://www.netlify.com/)
- [Cloudflare Pages](https://pages.cloudflare.com/)

部署方式：将 `index.html` 上传至任意静态托管服务，手机打开即可使用。

---

## 使用说明

1. 手机浏览器打开页面
2. 点击 **"开启传感器权限"** 按钮（iOS 需要此步骤）
3. 移动手机，观察 3D 模型、数据面板与轨迹变化
4. 如果静止时有漂移，点击 **"零点校准"** 扣除偏移
5. 点击 **"重置轨迹"** 清空数据

---

## 兼容性

| 平台 | 支持情况 |
|------|---------|
| iOS Safari | ✅ 支持（需点击授权） |
| Android Chrome | ✅ 支持（通常无需额外权限） |
| 桌面浏览器 | ⚠️ 可打开但无降罢仪数据（显示为 0） |

---

## 免责声明

该应用仅用于演示和实验目的。消费级手机传感器的精度有限，通过二次积分估算的位移会随时间积累漂移。如需精确的惯性导航，需结合卡尔曼滤波、磁力计、视觉里程计或外部定位系统。

---

## License

MIT