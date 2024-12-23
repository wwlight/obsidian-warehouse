>[!note] 说明
>内容整理来自 [claude.ai](https://claude.ai/)

## 基本规则

```ad-success
title: 扩展

- 渐变：[gradient](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient)
- 线性渐变：[linear-gradient()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient/linear-gradient)
- 径向渐变：[radial-gradient()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient/radial-gradient)
- 重复渐变：[repeating-linear-gradient()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient/repeating-linear-gradient) 、[repeating-radial-gradient()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient/repeating-radial-gradient)
- 锥形渐变：[conic-gradient()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient/conic-gradient)
```


- 在 CSS 渐变中，角度的定义遵循以下规则：
	- 0 度是从下往上
	- 90 度是从左往右
	- 180 度是从上往下
	- 270 度（或 -90 度）是从右往左

## 和数学圆中角度的区别
- 起始位置不同：
    - CSS 渐变：0° 指向上方（12点钟方向）
    - 数学角度：0° 指向右方（3点钟方向）
- 旋转方向不同：
    - CSS 渐变：顺时针旋转
    - 数学角度：逆时针旋转
- 常用角度对应关系：
```
	 CSS渐变    数学角度
	 0°    →   90°
	 90°   →   0°
	 180°  →   270°
	 270°  →   180°
```
- 实际应用场景：
	- CSS渐变角度主要用于设计和用户界面，更符合视觉直觉（从上到下更自然）
	- 数学角度用于数学计算和科学场景，符合笛卡尔坐标系统

## 转换方式
```js
// CSS角度转数学角度
const cssToMath = (cssAngle) => (90 - cssAngle + 360) % 360;

// 数学角度转CSS角度
const mathToCss = (mathAngle) => (90 - mathAngle + 360) % 360;
```

## 相关图例
![[dark-mode-angles.svg]]