# Design System — Stretchly

## Product Context
- **What this is:** 跨平台休息提醒桌面应用（Electron），提醒用户定时休息
- **Who it's for:** 长时间使用电脑的知识工作者、开发者、远程工作者
- **Space/industry:** 健康/生产力工具
- **Project type:** Desktop App (Electron) — 全屏休息界面 + 设置窗口 + 欢迎界面

## Memorable Thing
**"这是苹果会设计的应用"** — 每个设计决策都应该强化这个感受：毛玻璃、圆角、SF Pro 风格字体、微妙动效、宽松间距。

## Aesthetic Direction
- **Direction:** Apple Liquid Glass — 透明毛玻璃面板、深度层次、自适应颜色、微妙发光边缘
- **Decoration level:** Intentional — 毛玻璃效果本身就是装饰，不需要额外装饰元素
- **Mood:** 沉浸、宁静、原生感。用户休息时看到的是「暂停」的视觉体验，不是另一个 UI
- **Reference:** macOS Sonoma/Vision Pro 系统界面、Apple 偏好设置面板

## Typography
- **Display/Hero:** Geist — 现代、几何、接近 SF Pro Display 的视觉感受
- **Body:** Geist — 同一字体，不同 weight (400/500)
- **UI/Labels:** Geist (weight 500)
- **Data/Tables:** Geist Mono — 支持 tabular-nums
- **Code:** Geist Mono
- **Fallback:** Noto Sans (CJK 语言) → system-ui (最终 fallback)
- **Loading:** Google Fonts 或自托管到 `app/css/fonts/`
- **Scale:**
  - Display: 48px / 56px line-height / weight 300
  - H1: 32px / 40px / weight 400
  - H2: 24px / 32px / weight 500
  - Body: 16px / 24px / weight 400
  - Small: 14px / 20px / weight 400
  - Micro: 12px / 16px / weight 500

## Color
- **Approach:** Balanced + Adaptive (跟随系统 Light/Dark 模式)

### Light Mode
| Token | Hex | Usage |
|-------|-----|-------|
| `--glass-bg` | `rgba(255, 255, 255, 0.72)` | 主毛玻璃背景 |
| `--surface` | `rgba(255, 255, 255, 0.85)` | 卡片、面板表面 |
| `--text-primary` | `#1d1d1f` | 主文字 |
| `--text-secondary` | `#86868b` | 次要文字、说明 |
| `--text-muted` | `#aeaeb2` | 最弱文字 |
| `--border` | `rgba(0, 0, 0, 0.08)` | 边框 |
| `--border-strong` | `rgba(0, 0, 0, 0.12)` | 强边框 |
| `--primary` | `#478484` | 主色调 (绿松石，保留用户品牌色) |
| `--accent` | `#007AFF` | 强调色 (Apple 蓝) |
| `--success` | `#34C759` | 成功状态 |
| `--warning` | `#FF9500` | 警告状态 |
| `--error` | `#FF3B30` | 错误状态 |

### Dark Mode
| Token | Hex | Usage |
|-------|-----|-------|
| `--glass-bg` | `rgba(30, 30, 30, 0.75)` | 主毛玻璃背景 |
| `--surface` | `rgba(44, 44, 46, 0.9)` | 卡片、面板表面 |
| `--text-primary` | `#f5f5f7` | 主文字 |
| `--text-secondary` | `#98989d` | 次要文字 |
| `--text-muted` | `#636366` | 最弱文字 |
| `--border` | `rgba(255, 255, 255, 0.1)` | 边框 |
| `--border-strong` | `rgba(255, 255, 255, 0.18)` | 强边框 |
| `--primary` | `#478484` | 主色调 (保持一致) |
| `--accent` | `#0A84FF` | 强调色 (Apple 深色蓝) |
| `--success` | `#32D74B` | 成功状态 |
| `--warning` | `#FF9F0A` | 警告状态 |
| `--error` | `#FF453A` | 错误状态 |

