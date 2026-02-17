# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在此仓库中工作时提供指导。

## 项目概览

这是一个加密货币钱包移动端界面项目（RekashPay）。

**Crypto Wallet** - `crypto-wallet.html`
- 移动端优先的加密货币钱包界面
- 设计来自 Figma 设计稿
- 使用原生 HTML/CSS/JavaScript 构建
- 采用 SF Pro 字体系列和 Figma 设计令牌
- 资源 URL 来自 Figma API（有效期 7 天）

## 开发指南

### 本地开发

直接在浏览器中打开文件：
```bash
open crypto-wallet.html
```

无需构建过程 - 所有样式和脚本都内联在文件中。

### 预览和调试

- 使用浏览器开发者工具查看响应式布局（推荐 375px 移动端视口）
- 所有交互逻辑在 `<script>` 标签中
- LocalStorage 不用于此项目（仅展示 UI）

## 设计系统

### 颜色令牌（来自 Figma）

```css
--bg-primary: #ffffff;           /* 主背景色 */
--bg-secondary: #f8f9fb;         /* 次要背景色 */
--neutral-50: #f9f9f9;           /* 中性灰 50 */
--neutral-100: #f0f0f0;          /* 中性灰 100 */
--neutral-400: #a3a3a3;          /* 中性灰 400 */
--neutral-500: #7a818a;          /* 中性灰 500 */
--neutral-700: #231815;          /* 中性灰 700 */
--primary-green: #008651;        /* 主绿色（轮播指示器）*/
--success-600: #34c759;          /* 成功色（正向金额）*/
--danger-600: #f64c4c;           /* 危险色（负向金额）*/
--promo-bg: #eaf2ff;             /* 推广横幅背景 */
```

### 排版系统

- **字体栈**: `-apple-system, 'SF Pro', BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif`
- **字号规范**:
  - 余额主数字: 36px (粗体 700)
  - 余额小数: 24px (半粗体 600)
  - 货币单位: 16px (中等 500)
  - 标题: 14px (半粗体 600)
  - 正文: 12px (常规 400)

### 布局规范

- **容器宽度**: 375px（移动端标准宽度）
- **圆角**:
  - 卡片/横幅: 20px
  - 学习卡片: 14px
  - 操作按钮图标: 50%（圆形）
- **间距**:
  - 卡片内边距: 20px
  - 组件间距: 16px
  - 操作按钮间距: 40px

### 组件尺寸

- **操作按钮图标**: 56px × 56px（圆形，背景 #f9f9f9）
- **交易项高度**: 64px
- **USDT 图标**: 32px × 32px
- **学习卡片图片**: 96px 高度
- **推广横幅最小高度**: 114px
- **轮播指示点**: 4px × 4px

## 界面结构

### 主要区块

1. **余额卡片** (`.balance-card`)
   - 余额显示区域：支持显示/隐藏切换
   - 三个操作按钮：Deposit、Send、Referral
   - 使用 Figma 导出的真实图标

2. **推广横幅** (`.promo-banner`)
   - 浅蓝色背景 (#eaf2ff)
   - 右侧图片装饰
   - 底部轮播指示器（绿色激活态）
   - 自动轮播切换（3 秒间隔）

3. **学习区域** (`.section > .learn-cards`)
   - 两列网格布局
   - 以太坊认证教程
   - Rekash Pay 全球支付介绍

4. **交易历史** (`.section > .activity-list`)
   - USDT 交易记录列表
   - 状态显示: Processing.../Confirmed/Failed/Pending
   - 金额颜色：正数绿色、负数红色

## Figma 集成

### 设计文件信息

- **Figma 文件**: `https://www.figma.com/design/B3XZx7b2Up9plGT9PVdBvX/RekashPay`
- **节点 ID**: `132:2201`
- **设计系统**: RekashPay 移动端钱包界面

### 使用 Figma MCP

连接到 Figma：
```bash
/mcp
```

获取最新设计和资源：
```javascript
mcp__figma__get_design_context({
  fileKey: "B3XZx7b2Up9plGT9PVdBvX",
  nodeId: "132:2201",
  clientLanguages: "html,css,javascript"
})
```

### 资源管理

- **图片 URL**: 所有图片使用 Figma API URL
- **有效期**: 7 天后过期
- **刷新方法**: 重新调用 `mcp__figma__get_design_context` 获取新 URL
- **关键资源**:
  - 操作图标（Deposit/Send/Referral）
  - 眼睛/下拉图标
  - 推广横幅图片
  - 学习卡片图片（以太坊、Rekash Pay）
  - USDT 代币图标

## 开发注意事项

### 修改 HTML 文件时

1. **保持内联结构**
   - 所有样式在 `<style>` 标签内
   - 所有脚本在 `<script>` 标签内
   - 无外部依赖文件

2. **维护 CSS 变量**
   - 在 `:root` 中统一管理颜色令牌
   - 使用变量而非硬编码颜色值
   - 保持与 Figma 设计令牌一致

3. **动画和过渡**
   - 保持现有动画时长和缓动函数
   - 淡入动画: `fadeInUp 0.5s ease-out`
   - 交互反馈: `0.2s ease` 过渡

4. **响应式设计**
   - 优先支持移动端（375px）
   - 容器最大宽度不超过 375px
   - 保持 16px 外边距

### 图片资源过期处理

当 Figma 图片 URL 过期（7 天后）：

1. 连接 Figma MCP 服务器（`/mcp`）
2. 调用 `mcp__figma__get_design_context` 获取新的资源 URL
3. 替换 HTML 中的旧 URL
4. 验证所有图片正常显示

### 设计还原标准

修改界面时必须严格遵循 Figma 设计：
- ✅ 精确的颜色值（使用设计令牌）
- ✅ 准确的字号和字重
- ✅ 正确的间距和圆角
- ✅ 一致的阴影效果
- ✅ 匹配的组件尺寸

### JavaScript 交互逻辑

当前实现的交互功能：
- **余额切换**: 点击眼睛图标显示/隐藏余额
- **轮播自动播放**: 3 秒间隔自动切换指示点
- **点击反馈**: 卡片和按钮点击时的缩放效果

扩展功能时保持：
- 简洁的事件处理
- 直接的 DOM 操作
- 无外部库依赖

