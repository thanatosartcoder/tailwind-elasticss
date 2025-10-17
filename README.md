# tailwind-elasticss

Elastic responsive utilities for Tailwind CSS v4 with intelligent `clamp()` and container query support.

[![npm version](https://img.shields.io/npm/v/tailwind-elasticss.svg)](https://www.npmjs.com/package/tailwind-elasticss)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Features

✨ **Automatic clamp() calculation** - No manual math required  
🎯 **Container query support** - Respond to parent container size  
🔧 **Customizable via CSS variables** - Full control when you need it  
⚡ **Zero JavaScript** - Pure CSS solution for Tailwind CSS v4  
📦 **Tiny footprint** - Just CSS utilities, no dependencies

## Installation

```bash
npm install tailwind-elasticss
```

## Usage

Add the plugin to your CSS file:

```css
@import "tailwindcss";
@import "tailwind-elasticss";
```

## API Reference

### Viewport-based Utilities

#### Width & Height

```html
<!-- Automatic: clamp(176px, 200px, 240px) -->
<div class="w-fluid-[200px]">Auto-calculated fluid width</div>

<!-- Height -->
<div class="h-fluid-[300px]">Auto-calculated fluid height</div>
```

#### Max Width & Max Height

```html
<!-- max-width: clamp(704px, 800px, 960px) -->
<div class="max-w-fluid-[800px]">Fluid max-width</div>

<!-- max-height -->
<div class="max-h-fluid-[400px]">Fluid max-height</div>
```

### Container Query Utilities

Require `@container` on parent element.

```html
<div class="@container">
  <!-- Responds to container size -->
  <div class="w-fluid-cq-[250px]">Container-aware width</div>
  
  <!-- Also works with max-width -->
  <article class="max-w-fluid-cq-[600px]">Container-aware max-width</article>
</div>
```

### Customization with CSS Variables

#### For width/height utilities

```html
<!-- Custom min/max bounds -->
<div class="fluid-min-[150px] fluid-max-[300px] w-fluid-[200px]">
  clamp(150px, 200px, 300px)
</div>

<!-- Works with percentages -->
<div class="fluid-max-[95%] w-fluid-[200px]">
  clamp(176px, 200px, 95%)
</div>
```

#### For max-width/max-height utilities

```html
<!-- Custom bounds for max-width -->
<div class="fluid-max-w-min-[500px] fluid-max-w-max-[1200px] max-w-fluid-[800px]">
  max-width: clamp(500px, 800px, 1200px)
</div>
```

## Complete Utilities List

### Viewport-based (Respond to viewport size)

| Utility | CSS Variable (min) | CSS Variable (max) | Default Behavior |
|---------|-------------------|-------------------|------------------|
| `w-fluid-[value]` | `--fluid-min` | `--fluid-max` | 88% → 120% |
| `h-fluid-[value]` | `--fluid-min` | `--fluid-max` | 88% → 120% |
| `max-w-fluid-[value]` | `--fluid-max-w-min` | `--fluid-max-w-max` | 88% → 120% |
| `max-h-fluid-[value]` | `--fluid-max-w-min` | `--fluid-max-w-max` | 88% → 120% |

### Container Query-based (Respond to parent container)

| Utility | Breakpoints | Behavior |
|---------|------------|----------|
| `w-fluid-cq-[value]` | `< 400px`: 85%→115%<br>`400-800px`: 90%→130%<br>`> 800px`: Fixed | Container-aware |
| `h-fluid-cq-[value]` | Same as above | Container-aware |
| `max-w-fluid-cq-[value]` | Same as above | Container-aware |
| `max-h-fluid-cq-[value]` | Same as above | Container-aware |

### CSS Variable Utilities

| Utility | Sets Variable | Used By |
|---------|--------------|---------|
| `fluid-min-[value]` | `--fluid-min` | `w-fluid-*`, `h-fluid-*` |
| `fluid-max-[value]` | `--fluid-max` | `w-fluid-*`, `h-fluid-*` |
| `fluid-max-w-min-[value]` | `--fluid-max-w-min` | `max-w-fluid-*`, `max-h-fluid-*` |
| `fluid-max-w-max-[value]` | `--fluid-max-w-max` | `max-w-fluid-*`, `max-h-fluid-*` |

## Examples

### Responsive sidebar

```html
<div class="@container flex">
  <aside class="w-fluid-cq-[250px] bg-gray-800">
    <!-- Sidebar adapts to container -->
  </aside>
  <main class="flex-1">
    <!-- Main content -->
  </main>
</div>
```

### Content container with fluid max-width

```html
<article class="w-full max-w-fluid-[800px] mx-auto px-4">
  <!-- Max-width scales between 704px and 960px -->
  <h1>Article Title</h1>
  <p>Content...</p>
</article>
```

### Modal with custom bounds

```html
<div class="fluid-min-[300px] fluid-max-[90%] w-fluid-[500px]">
  <!-- Width: clamp(300px, 500px, 90%) -->
  <h2>Modal Title</h2>
  <p>Modal content...</p>
</div>
```

### Reusable bounds for multiple elements

```html
<div class="fluid-min-[100px] fluid-max-[500px]">
  <div class="w-fluid-[200px]">Card 1</div>
  <div class="w-fluid-[300px]">Card 2</div>
  <div class="w-fluid-[400px]">Card 3</div>
  <!-- All inherit min: 100px, max: 500px -->
</div>
```

### Grid with container-aware cards

```html
<div class="@container grid grid-cols-[repeat(auto-fit,minmax(200px,1fr))] gap-4">
  <div class="w-fluid-cq-[280px]">
    <!-- Each card responds to its grid cell size -->
  </div>
</div>
```

## Browser Support

- Chrome/Edge 105+
- Firefox 110+
- Safari 16+

Container queries require modern browser support. Check [caniuse.com](https://caniuse.com/css-container-queries) for details.

## Requirements

- Tailwind CSS v4.0.0 or higher

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT © [Your Name]

## Related

- [Tailwind CSS](https://tailwindcss.com)
- [CSS Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries)
- [CSS clamp()](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp)