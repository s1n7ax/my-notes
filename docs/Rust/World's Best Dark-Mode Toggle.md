This not is based off of [this video by Leptos developer](https://www.youtube.com/watch?v=AD3FHodVgE8)

1. Using the color-scheme meta tag or CSS

**HTML:**

```html
<head>
  <meta name="color-scheme" content="dark light">
</head>
```

**CSS:**

```css
:root {
  color-scheme: dark;
}
```

**Rust Leptos:**

```rust
view! {
	cx,
	<Meta name="color-scheme" content="dark light">
}
```
