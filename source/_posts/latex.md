---
title: LaTeX 数学公式
excerpt: 使用主题内置的 KaTeX 服务端渲染优雅地书写数学公式。
date: 2026-03-28 23:51
cover: /img/klara-kulikova-PgrSvkU1_4Y-unsplash.jpg
coverInfo:
  author: Klara Kulikova
  url: https://unsplash.com/photos/PgrSvkU1_4Y
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
latex: true
---

## 简介

Linen 主题内置了基于 [KaTeX](https://katex.org/) 的服务端数学公式渲染（无需额外安装 Hexo 公式插件）：

- **构建期预渲染**：公式在 `hexo generate` 阶段直接渲染为 HTML，浏览器端零 JavaScript 解析开销，首屏即现。
- **按需输出与加载资源**：仅当站点中存在已渲染的公式时，才会生成内置的 `katex.min.css` 与 `.woff2` 字体；且仅在包含公式的页面中引入样式表，不影响普通文章加载速度。

## 全局配置

在站点根目录的 `_config.linen.yml` 中配置 `latex`：

- **快捷开启**

  ```yaml _config.linen.yml
  latex: true
  ```

- **完整配置（自定义 CSS 或 KaTeX 选项）**

  ```yaml _config.linen.yml
  latex:
    enable: true
    css: "" # 可选，填入自定义本地路径或 CDN 链接；留空则自动使用主题内置的 KaTeX CSS 与字体
    options:
      throwOnError: false # 默认 false
      strict: ignore      # 默认 "ignore"
      macros:
        "\\RR": "\\mathbb{R}"
        "\\E": "\\mathbb{E}"
  ```

## 页面级配置

如果不想全局开启，或者希望在单篇文章中关闭/定制公式选项，可以在文章的 Front Matter 中使用 `latex`（或别名 `math`）：

```yaml
---
title: 某篇包含数学公式的文章
latex: true # 也可写 math: true；全局开启时写 false 可单篇关闭
---
```

也支持在单篇文章中传入页面级 KaTeX 选项与宏定义（会与全局 `options` 合并）：

```yaml
---
title: 自定义宏示例
latex:
  enable: true
  macros:
    "\\vect": "\\mathbf{#1}"
---
```

## 书写语法与示例

本页已开启 `latex: true`，下方展示了常用写法的源码与实际渲染效果。

### 行内公式

使用单个美元符号 `$ ... $` 包裹单行数学表达式：

```markdown
质能方程 $E = mc^2$，欧拉恒等式 $e^{i\pi} + 1 = 0$，以及条件概率 $P(A \mid B) = \frac{P(A \cap B)}{P(B)}$。
```

渲染效果：质能方程 $E = mc^2$，欧拉恒等式 $e^{i\pi} + 1 = 0$，以及条件概率 $P(A \mid B) = \frac{P(A \cap B)}{P(B)}$。

为了避免正文中的货币价格被误识别为公式，行内公式需满足以下规则：

- 不能跨行；
- 起始 `$` 后不能紧跟空白字符，且前一个字符不能是数字；
- 结束 `$` 前不能紧跟空白字符，且后一个字符不能是数字。

例如价格写法 `$100`、`从 $10 到 $20` 不会被误解析；如需在特殊位置输出字面 `$`，可使用反斜杠转义 `\$`。

### 块级公式

使用双美元符号 `$$ ... $$` 书写独立成行或多行的展示公式：

```markdown
$$
\int_{-\infty}^{+\infty} e^{-x^2}\,dx = \sqrt{\pi}
$$
```

渲染效果：

$$
\int_{-\infty}^{+\infty} e^{-x^2}\,dx = \sqrt{\pi}
$$

支持多行对齐环境与矩阵：

```markdown
$$
\begin{aligned}
\nabla \cdot \mathbf{E} &= \frac{\rho}{\varepsilon_0} \\
\nabla \cdot \mathbf{B} &= 0 \\
\nabla \times \mathbf{E} &= -\frac{\partial \mathbf{B}}{\partial t} \\
\nabla \times \mathbf{B} &= \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}
\end{aligned}
$$
```

渲染效果：

$$
\begin{aligned}
\nabla \cdot \mathbf{E} &= \frac{\rho}{\varepsilon_0} \\
\nabla \cdot \mathbf{B} &= 0 \\
\nabla \times \mathbf{E} &= -\frac{\partial \mathbf{B}}{\partial t} \\
\nabla \times \mathbf{B} &= \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}
\end{aligned}
$$

也支持在引用块（`>`）内直接书写多行块级公式：

> 高斯分布的概率密度函数定义为：
>
> $$
> f(x) = \frac{1}{\sigma \sqrt{2\pi}} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)
> $$

### 自动跳过区域

以下区域中的 `$` 和 `$$` 会被自动忽略，不会触发公式解析：

- Markdown 围栏代码块（```` ``` ```` / `~~~`）与行内代码（`` `$x$` ``）
- 原生 HTML `<pre>`、`<code>`、`<script>`、`<style>` 标签内部
- Hexo 标签 `{% codeblock %}` 与 `{% raw %}` 内部
