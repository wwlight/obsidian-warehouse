### Vue 3 双向绑定原理

- Vue 3 中响应式是通过 Composition API 中的 `ref` 和 `reactive` 两个 `API` 来实现；
- 核心原理用的 `js` 中的 `Proxy` 代理包装原始对象；
- 借助 `Proxy` 可以拦截对象的读取（get，依赖收集）和设置（set，触发依赖更新）操作；
- 依赖收集
	- 当读取响应式对象的属性时，Vue 会记录当前正在执行的副作用函数（如计算属性、监听器）
	- 这些副作用函数会被收集为依赖项
- 依赖触发
	- 当响应式对象的属性发生变化时
	- Vue 会找到所有依赖这个属性的副作用函数
	- 并重新执行这些函数，从而更新视图
- `ref` 实现

```js
function ref(value) {
  const wrapper = {
    value
  }
  return new Proxy(wrapper, {
    get(target, key) {
      // 依赖收集
      track(target, key)
      return target[key]
    },
    set(target, key, newValue) {
      // 触发依赖更新
      target[key] = newValue
      trigger(target, key)
      return true
    }
  })
}
```

- `reactive` 实现

```js
function reactive(target) {
  return new Proxy(target, {
    get(target, key, receiver) {
      // 依赖收集
      const result = Reflect.get(target, key, receiver)
      track(target, key)
      return result
    },
    set(target, key, value, receiver) {
      // 触发依赖更新
      const result = Reflect.set(target, key, value, receiver)
      trigger(target, key)
      return result
    }
  })
}
```

---

### Vue 3 中的 track 和 trigger 实现

- `track` (依赖收集) 的工作流程
	- 检查当前是否有激活的副作用函数
	- 创建一个全局的依赖映射表 `targetMap`
	- 为每个响应式对象建立依赖关系映射
	- 将当前的副作用函数添加到对应属性的依赖集合中
- `track` 实现

```js
// 简化的 track 实现
const targetMap = new WeakMap()

function track(target, key) {
  // 获取当前激活的副作用函数
  let activeEffect = getActiveEffect()
  
  // 如果没有激活的副作用函数，直接返回
  if (!activeEffect) return

  // 获取目标对象的依赖映射
  let depsMap = targetMap.get(target)
  if (!depsMap) {
    depsMap = new Map()
    targetMap.set(target, depsMap)
  }

  // 获取特定 key 的依赖集合
  let dep = depsMap.get(key)
  if (!dep) {
    dep = new Set()
    depsMap.set(key, dep)
  }

  // 将当前副作用函数添加到依赖集合中
  dep.add(activeEffect)
}
```

- `trigger`（依赖触发）的工作流程
	- 从 `targetMap` 中找到目标对象的依赖映射
	- 获取特定属性的依赖集合
	- 依次执行所有依赖的副作用函数
- `trigger` 实现

```js
function trigger(target, key) {
  // 获取目标对象的依赖映射
  const depsMap = targetMap.get(target)
  if (!depsMap) return

  // 获取特定 key 的依赖集合
  const dep = depsMap.get(key)
  if (!dep) return

  // 执行所有依赖的副作用函数
  const effects = new Set(dep)
  effects.forEach(effect => {
    // 调度执行副作用函数
    effect()
  })
}
```

- 详细工作机制
	- **依赖收集（track）**
		- 在读取响应式对象属性时发生
		- 记录当前正在执行的副作用函数
		- 建立属性与副作用函数的映射关系
	- **依赖触发（trigger）**
		- 在修改响应式对象属性时发生
		- 找到所有依赖该属性的副作用函数
		- 重新执行这些函数
- 核心数据结构

```js
// 依赖映射的大致结构
WeakMap<target, Map<key, Set<effect>>>
```

- 优势
	- 精确的依赖追踪
	- 按需收集依赖
	- 高性能的依赖管理
	- 自动清理无用依赖

### Vue 3 和 Vue 2 双向绑定区别

```ad-important
title: Vue 3 的响应式系统相比 Vue 2
- 更灵活的代理机制
- 更高效的依赖收集
- 更精细的性能控制
- 更简洁的 API 设计
```

1. 响应式实现原理
	- Vue 2
		- 使用 `Object.defineProperty()` 实现
		- 通过递归方式劫持对象属性
		- 对于对象新增或删除属性需要使用 `Vue.set()` 和 `Vue.delete()`
		- 无法监听数组下标变化和数组长度变化
	- Vue 3
		- 使用 `Proxy` 代理
		- 可以拦截更多的操作
		- 动态添加/删除属性直接生效
		- 可以监听数组的所有变化
		- 性能和内存占用更优
2. 响应式 API
	- Vue 2
		- 只有 `data` 选项
		- 通过 `computed` 和 `watch` 实现响应
		- 响应式转换是全量的
	- Vue 3
		- `ref()`: 创建基础类型响应式引用
		- `reactive()`: 创建对象类型响应式状态
		- `computed()`: 计算属性
		- `watchEffect()`: 自动收集依赖的监听器
		- 可以精确控制响应范围