### Glass Effect CSS
```css
.glass-panel {
  background: var(--glass-bg);
  backdrop-filter: blur(40px) saturate(180%);
  -webkit-backdrop-filter: blur(40px) saturate(180%);
  border: 1px solid var(--border-strong);
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

/* Dark mode adjustment */
@media (prefers-color-scheme: dark) {
  .glass-panel {
    box-shadow: 
      0 8px 32px rgba(0, 0, 0, 0.24),
      inset 0 1px 0 rgba(255, 255, 255, 0.08);
  }
}
```

### Electron Vibrancy (macOS only)
```javascript
// Break windows - immersive fullscreen glass
new BrowserWindow({
  vibrancy: 'under-window',
  visualEffectState: 'active'
})

// Preferences window - sidebar glass
new BrowserWindow({
  vibrancy: 'sidebar',
  visualEffectState: 'active'
})
```

## Spacing
- **Base unit:** 8px
- **Density:** Comfortable (Apple HIG 风格宽松间距)
- **Scale:**
  - `--space-2xs`: 4px
  - `--space-xs`: 8px
  - `--space-sm`: 12px
  - `--space-md`: 16px
  - `--space-lg`: 24px
  - `--space-xl`: 32px
  - `--space-2xl`: 48px
  - `--space-3xl`: 64px

## Border Radius
- **Scale:**
  - `--radius-sm`: 6px (小按钮、输入框、tags)
  - `--radius-md`: 12px (卡片、面板、大按钮)
  - `--radius-lg`: 18px (窗口、大卡片、模态框内容区)
  - `--radius-xl`: 24px (全屏模态框)
  - `--radius-full`: 9999px (圆形元素、pill buttons)

## Layout
- **Approach:** Hybrid
  - **Break windows:** 沉浸式全屏，居中内容，无边框
  - **Preferences:** Apple HIG 风格侧边栏导航 + 分组控件
  - **Welcome:** 居中卡片式布局
- **Grid:** 12-column (Preferences), 单列居中 (Break/Welcome)
- **Max content width:** 720px (Preferences)
- **Content padding:** 32px (lg)

### Break Window Layout
```
┌─────────────────────────────────────┐
│                                     │
│    [毛玻璃背景 - blur 40px]         │
│                                     │
│         ┌─────────────┐             │
│         │ 休息提示文字 │             │
│         │   (居中)    │             │
│         │             │             │
│         │  进度条     │             │
│         │             │             │
│         │ [推迟][跳过] │             │
│         └─────────────┘             │
│                                     │
└─────────────────────────────────────┘
```

### Preferences Window Layout
```
┌────────────────────────────────────────┐
│ [侧边栏毛玻璃] │ [内容区毛玻璃]        │
│ ┌────────────┐ │ ┌──────────────────┐ │
│ │ ⚙️ 设置    │ │ │ 设置内容         │ │
│ │ 📅 计划    │ │ │                  │ │
│ │ 🎨 主题    │ │ │ [控件分组]       │ │
│ │ ℹ️ 关于    │ │ │                  │ │
│ │ ❤️ 赞助    │ │ │                  │ │
│ └────────────┘ │ └──────────────────┘ │
└────────────────────────────────────────┘
```

## Motion
- **Approach:** Minimal-functional — Apple 式微妙过渡，不干扰用户休息
- **Easing:**
  - Enter: `cubic-bezier(0.16, 1, 0.3, 1)` (ease-out-expo)
  - Exit: `cubic-bezier(0.7, 0, 0.84, 0)` (ease-in-expo)
  - Move: `cubic-bezier(0.4, 0, 0.2, 1)` (ease-in-out)
- **Duration:**
  - Micro: 100ms (hover 状态、颜色变化)
  - Short: 200ms (过渡动画、面板切换)
  - Medium: 350ms (面板展开、窗口显示)
  - Long: 500ms (全屏过渡、休息界面进入)

