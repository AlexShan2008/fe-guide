# A summary of this project

## 1.CSS

### 1.1 `transition:`当属性是背景渐变`linear-gradient`时无效：

> 现象：

```scss
...fadeIn // 无效
background: linear-gradient(90deg, #0042d2 0%, #009aee 100%);
```
> 解决方案：（障眼法，加遮罩层）,`hover`时候改变不透明度

```scss
.jss1 .content .item .main .mask {
    top: 0;
    left: 0;
    width: 100%;
    color: #fff;
    height: 100%;
    opacity: 0;
    padding: 0 .48rem .48rem;
    position: absolute;
    transition: all .3s ease;
    background: linear-gradient(90deg, #0042d2 0%, #009aee 100%);
    border-radius: 10px;
}
```

### 1.2 当高度不固定时`min-height`时，`transition:`无效：

> 现象：

```scss
...fadeIn // 无效
min-height: 0;
max-height: 0;
```

> 解决方案：两种状态下设置`max-height`，且自适应高度状态下时`max-height`设置为不可能超过的数值

```scss
min-height: auto;
max-height: 100vh;
```

### 1.3 呼吸灯效果

> 现象：实现星光闪耀

```scss
```

> 解决方案：用`animation`实现动画，改变不透明度

```scss
.jss422 .star {
    left: 0;
    animation: breath 4s infinite ease-in-out alternate;
}

@-webkit-keyframes breath{
  0%{opacity:.2}
  50%{opacity:1}
  to{opacity:.2}
}
@keyframes breath{
  0%{opacity:.2}
  50%{opacity:1}
  to{opacity:.2}
}
```


### 1.3 滚动视差

> 现象：实现背景固定，文字滚动

```scss
```

> 解决方案：用`background-attachment: fixed;`实现背景固定

```scss
background-attachment: fixed;
```


### 1.4 `vw` VS `rem` VS `%` 移动端布局单位对比

> vw：基于视口，按比例显示，和父级元素大小无关

```scss
1vw = 1%
```

> rem：基于`html`和`body`的`font-size`，按比例显示

```scss
1rem = 1px // html或者body 的font-size
```

> %：基于父级元素大小，按比例显示

```scss
1% = 1%（parent: font-size ） // 已父级元素为参考font-size
```

## 2.`javascript`

### 2.1 

> 目标：滚动鼠标滚轮的时候，改变显示效果

```scss
```

> 解决方案：

```jsx
handleScroll = () => {
    const top =
      document.documentElement.scrollTop ||
      document.body.scrollTop ||
      window.pageYOffset
    if (top > 63) {
      this.setState({
        active: true
      })
    } else {
      this.setState({
        active: false
      })
    }
  }

componentDidMount () {
  const scrollFn = _.throttle(this.handleScroll, 300)

  this.setState({
    loaded: true,
    scrollFn
  })

  window.addEventListener('scroll', scrollFn)
}

componentWillUnmount () {
  window.removeEventListener('scroll', this.state.scrollFn)
}
```

### 2.2 

> 目标：不支持浏览器友情提示（如：`IE 11`以下）
> 解决方案：在`index.html`添加提示

```jsx
```
