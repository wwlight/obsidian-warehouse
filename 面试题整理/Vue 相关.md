### Vue 双向绑定原理

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
### Vue 3 和 Vue 2 双向绑定区别
>[!important]
>Vue 3 的响应式系统相比 Vue 2
	>- 更灵活的代理机制
	>- 更高效的依赖收集
	>- 更精细的性能控制
	>- 更简洁的 API 设计

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
	-  Vue 2
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
		- 需要使用变异方法（push, pop等），vue 2 内部进行了重写
		- 直接通过下标修改数组不会触发响应， `$set ()`
	- Vue 3
		- 可以直接通过下标修改数组
		- 所有数组操作都能被正确追踪
5. 性能和体积
	-  Vue 3
		- 响应式系统体积更小
		- 运行时性能更优
		- 内存占用更低
		- 依赖收集更精确 
