---
title: Markdown
title_zh-CN: Markdown
categories:
  - writing
end: true
---

Valaxy 带有内置的 Markdown 扩展。

## 标题锚点 {#header-anchors}

标题会自动应用锚点。可以使用 `markdown.anchor` 选项配置锚点的渲染。

### 自定义锚点 {#custom-anchors}

要为标题指定自定义锚点而不是使用自动生成的锚点，请向标题添加后缀：

```
# 使用自定义锚点 {#my-anchor}
```

这允许将标题链接为 `#my-anchor`，而不是默认的 `#使用自定义锚点`。

## 链接 {#links}

内部和外部链接都会被特殊处理。

### 内部链接 {#internal-links}

内部链接将转换为单页导航的路由链接。此外，子目录中包含的每个 `index.md` 都会自动转换为 `index.html`，并带有相应的 URL `/`。

例如，给定以下目录结构：

```
.
├─ index.md
├─ foo
│  ├─ index.md
│  ├─ one.md
│  └─ two.md
└─ bar
   ├─ index.md
   ├─ three.md
   └─ four.md
```

假设现在处于 `foo/one.md` 文件中：

```md
[Home](/) <!-- 将用户导航至根目录下的 index.html -->
[foo](/foo/) <!-- 将用户导航至目录 foo 下的 index.html -->
[foo heading](./#heading) <!-- 将用户锚定到目录 foo 下的index文件中的一个标题上 -->
[bar - three](../bar/three) <!-- 可以省略扩展名 -->
[bar - three](../bar/three.md) <!-- 可以添加 .md -->
[bar - four](../bar/four.html) <!-- 或者可以添加 .html -->
```

### 页面后缀 {#page-suffix}

默认情况下，生成的页面和内部链接带有 `.html` 后缀。

### 外部链接 {#external-links}

外部链接带有 `target="_blank" rel="noreferrer"`：

