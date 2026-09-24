# Heliosail · 光帆飞船太阳系逃逸模拟器

> 一个纯前端、交互式的光帆飞船物理模拟器。  
> 调节质量、帆面积和倾角，看它能否借助太阳光压逃出太阳系，并最终进入星际空间。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![HTML5](https://img.shields.io/badge/HTML-5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
[![Canvas](https://img.shields.io/badge/Canvas-2D-5EB0FF)](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API)

---

## 简介

**Heliosail** 是一个在浏览器中运行的光帆飞船模拟器。它基于真实的太阳引力与太阳光压模型，用 RK4 数值积分求解飞船轨道。你可以实时调整飞船质量、光帆面积、帆面倾角和模拟速度，观察飞船从地球出发，逐渐加速、穿越各大行星轨道，最终逃逸太阳系。

核心问题只有一个：

> **面质比（A/m）要多大，光帆才能真正战胜太阳引力？**

答案大约是 **654 m²/kg**。低于它，飞船会被太阳引力束缚；高于它，光压净推力大于引力，飞船可以向外加速并最终逃逸。

---

## 特性

- **真实物理模型**：太阳引力 + 太阳光压，按距离平方衰减
- **RK4 数值积分**：轨道计算稳定，长时间模拟不发散
- **实时参数调节**：质量、帆面积、倾角、时间速度
- **动态轨道渲染**：行星轨道、飞船轨迹、速度矢量、比例尺
- **里程碑提示**：穿越火星、木星、海王星轨道、日球层顶等
- **逃逸状态判定**：自动计算比机械能，区分束缚轨道与逃逸轨道
- **纯前端单文件**：无需构建、无需后端，打开即用

---

## 快速开始

### 方式一：直接打开

1. 下载或克隆本仓库
2. 用浏览器打开 `index.html`
3. 点击“发射”，开始模拟

```bash
git clone https://github.com/你的用户名/heliosail.git
cd heliosail
# 直接用浏览器打开 index.html
```

### 方式二：本地服务器（可选）

```bash
# Python 3
python -m http.server 8080

# 然后访问 http://localhost:8080
```

---

## 操作说明

| 控件 | 作用 |
|------|------|
| **飞船质量** | 0.001 kg ~ 50 kg，对数滑块 |
| **光帆面积** | 0.5 m² ~ 5000 m²，对数滑块 |
| **帆面倾角** | 0° ~ 60°，影响推力方向与大小 |
| **时间速度** | 0.2 ~ 100 天/帧，控制模拟快慢 |
| **发射 / 暂停** | 开始或暂停模拟，快捷键 `Space` |
| **重置** | 飞船回到地球轨道，快捷键 `R` |

右侧面板实时显示：

- 任务时间
- 距太阳距离（AU）
- 速度（km/s）
- 面质比（m²/kg）
- 光压与引力之比
- 比机械能
- 当前状态（束缚 / 逃逸）

---

## 物理模型

### 太阳引力

```
a_grav = -GM / r²
```

其中 `GM = 2.959122082855911e-4 AU³/day²`。

### 太阳光压

在距离太阳 `r`（AU）处，光压产生的加速度为：

```
a_rad = K_RAD × (A / m) × cos²(α) / r²
```

- `K_RAD = 4.5265e-7`，对应 1 AU 处完全反射光帆的加速度系数
- `A/m` 为面质比
- `α` 为帆面法线与径向的夹角

### 临界面质比

令 `a_rad = a_grav`，得到：

```
(A/m)_crit = GM / K_RAD ≈ 653.7 m²/kg
```

超过这个值，光压净推力大于太阳引力，飞船可以向外加速。

### 数值积分

采用 **四阶龙格-库塔法（RK4）** 求解轨道微分方程，保证长时间模拟的稳定性。

---

## 截图

> 建议在此处放一张模拟器运行截图或 GIF。  
> 例如：飞船轨迹穿越木星轨道，右侧面板显示“逃逸轨道”。

```
docs/screenshot.png
```

---

## 技术栈

- **HTML5 Canvas 2D**：轨道与飞船渲染
- **原生 JavaScript (ES6)**：物理计算、UI 交互、主循环
- **CSS3**：深色玻璃拟态面板、响应式布局
- **无依赖、无构建工具**

---

## 项目结构

```
heliosail/
├── index.html      # 单文件应用，包含全部 HTML/CSS/JS
├── README.md
├── LICENSE
└── docs/
    └── screenshot.png
```

---

## 可扩展方向

- 加入更多太阳系天体（行星实际位置、引力弹弓）
- 支持激光帆模式，外部激光功率可调
- 导出轨道数据为 CSV / JSON
- 增加 3D 视图（Three.js）
- 加入太阳风粒子压力
- 支持多飞船对比模拟

---

## 贡献

欢迎提交 Issue 和 Pull Request。

1. Fork 本仓库
2. 创建分支：`git checkout -b feature/your-feature`
3. 提交改动：`git commit -m 'Add some feature'`
4. 推送分支：`git push origin feature/your-feature`
5. 打开 Pull Request

---

## 许可

本项目采用 [MIT License](LICENSE) 开源。

---

## 致谢

- 光压与轨道力学公式参考经典天体力学与太阳帆推进文献
- 灵感来自 IKAROS、LightSail 2、Breakthrough Starshot 等真实光帆任务

---

**Heliosail** — 让光子带你离开太阳系。