### Key Animations
```css
/* Break window fade in */
.break-window {
  animation: fadeIn 500ms cubic-bezier(0.16, 1, 0.3, 1);
}

/* Button hover */
.button {
  transition: background-color 100ms ease, 
              transform 100ms cubic-bezier(0.16, 1, 0.3, 1);
}
.button:hover {
  transform: scale(1.02);
}

/* Progress bar */
.progress-bar {
  transition: width 200ms linear;
}

/* Respect reduced motion */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Component Patterns

### Buttons
```css
/* Primary button */
.btn-primary {
  background: var(--primary);
  color: white;
  border-radius: var(--radius-sm);
  padding: var(--space-xs) var(--space-md);
  font-weight: 500;
}

/* Glass button (transparent) */
.btn-glass {
  background: var(--surface);
  color: var(--text-primary);
  border-radius: var(--radius-sm);
  border: 1px solid var(--border);
}

/* Pill button */
.btn-pill {
  border-radius: var(--radius-full);
}
```

### Cards/Panels
```css
.card {
  background: var(--surface);
  border-radius: var(--radius-md);
  border: 1px solid var(--border);
  padding: var(--space-lg);
}
```

### Input Fields
```css
.input {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: var(--space-xs) var(--space-sm);
  color: var(--text-primary);
}
.input:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(0, 122, 255, 0.2);
}
```

### Progress Bar
```css
.progress-bar {
  height: 6px;
  background: var(--surface);
  border-radius: var(--radius-full);
  overflow: hidden;
}
.progress-bar-fill {
  background: var(--primary);
  height: 100%;
  border-radius: var(--radius-full);
}
```

## Platform Considerations

### macOS (Primary Target)
- Use native `vibrancy` API for best performance
- `backdrop-filter` CSS as fallback
- SF Pro / Geist 字体优先
- 18px 圆角窗口 (符合 Apple HIG)

### Windows
- `backdrop-filter` 支持 Electron
- 降级: 使用 `rgba` 背景 + 模糊度较低的 `blur(20px)`
- 圆角: 12px (Windows 11 风格)

### Linux
- `backdrop-filter` 支持有限
- 降级: 使用纯色背景 + subtle shadow
- 圆角: 8px (GTK 风格)

## Risks Taken (Deliberate Departures)

### Risk 1: Immersive Glass Break Window
- **What:** 全屏休息界面使用沉浸式毛玻璃，内容漂浮在半透明层上
- **Why:** 创造「暂停」的心理感受，与其他应用视觉分离
- **Gain:** 用户真正「休息」的感觉，不是看另一个 UI
- **Cost:** 需要精心设计对比度，确保文字可读

### Risk 2: Vibrancy for Preferences Window
- **What:** 设置窗口也使用原生 vibrancy，不只是休息界面
- **Why:** 整体一致性，Apple 系统偏好设置就是这样
- **Gain:** 更原生的 macOS 体验
- **Cost:** Windows/Linux 需降级处理

### Risk 3: Geist Font Family
- **What:** 使用 Geist 字体替代 Noto Sans
- **Why:** Geist 更接近 SF Pro 的几何感，现代感更强
- **Gain:** 更「苹果」的视觉感受
- **Cost:** CJK 语言需回退到 Noto Sans

## Anti-Patterns (Avoid)
- ❌ Purple gradients as accent
- ❌ 3-column feature grids with colored circle icons
- ❌ Centered everything with uniform spacing
- ❌ Bubble radius on all elements (use hierarchical scale)
- ❌ Gradient CTA buttons (use solid or glass)
- ❌ system-ui / -apple-system as primary font (use Geist)
- ❌ Generic stock-photo hero sections
- ❌ "Built for X" / "Designed for Y" marketing copy patterns

## Decisions Log
| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-04-29 | Initial design system created | Apple Liquid Glass 风格，强化「苹果会设计的应用」记忆点 |
| 2026-04-29 | Geist font chosen | 更接近 SF Pro 的几何感，支持 tabular-nums |
| 2026-04-29 | Vibrancy for all windows | macOS 原生体验，一致性 |
| 2026-04-29 | Risk: immersive glass break | 创造「暂停」心理感受 |