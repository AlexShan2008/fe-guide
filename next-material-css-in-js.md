# A Core Points Guide for Next.js and MaterialUI

### Webpack resolve alias

```
@utils => utils
@stores => stores
@static => static
@constants => constants
@components => components
```

### File type

- react compnent and page => `.jsx`
- normal js => `.js`

> in pages directory `.jsx` file will be render as page

### Strongly Recommended

- CSS in JS, CSS 样式：[React JSS](https://github.com/cssinjs/react-jss)
- UI 库：[material-ui](https://github.com/mui-org/material-ui)
- [你需要知道的 CSS-in-JS](https://www.infoq.cn/article/2017/11/css-in-js-need-know)

### Grid Layout

**1. Grid**

```JSX
const message = `Truncation should be conditionally applicable on this long line of text
 as this is a much longer line than what the container can support. `;

<Grid container spacing={24}>
  <Grid item xs={12} sm >
    <Paper className={classes.paper}>xs</Paper>
  </Grid>
</Grid>

<Grid item xs zeroMinWidth>
  <Typography noWrap>{message}</Typography>
</Grid>
```

**2. Breakpoints**

每个断点都与 _ 固定 _ 屏幕宽度匹配:

- ** xs **, 超小: 0px 或更大
- ** sm **, 小: 600px 或更大
- ** md **, 中等: 960px 或更大
- ** lg **, 大: 1280px 或更大
- ** xl **, 超大: 1920px 或更大
  这些值可以自定义。 这些值被用于主题设定，你可以在 breakpoints.values 对象上找到它们。

**3. MediaQuery**  
[Mobile First 原则](https://baijiahao.baidu.com/s?id=1617748122977936710&wfr=spider&for=pc)

```javascript
-theme.breakpoints.up(key) -
  theme.breakpoints.down(key) -
  theme.breakpoints.only(key) -
  theme.breakpoints.between(start, end);
```

```JSX
const styles = theme => ({
  root: {
    padding: theme.spacing.unit,
    [theme.breakpoints.down('sm')]: {
      backgroundColor: theme.palette.secondary.main,
    },
    [theme.breakpoints.up('md')]: {
      backgroundColor: theme.palette.primary.main,
    },
    [theme.breakpoints.up('lg')]: {
      backgroundColor: green[500],
    },
  },
});
```

**4. Hidden**

> 应用 Hidden 组件实现组件的显示或者隐藏

```
xs 0 - 600
sm 600 - 960
md 960 - 1280
lg 1280 - 1920
up: 从最小值开始
down: 从最大值开始

innerWidth  |xs      sm       md       lg       xl
            |--------|--------|--------|--------|-------->
width       |   xs   |   sm   |   md   |   lg   |   xl

smUp        |   show | hide
mdDown      |                     hide | show
```

```JSX
<Hidden xsDown>
  <Paper className={classes.paper}>xsDown</Paper>
</Hidden>
<Hidden smDown>
  <Paper className={classes.paper}>smDown</Paper>
</Hidden>
<Hidden mdDown>
  <Paper className={classes.paper}>mdDown</Paper>
</Hidden>
<Hidden lgDown>
  <Paper className={classes.paper}>lgDown</Paper>
</Hidden>
<Hidden xlDown>
  <Paper className={classes.paper}>xlDown</Paper>
</Hidden>`
```

**5. Laze Loading Components**

```JSX
//import Highlight from 'react-highlight'
import dynamic from 'next/dynamic'

const Highlight = dynamic(import('react-highlight'))

```

**6. Enabling decorator syntax**
(Enabling decorator syntax)[https://mobx.js.org/best/decorators.html]

```sh
npm install --save-dev babel-preset-mobx

```

`.babelrc`:

```
{
  "presets": ["mobx"]
}
```

6.1 Babel 6: manually enabling decorators

```sh
npm i --save-dev babel-plugin-transform-decorators-legacy
```

```JSON

{
  "presets": ["es2015", "stage-1"],
  "plugins": ["transform-decorators-legacy"]
}
```

6.2 Babel 7

```sh
npm i --save-dev @babel/plugin-proposal-class-properties @babel/plugin-proposal-decorators
```

```JSON
{
    "presets": ["mobx"],
    "plugins": [
        ["@babel/plugin-proposal-decorators", { "legacy": true}],
        ["@babel/plugin-proposal-class-properties", { "loose": true}]
    ]
}
```

## Carousel (轮播图插件)

[react-slick](https://www.npmjs.com/package/react-slick)

1. install package

```sh
yarn add react-slick
yarn add slick-carousel
```

2. import css and font files

```css
@import "./slick/slick.css";
@import "./slick/slick-theme.css";
```

### eslint-plugin-react-hooks

[eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)

// .eslintrc

```json
{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn"
  }
}
```
