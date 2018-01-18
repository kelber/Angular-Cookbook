# SaaS 

### 2018 

```css
$back-image url('./assets/camaro.jpg'), no repeat;

body {
  background-image: $back-image;
}

@mixin anchorAtivo {
  font-size: 2em;
  font-weight: bold;
}
```

// Where you will use
```css
  @import '.././styles.scss';

  h1 {
    color: $primary;
    .active {
      @include: anchorAtivo
    }
  }

  a {
    color: red;
    &:hover {
      color: blue;
    }
  }


```