3. 嵌套对象处理
	- Vue 2
		- 深度监听需要递归
		- 性能开销较大
		- 对于深层嵌套对象，响应式不够高效
	- Vue 3
			- Proxy 可以懒递归
			- 只有访问到的属性才会被代理
			- 性能更高，内存占用更少
4. 数组响应式
	- Vue 2
		- 需要使用变异方法（push, pop 等），vue 2 内部进行了重写
		- 直接通过下标修改数组不会触发响应，`$set ()`
	- Vue 3
		- 可以直接通过下标修改数组
		- 所有数组操作都能被正确追踪
5. 性能和体积
	- Vue 3
		- 响应式系统体积更小
		- 运行时性能更优
		- 内存占用更低
		- 依赖收集更精确

---

###  Vue SEO 问题原因？如何解决？

```ad-info
title: 说明

SEO 问题可以通过多种技术方案解决，选择合适的渲染策略和持续优化。
```

- 产生原因
	1. 客户端渲染（CSR，`client-side rendering`）
		- Vue 默认使用客户端渲染
		- 页面初始内容为空 HTML
		- 搜索引擎爬虫难以抓取完整内容
	2. JavaScript 依赖
		- 内容通过 JS 动态生成
		- 搜索引擎爬虫可能无法执行 JavaScript
		- 导致页面内容无法被正确索引
	3. 首屏加载性能
		- 需要下载并执行 JavaScript
		- 初始加载时间较长
		- 影响搜索引擎评分和用户体验
- 解决方案
	1. [Meta 标签优化](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta)
		- 动态设置 SEO 相关标签
		- 精细化 meta 信息控制
	2. 服务端渲染（SSR，`server-side rendering`）
		- 直接生成完整 HTML
		- 搜索引擎友好
		- 首屏性能优化
	3. 预渲染（Pre-rendering）
		- 构建时生成静态 HTML
		- 适合相对静态的页面
		- 较低成本的 SEO 解决方案
	4. 静态站点生成（SSG，`static site generation`）
		 - 构建时预先生成所有页面
		- 性能极高
		- 适合内容相对固定的站点
	5. Nuxt.js 方案
		- 开箱即用的 SSR 解决方案
		- 内置 SEO 优化工具
		- 配置简单
- 最佳实践建议
	1. 选择合适的渲染策略
		- 内容密集型：SSR
		- 交互性强：CSR + SSR 混合
		- 静态站点：SSG
	2. 性能优化
		- 代码分割
		- 懒加载
		- 资源压缩
	3. 持续监控
		- 使用 Google Search Console
		- 分析爬虫抓取情况
		- 调整优化策略
- 推荐框架
	- Nuxt.js
	- Vite + Vue3
	- Astro
	- Gatsby

---

### SEO 如何理解

```ad-attention
title: 注意

SEO（Search Engine Optimization，搜索引擎优化）是一个网站提高在搜索引擎中可见性和排名的综合策略。
```

- 核心目标
	- 提高网站在搜索引擎中的排名
	- 增加网站的有机流量（免费的搜索流量）
	- 提高网站的可见性和用户访问量
- 工作原理
	- **爬虫**：自动化程序，遍历网络上的网页
	- **索引**：将网页内容存储和组织
	- **排名**：根据特定算法评估网页相关性和重要性
- 主要优化方向
	1. 内容优化
		- 高质量、原创的内容
		- 关键词合理分布
		- 内容与用户搜索意图匹配
		- 定期更新内容
	2. 技术优化
		- 网站加载速度
		- 移动端兼容性
		- HTML 结构清晰
		- 安全性（HTTPS）
		- 网站地图（Sitemap）
	3. 链接建设
		- 高质量的外部链接
		- 内部链接优化
		- 避免垃圾链接
		- 锚文本优化
	4. 用户体验
		 - 网站导航清晰
		- 内容可读性
		- 交互性
		- 低跳出率
- 具体实践

``` html
<!-- SEO 优化的 HTML 示例 -->
<head>
  <!-- 明确、简洁的标题 -->
  <title>专业网站开发服务 | 定制网站解决方案</title>
  
  <!-- 描述性的 meta 标签 -->
  <meta name="description" 
        content="提供高质量、定制化的网站开发服务，帮助企业建立专业的在线形象。">
  
  <!-- 语义化 HTML5 标签 -->
  <header>
    <h1>专业网站开发</h1>
  </header>
</head>
``` 

- 关键指标
	1. **关键词排名**
		- 目标关键词在搜索结果中的位置
		- 长尾关键词的覆盖
	2. **流量指标**
		- 搜索引擎带来的访问量
		- 访问时长
		- 跳出率
	3. **转化率**
		- 搜索流量带来的实际业务转化
- 常见工具
	- Google Search Console
	- Google Analytics
	- SEMrush
	- Ahrefs
	- MOZ

---
