## the note of Next.js

### Using Shared Components

**1. Method 1 - Layout as a Higher Order Component**

```JSX
// components/MyLayout.js

import Header from './Header'

const layoutStyle = {
  margin: 20,
  padding: 20,
  border: '1px solid #DDD'
}

const withLayout = Page => {
  return () => (
    <div style={layoutStyle}>
      <Header />
      <Page />
    </div>
  )
}

export default withLayout
```

```JSX
// pages/index.js

import withLayout from '../components/MyLayout'

const Page = () => <p>Hello Next.js</p>

export default withLayout(Page)
```

```JSX
// pages/about.js

import withLayout from '../components/MyLayout'

const Page = () => <p>This is the about page</p>

export default withLayout(Page)
```

**2. Method 2 - Page content as a prop**

```JSX
// components/MyLayout.js

import Header from './Header'

const layoutStyle = {
  margin: 20,
  padding: 20,
  border: '1px solid #DDD'
}

const Layout = props => (
  <div style={layoutStyle}>
    <Header />
    {props.content}
  </div>
)

export default Layout
```

```JSX
// pages/index.js

import Layout from '../components/MyLayout.js'

const indexPageContent = <p>Hello Next.js</p>

export default function Index() {
  return <Layout content={indexPageContent} />
}
```

```JSX
// pages/about.js

import Layout from '../components/MyLayout.js'

const aboutPageContent = <p>This is the about page</p>

export default function About() {
  return <Layout content={aboutPageContent} />
}
```

> react-markdown

```sh
npm install --save react-markdown
```
