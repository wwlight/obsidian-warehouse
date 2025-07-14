#备忘录 #unocss

### 常用预设

````col
```col-md
`size-full`
```
```col-md
`size-16`
```
===
```css
.size-full,
[size-full=""] {
  width: 100%;
  height: 100%;
}
```
```css
.size-16,
[size-16=""] {
  width: 16px;
  height: 16px;
}
```
````

````col
```col-md
`w-screen`
```
```col-md
`w-full`
```
===
```css
.w-screen,
[w-screen=""] {
  width: 100vw;
}
```
```css
.w-full,
[w-full=""] {
  width: 100%;
}
```
````

````col
```col-md
`truncate`
```
```col-md
`line-clamp-2`
```
===
```css
.truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```
```css
.line-clamp-2,
[line-clamp-2=""] {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  line-clamp: 2;
}
```
````

````col
```col-md
`hidden`
```
```col-md
`block`
```
===
```css
.hidden,
[hidden=""] {
  display: none;
}
```
```css
.block,
[block=""] {
  display: block;
}
```
````

````col
```col-md
`invisible`
```
```col-md
`visible`
```
===
```css
.invisible,
[invisible=""] {
  visibility: hidden;
}
```
```css
.visible,
[visible=""] {
  visibility: visible;
}
```
````

````col
```col-md
`text-[--el-color-primary]` `[!!success: 推荐]`
```
```col-md
`text-[var(--el-color-primary)]`
```
===
```css
.text-\[--el-color-primary\],
[text-\[--el-color-primary\]=""] {
  color: var(--el-color-primary);
}
```
```css
.text-\[var\(--el-color-primary\)\],
[text-\[var\(--el-color-primary\)\]=""] {
  color: var(--el-color-primary);
}
```
````

### 媒体查询

```ad-note
title: 相关问题资料
+ [https://github.com/unocss/unocss/discussions/997](https://github.com/unocss/unocss/discussions/997)
+ [https://github.com/unocss/unocss/issues/181](https://github.com/unocss/unocss/issues/181)
+ [https://windicss.org/utilities/general/variants.html#desktop-first](https://windicss.org/utilities/general/variants.html#desktop-first)

```

```col
`container`
===
```css
.container,
[container=""] {
  width: 100%;
}
@media (min-width: 768px) {
  .container,
  [container=""] {
    max-width: 768px;
  }
}
@media (min-width: 992px) {
  .container,
  [container=""] {
    max-width: 992px;
  }
}
@media (min-width: 1200px) {
  .container,
  [container=""] {
    max-width: 1200px;
  }
}
@media (min-width: 1920px) {
  .container,
  [container=""] {
    max-width: 1920px;
  }
}
```

````col
```col-md
`md:w-10`
```
```col-md
`at-md:w-10`
```
===
```css
@media (min-width: 992px) {
  .md\:w-10,
  [md\:w-10=""] {
    width: 10px;
  }
}
```
```css
@media (min-width: 992px) and (max-width: 1199.9px) {
  .at-md\:w-10,
  [at-md\:w-10=""] {
    width: 10px;
  }
}
```
````

````col
```col-md
`lt-md:w-10` `[!!success: 推荐]`
```
```col-md
`<md:w-10`
```
===
```css
@media (max-width: 991.9px) {
  .lt-md\:w-10,
  [lt-md\:w-10=""] {
    width: 10px;
  }
}
```

```css
@media (max-width: 991.9px) {
  .\<md\:w-10,
  [\<md\:w-10=""] {
    width: 10px;
  }
}
```
````

### 变体组

```ad-info
title: 说明

- 相关文档：[variant-group](https://unocss.dev/transformers/variant-group)
```

```javascript
import { defineConfig, transformerVariantGroup } from 'unocss'

export default defineConfig({
  // ...
  transformers: [
    transformerVariantGroup(),
  ],
})
```

```html
<div class="hover:(bg-gray-400 font-medium) font-(light mono)"/>
<!-- 将转换为 -->
<div class="hover:bg-gray-400 hover:font-medium font-light font-mono"/>
```

### 指令转换器

```ad-info
title: 说明
- 相关文档：[directives](https://unocss-cn.pages.dev/transformers/directives)
```

```javascript
import { defineConfig, transformerDirectives } from 'unocss'

export default defineConfig({
  // ...
  transformers: [
    transformerDirectives(),
  ],
})
```

```css
.custom-div {
  @apply text-center my-0 font-medium;
}
/* 将转换为 */
.custom-div {
  margin-top: 0rem;
  margin-bottom: 0rem;
  text-align: center;
  font-weight: 500;
}
```

### 自定义

```ad-info
title: 说明
- 不存在的预设可通过中括号 `[]` 方式自定义
```

````col
`[isolation:isolate]`
===
```css
.\[isolation\:isolate\],
[\[isolation\:isolate\]=""] {
  isolation: isolate;
}
```

````

````col
`[clip-path:polygon(97%_0,100%_50%%_100%_100%_0)]`
===
```css
.\[clip-path\:polygon\(97\%_0\\%_50\%\\%_100\%\_100\%\_0\)\],
[\[clip-path\:polygon\(97\%_0\\%_50\%\\%_100\%\_100\%\_0\)\]=""] {
  clip-path: polygon(97% 0, 100% 50%, 97% 100%, 0 100%, 0 0);
}
```
````
