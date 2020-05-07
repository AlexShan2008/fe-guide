# FE Guide

## 最佳原则

- 坚持制定好的代码规范。
- 无论团队人数多少，代码应该同出一门。
- 如果你想要为这个规范做贡献或觉得有不合理的地方，可以随时更新。

## 编码规范

### 命名规则

#### 项目命名

全部采用小写方式， 以短横线分隔。

例：`my-project-name`

#### 目录命名

- 参照项目命名规则；
- 完整英文命名的用复数形式，缩写用单数形式
- 例：`scripts, js, styles, css, images, img, data-models, modules, pages`

#### 文件命名

同目录命名规则

### HTML

### CSS, SCSS

参照[Airbnb CSS / Sass Styleguide](https://github.com/airbnb/css)

#### Formatting

- Use soft tabs (2 spaces) for indentation.
- Prefer dashes over camelCasing in class names.
  - Underscores and PascalCasing are okay if you are using BEM (see OOCSS and BEM below).
- Do not use ID selectors.
- When using multiple selectors in a rule declaration, give each selector its own line.
- Put a space before the opening brace { in rule declarations.
- In properties, put a space after, but not before, the : character.
- Put closing braces } of rule declarations on a new line.
- Put blank lines between rule declarations.

Bad

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```
Good

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

#### Comments

- Prefer line comments (// in Sass-land) to block comments.
- Prefer comments on their own line. Avoid end-of-line comments.
- Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks

#### OOCSS and BEM

We encourage some combination of OOCSS and BEM for these reasons:

- It helps create clear, strict relationships between CSS and HTML
- It helps us create reusable, composable components
- It allows for less nesting and lower specificity
- It helps in building scalable stylesheets

**OOCSS**, or “Object Oriented CSS”, is an approach for writing CSS that encourages you to think about your stylesheets as a collection of “objects”: reusable, repeatable snippets that can be used independently throughout a website.

- Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
- Smashing Magazine's Introduction to [OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, or “Block-Element-Modifier”, is a naming convention for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind, and can serve as a solid set of guidelines for implementing OOCSS.

- CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
- Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

We recommend a variant of BEM with PascalCased “blocks”, which works particularly well when combined with components (e.g. React). Underscores and dashes are still used for modifiers and children.

**Example**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

- .ListingCard is the “block” and represents the higher-level component
- .ListingCard__title is an “element” and represents a descendant of .ListingCard that helps compose the block as a whole.
- .ListingCard--featured is a “modifier” and represents a different state or variation on the .ListingCard block.

#### JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

#### Border

Use 0 instead of none to specify that a style has no border.

Bad

```css
.foo {
  border: none;
}
```

Good

```ccc
.foo {
  border: 0;
}
```

### Sass

#### Syntax

- Use the .scss syntax, never the original .sass syntax
- Order your regular CSS and @include declarations logically (see below)

Ordering of property declarations

1. Property declarations

   List all standard property declarations, anything that isn't an @include or a nested selector.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  // ...
}
```

2. @include declarations
   Grouping @includes at the end makes it easier to read the entire selector.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  // ...
}
```

3. Nested selectors

   Nested selectors, if necessary, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

```scss
.btn {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);

  .icon {
    margin-right: 10px;
  }
}
```

#### Variables

Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).

#### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

#### Extend directive
`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using `@extend`, and you can DRY up your stylesheets nicely with mixins.

#### Nested selectors

Do not nest selectors more than three levels deep!

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

When selectors become this long, you're likely writing CSS that is:

- Strongly coupled to the HTML (fragile) —OR—
- Overly specific (powerful) —OR—
- Not reusable
- Again: never nest ID selectors!

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should never need to do this.

### css-in-javascript

参照[Airbnb CSS-in-JavaScript Style Guide](https://github.com/AlexShan2008/javascript/tree/master/css-in-javascript)


### JavaScript

参照[AirBnB规范](https://github.com/airbnb/javascript)


## 构建规范

## 组件规范