- [vuejs.org](https://cn.vuejs.org)
- [valaxy on GitHub](https://github.com/YunYouJun/valaxy)

## frontmatter {#frontmatter}

[YAML 格式的 frontmatter](https://jekyllrb.com/docs/front-matter/) 开箱即用：

```yaml
---
title: Blogging Like a Hacker
lang: en-US
---
```

此数据将可用于页面的其余部分，以及所有自定义和主题组件。

更多信息，参见 [frontmatter](/guide/writing/frontmatter)。

## GitHub 风格的表格 {#github-style-tables}

**输入**

```
| Tables        |      Are      |  Cool |
| ------------- | :-----------: | ----: |
| col 3 is      | right-aligned | $1600 |
| col 2 is      |   centered    |   $12 |
| zebra stripes |   are neat    |    $1 |
```

**输出**

| Tables        |      Are      |   Cool |
| ------------- | :-----------: | -----: |
| col 3 is      | right-aligned | \$1600 |
| col 2 is      |   centered    |   \$12 |
| zebra stripes |   are neat    |    \$1 |

## Emoji :tada:

**输入**

```
:tada: :100:
```

**输出**

:tada: :100:

这里可以找到[所有支持的 emoji 列表](https://github.com/markdown-it/markdown-it-emoji/blob/master/lib/data/full.mjs)。

## 目录表 (TOC) {#table-of-contents}

**输入**

```
[[toc]]
```

**输出**

[[toc]]

可以使用 `markdown.toc` 选项配置 TOC 的呈现效果。

## 自定义容器 {#custom-containers}

自定义容器可以通过它们的类型、标题和内容来定义。

### 默认标题 {#default-title}

**输入**

```md
::: info
This is an info box.
:::

::: tip
This is a tip.
:::

::: warning
This is a warning.
:::

::: danger
This is a dangerous warning.
:::

::: details
This is a details block.
:::
```

**输出**

::: info
This is an info box.
:::

::: tip
This is a tip.
:::

::: warning
This is a warning.
:::

::: danger
This is a dangerous warning.
:::

::: details
This is a details block.
:::

### 自定义标题 {#custom-title}

可以通过在容器的 "type" 之后附加文本来设置自定义标题。

**输入**

````md
::: danger STOP
危险区域，请勿继续
:::

::: details 点我查看代码

```js
console.log('Hello, valaxy!')
```

:::
````

**输出**

::: danger STOP
危险区域，请勿继续
:::

::: details 点我查看代码

```js
console.log('Hello, valaxy!')
```

:::

## GitHub 风格的警报 {#github-flavored-alerts}

valaxy 同样支持以标注的方式渲染 [GitHub 风格的警报](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts)。它们和[自定义容器](#custom-containers)的渲染方式相同。

```md
> [!NOTE]
> 强调用户在快速浏览文档时也不应忽略的重要信息。

> [!TIP]
> 有助于用户更顺利达成目标的建议性信息。

> [!IMPORTANT]
> 对用户达成目标至关重要的信息。

> [!WARNING]
> 因为可能存在风险，所以需要用户立即关注的关键内容。

> [!CAUTION]
> 行为可能带来的负面影响。
```

> [!NOTE]
> 强调用户在快速浏览文档时也不应忽略的重要信息。

> [!TIP]
> 有助于用户更顺利达成目标的建议性信息。

> [!IMPORTANT]
> 对用户达成目标至关重要的信息。

> [!WARNING]
> 因为可能存在风险，所以需要用户立即关注的关键内容。

> [!CAUTION]
> 行为可能带来的负面影响。

## 代码块中的语法高亮 {#syntax-highlighting-in-code-blocks}

Valaxy 使用 [Shiki](https://github.com/shikijs/shiki) 在 Markdown 代码块中使用彩色文本实现语法高亮。Shiki 支持多种编程语言。需要做的就是将有效的语言别名附加到代码块的开头：

**输入**

````
```js
export default {
  name: 'MyComponent',
  // ...
}
```
````

````
```html
<ul>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
  </li>
</ul>
```
````

**输出**

```js
export default {
  name: 'MyComponent'
  // ...
}
```

```html
<ul>
  <li v-for="todo in todos" :key="todo.id">{{ todo.text }}</li>
</ul>
```

在 Shiki 的代码仓库中，可以找到[合法的编程语言列表](https://shiki.style/languages)。

<!-- 还可以全局配置中自定义语法高亮主题。有关详细信息，参见 [`markdown` 选项](/site-config#markdown)得到更多信息。 -->

## 在代码块中实现行高亮 {#line-highlighting-in-code-blocks}

**输入**

````
```js{4}
export default {
  data () {
    return {
      msg: 'Highlighted!'
    }
  }
}
```
````

**输出**

```js{4}
export default {
  data () {
    return {
      msg: 'Highlighted!'
    }
  }
}
```

**输入**

````md
```ts {1}
// line-numbers is disabled by default
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers {1}
// line-numbers is enabled
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers=2 {1}
// line-numbers is enabled and start from 2
const line3 = 'This is line 3'
const line4 = 'This is line 4'
```
````

**输出**

```ts {1}
// line-numbers is disabled by default
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers {1}
// line-numbers is enabled
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers=2 {1}
// line-numbers is enabled and start from 2
const line3 = 'This is line 3'
const line4 = 'This is line 4'
```

除了单行之外，还可以指定多个单行、多行，或两者均指定：

- 多行：例如 `{5-8}`、`{3-10}`、`{10-17}`
- 多个单行：例如 `{4,7,9}`
- 多行与单行：例如 `{4,7-13,16,23-27,40}`

**输入**

````
```js{1,4,6-8}
export default { // Highlighted
  data () {
    return {
      msg: `Highlighted!
      This line isn't highlighted,
      but this and the next 2 are.`,
      motd: 'valaxy is awesome',
      lorem: 'ipsum'
    }
  }
}
```
````

**输出**

```js{1,4,6-8}
export default { // Highlighted
  data () {
    return {
      msg: `Highlighted!
      This line isn't highlighted,
      but this and the next 2 are.`,
      motd: 'valaxy is awesome',
      lorem: 'ipsum',
    }
  }
}
```

也可以使用 `// [!code highlight]` 注释实现行高亮。

**输入**

````
```js
export default {
  data () {
    return {
      msg: 'Highlighted!' // [!!code highlight]
    }
  }
}
```
````

**输出**

```js
export default {
  data() {
    return {
      msg: 'Highlighted!' // [!code highlight]
    }
  }
}
```

## 代码块中聚焦 {#focus-in-code-blocks}

在某一行上添加 `// [!code focus]` 注释将聚焦它并模糊代码的其他部分。

此外，可以使用 `// [!code focus:<lines>]` 定义要聚焦的行数。

**输入**

````
```js
export default {
  data () {
    return {
      msg: 'Focused!' // [!!code focus]
    }
  }
}
```
````

**输出**

```js
export default {
  data() {
    return {
      msg: 'Focused!' // [!code focus]
    }
  }
}
```

## 代码块中的颜色差异 {#colored-diffs-in-code-blocks}

在某一行添加 `// [!code --]` 或 `// [!code ++]` 注释将会为该行创建 diff，同时保留代码块的颜色。

**输入**

````
```js
export default {
  data () {
    return {
      msg: 'Removed' // [!!code --]
      msg: 'Added' // [!!code ++]
    }
  }
}
```
````

**输出**

```js
export default {
  data () {
    return {
      msg: 'Removed' // [!code --]
      msg: 'Added' // [!code ++]
    }
  }
}
```

## 高亮“错误”和“警告” {#errors-and-warnings-in-code-blocks}

在某一行添加 `// [!code warning]` 或 `// [!code error]` 注释将会为该行相应的着色。

**输入**

````
```js
export default {
  data () {
    return {
      msg: 'Error', // [!!code error]
      msg: 'Warning' // [!!code warning]
    }
  }
}
```
````

**输出**

```js
export default {
  data() {
    return {
      msg: 'Error', // [!code error]
      msg: 'Warning' // [!code warning]
    }
  }
}
```

## 行号 {#line-numbers}

可以通过以下配置为每个代码块启用行号：

```ts
export default defineConfig<ThemeConfig>({
  markdown: {
    lineNumbers: true
  }
})
```

<!-- 查看 [`markdown` 选项](../site-config#markdown) 获取更多信息。 -->

可以在代码块中添加 `:line-numbers` / `:no-line-numbers` 标记来覆盖在配置中的设置。

还可以通过在 `:line-numbers` 之后添加 `=` 来自定义起始行号，例如 `:line-numbers=2` 表示代码块中的行号从 2 开始。

**输入**

````md
```ts {1}
// 默认禁用行号
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers {1}
// 启用行号
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers=2 {1}
// 行号已启用，并从 2 开始
const line3 = 'This is line 3'
const line4 = 'This is line 4'
```
````

**输出**

```ts {1}
// 默认禁用行号
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers {1}
// 启用行号
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:line-numbers=2 {1}
// 行号已启用，并从 2 开始
const line3 = 'This is line 3'
const line4 = 'This is line 4'
```

## 导入代码片段 {#import-code-snippets}

可以通过下面的语法来从现有文件中导入代码片段：

```md
<<< @/filepath
```

此语法同时支持[行高亮](#line-highlighting-in-code-blocks)：

```md
<<< @/filepath{highlightLines}
```

**输入**

```md
<<< @/snippets/snippet.js{2}
```

**Code file**

<<< @/snippets/snippet.js

**输出**

<<< @/snippets/snippet.js{2}

::: tip
`@` 的值对应于源代码根目录，默认情况下是 valaxy 项目根目录，除非配置了 `srcDir`。或者也可以从相对路径导入：

```md
<<< ../snippets/snippet.js
```

:::

也可以使用 [VS Code region](https://code.visualstudio.com/docs/editor/codebasics#_folding) 来只包含代码文件的相应部分。可以在文件目录后面的 `#` 符号后提供一个自定义的区域名：

**输入**

```md
<<< @/snippets/snippet-with-region.js#snippet{1}
```

**Code file**

<<< @/snippets/snippet-with-region.js

**输出**

<<< @/snippets/snippet-with-region.js#snippet{1}

也可以像这样在大括号内(`{}`)指定语言：

```md
<<< @/snippets/snippet.cs{c#}

<!-- 带行高亮: -->

<<< @/snippets/snippet.cs{1,2,4-6 c#}

<!-- 带行号: -->

<<< @/snippets/snippet.cs{1,2,4-6 c#:line-numbers}
```

如果无法从文件扩展名推测出源语言，这将会很有帮助

## 代码组 {#code-groups}

可以像这样对多个代码块进行分组：

**输入**

````md
::: code-group

```js [config.js]
/**
 * @type {import('valaxy').UserConfig}
 */
const config = {
  // ...
}

export default config
```

```ts [config.ts]
import type { UserConfig } from 'valaxy'

const config: UserConfig = {
  // ...
}

export default config
```

:::
````

**输出**

::: code-group

```js [config.js]
/**
 * @type {import('valaxy').UserConfig}
 */
const config = {
  // ...
}

export default config
```

```ts [config.ts]
import type { UserConfig } from 'valaxy'

const config: UserConfig = {
  // ...
}

export default config
```

:::

也可以在代码组中[导入代码片段](#import-code-snippets)：

**输入**

```md
::: code-group

<!-- 文件名默认用作标题 -->

<<< @/snippets/snippet.js

<!-- 也可以提供定制的代码组 -->

<<< @/snippets/snippet-with-region.js#snippet{1,2 ts:line-numbers} [snippet with region]

:::
```

**输出**

::: code-group

<<< @/snippets/snippet.js

<<< @/snippets/snippet-with-region.js#snippet{1,2 ts:line-numbers} [snippet with region]

:::

## 包含 markdown 文件 {#markdown-file-inclusion}

可以像这样在一个 markdown 文件中包含另一个 markdown 文件，甚至是内嵌的。

::: tip
也可以使用 `@`，它的值对应于源代码根目录，默认情况下是 valaxy 项目根目录，除非配置了 `srcDir`。
:::

例如，可以这样用相对路径包含 Markdown 文件：

**输入**

```md
# Docs

## Basics

<!--@include: ./parts/basics.md-->
```

**Part file** (`parts/basics.md`)

```md
Some getting started stuff.

### Configuration

Can be created using `.foorc.json`.
```

**等价代码**

```md
# Docs

## Basics

Some getting started stuff.

### Configuration

Can be created using `.foorc.json`.
```

它还支持选择行范围：

**输入**

```md
# Docs

## Basics

<!--@include: ./parts/basics.md{3,}-->
```

**Part file** (`parts/basics.md`)

```md
Some getting started stuff.

### Configuration

Can be created using `.foorc.json`.
```

**等价代码**

```md
# Docs

## Basics

### Configuration

Can be created using `.foorc.json`.
```

所选行范围的格式可以是： `{3,}`、 `{,10}`、`{1,10}`

::: warning
如果指定的文件不存在，这将不会产生错误。因此，在使用这个功能的时候请保证内容按预期呈现。
:::

## 数学方程 {#math-equations}

**输入**

```md
When $a \ne 0$, there are two solutions to $(ax^2 + bx + c = 0)$ and they are
$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

**Maxwell's equations:**

| equation                                                                                                                                                                  | description                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| $\nabla \cdot \vec{\mathbf{B}}  = 0$                                                                                                                                      | divergence of $\vec{\mathbf{B}}$ is zero                                               |
| $\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t}  = \vec{\mathbf{0}}$                                                          | curl of $\vec{\mathbf{E}}$ is proportional to the rate of change of $\vec{\mathbf{B}}$ |
| $\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} = \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} = 4 \pi \rho$ | _wha?_                                                                                 |
```

**输出**

When $a \ne 0$, there are two solutions to $(ax^2 + bx + c = 0)$ and they are
$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

**Maxwell's equations:**

| equation                                                                                                                                                                  | description                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| $\nabla \cdot \vec{\mathbf{B}}  = 0$                                                                                                                                      | divergence of $\vec{\mathbf{B}}$ is zero                                               |
| $\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t}  = \vec{\mathbf{0}}$                                                          | curl of $\vec{\mathbf{E}}$ is proportional to the rate of change of $\vec{\mathbf{B}}$ |
| $\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} = \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} = 4 \pi \rho$ | _wha?_                                                                                 |

### Custom KaTeX Options {lang="en"}

### 自定义 KaTeX 选项 {lang="zh-CN"}

```ts
// valaxy.config.ts
export default defineValaxyConfig({
  markdown: {
    /**
     * KaTeX options
     * @see https://katex.org/docs/options.html
     */
    katex: {
      strict: false
    }
  }
})
```

## UnoCSS

::: en
We integrated [UnoCSS](https://unocss.dev), so you can use it in your markdown file.
:::

::: zh-CN
我们集成了 [UnoCSS](https://unocss.dev)，因此您可以在 Markdown 文件中直接使用它。
:::

::: en
Freedom to control your layout!

> More configurations see [UnoCSS Options](https://valaxy.site/guide/config/unocss-options).

:::

::: zh-CN
自由控制你的布局！

> 更多配置见 [UnoCSS Options | 配置](https://valaxy.site/guide/config/unocss-options)。

:::

<div class="flex flex-col">

<div class="flex grid-cols-3" gap="2">
  <div>

![image](https://www.yunyoujun.cn/images/avatar.jpg)

  </div>

  <div>

![image](https://www.yunyoujun.cn/images/avatar.jpg)

  </div>

  <div>

![image](https://www.yunyoujun.cn/images/avatar.jpg)

  </div>
</div>

<div class="flex grid-cols-2 justify-center items-center" gap="2">

![image](https://cdn.yunyoujun.cn/img/bg/stars-timing-1.jpg)

![image](https://cdn.yunyoujun.cn/img/bg/astronaut.webp)

</div>

</div>

```html
<div class="flex flex-col">
  <div class="flex grid-cols-3">
    <div>![image](https://www.yunyoujun.cn/images/avatar.jpg)</div>

    <div>![image](https://www.yunyoujun.cn/images/avatar.jpg)</div>

    <div>![image](https://www.yunyoujun.cn/images/avatar.jpg)</div>
  </div>

  <div class="flex grid-cols-2 justify-center items-center">
    ![image](https://cdn.yunyoujun.cn/img/bg/stars-timing-1.jpg)
    ![image](https://cdn.yunyoujun.cn/img/bg/astronaut.webp)
  </div>
</div>
```

## Mermaid

Based on [mermaid](https://mermaid.js.org/), you can use it in your markdown file directly.

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

````txt
```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
````

More examples see: [Mermaid](https://valaxy.site/examples/mermaid)

## 脚注 {lang="zh-CN"}

## Footnote {lang="en"}

::: zh-CN
你可以使用 `[^1]` 或 `[^footnote]` 来添加脚注，例如：

```md
这是一个脚注[^1-zh]。

这是一段脚注[^2-zh]。

[^1-zh]: 这是一个脚注。

[^2-zh]: 这是一段脚注。

正确缩进的脚注段落会被自动附加。

使用 `^[content]` 可以创建方便的内联脚注^[比如这个！]。
```

这是一个脚注[^1-zh]。

这是一段脚注[^2-zh]。

[^1-zh]: 这是一个脚注。

[^2-zh]: 这是一段脚注。

正确缩进的脚注段落会被自动附加。

使用 `^[content]` 可以创建方便的内联脚注^[比如这个！]。
:::

::: en
You can use `[^1]` or `[^footnote]` to add footnotes, for example:

```md
This is a footnote[^1-en].

This is a paragraph of footnote[^2-en].

[^1-en]: This is a footnote.

[^2-en]: This is a paragraph of footnote.

Footnote paragraphs with correct indentation will be automatically attached.

Use `^[content]` to create convenient inline footnotes^[like this!].
```

This is a footnote[^1-en].

This is a paragraph of footnote[^2-en].

[^1-en]: This is a footnote.

[^2-en]: This is a paragraph of footnote.

Footnote paragraphs with correct indentation will be automatically attached.

Use `^[content]` to create convenient inline footnotes^[like this!].
:::

### 脚注预览 {lang="zh-CN"}

### Footnote Preview {lang="en"}

::: zh-CN
借助 [`Floating Vue`](https://floating-vue.starpad.dev/), 添加的脚注链接在鼠标悬停时会显示脚注内容。你可以在本页面的脚注链接上试一试！

如果你想要自定义脚注的样式，可以参考 [Floating Vue 文档](https://floating-vue.starpad.dev/guide/config) 中的 `config` 设置 `site.config.ts` 中的 `floatingVue`，你也可以修改组件 `ValaxyFootnoteTooltip` 来达到这一点。
:::

::: en
With [`Floating Vue`](https://floating-vue.starpad.dev/), the added footnote links will display the footnote content when hovering over them. You can try it with the footnote links on this page!

If you want to customize the style of the footnote, you can refer to `config` in the [Floating Vue documentation](https://floating-vue.starpad.dev/guide/config) and change the `floatingVue` option in `site.config.ts` accordingly. You can also modify the `ValaxyFootnoteTooltip` component to achieve this.
:::

## 自定义 {lang="zh-CN"}

## Custom {lang="en"}

### 自定义 Markdown 容器 Class {lang="zh-CN"}

### Custom Markdown Container Class {lang="en"}

::: zh-CN

你可以在 Markdown 文件的 frontmatter 中添加 `markdownClass` 来自定义 Markdown 容器的 Class。

:::

::: en

You can add `markdownClass` in the frontmatter of the markdown file to customize the Class of the Markdown container.

:::

```md
---
markdownClass: 'markdown-body custom-markdown-class'
---
```
