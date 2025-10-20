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
📝 **Typography support** - Fluid font-size and line-height utilities

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

## Table of Contents

- [Layout Utilities](#layout-utilities)
  - [Width & Height](#width--height)
  - [Max Width & Max Height](#max-width--max-height)
- [Typography Utilities](#typography-utilities)
  - [Font Size](#font-size)
  - [Line Height](#line-height)
- [Container Queries](#container-queries)
- [Customization](#customization)
- [Complete API Reference](#complete-api-reference)
- [Examples](#examples)

---

## Layout Utilities

### Width & Height

Fluid width and height that automatically scales between 88% and 120% of the base value.

```html
<!-- Automatic: clamp(176px, 200px, 240px) -->
<div class="w-fluid-[200px]">Auto-calculated fluid width</div>

<!-- Height: clamp(264px, 300px, 360px) -->
<div class="h-fluid-[300px]">Auto-calculated fluid height</div>
```

**With custom bounds:**
```html
<!-- Custom min/max bounds -->
<div class="fluid-min-[150px] fluid-max-[300px] w-fluid-[200px]">
  <!-- width: clamp(150px, 200px, 300px) -->
</div>

<!-- Works with percentages -->
<div class="fluid-max-[95%] w-fluid-[200px]">
  <!-- width: clamp(176px, 200px, 95%) -->
</div>
```

### Max Width & Max Height

Fluid max-width and max-height utilities.

```html
<!-- max-width: clamp(704px, 800px, 960px) -->
<div class="max-w-fluid-[800px]">Fluid max-width</div>

<!-- max-height: clamp(352px, 400px, 480px) -->
<div class="max-h-fluid-[400px]">Fluid max-height</div>
```

**With custom bounds:**
```html
<div class="fluid-max-w-min-[500px] fluid-max-w-max-[1200px] max-w-fluid-[800px]">
  <!-- max-width: clamp(500px, 800px, 1200px) -->
</div>
```

---

## Typography Utilities

### Font Size

Fluid font-size that automatically scales for responsive typography.

```html
<!-- Basic: clamp(28.16px, 32px, 38.4px) -->
<h1 class="text-fluid-[32px]">Fluid heading</h1>

<!-- With custom min -->
<h1 class="fluid-text-min-[24px] text-fluid-[32px]">
  <!-- font-size: clamp(24px, 32px, 38.4px) -->
</h1>

<!-- With custom max -->
<p class="fluid-text-max-[20px] text-fluid-[16px]">
  <!-- font-size: clamp(14.08px, 16px, 20px) -->
</p>
```

**Fluid typography scale:**
```html
<div class="fluid-text-min-[14px] fluid-text-max-[72px]">
  <h1 class="text-fluid-[48px]">Display heading</h1>
  <h2 class="text-fluid-[32px]">Subheading</h2>
  <p class="text-fluid-[16px]">Body text</p>
  <!-- All respect the same min/max bounds -->
</div>
```

### Line Height

Fluid line-height for optimal readability at any size.

```html
<!-- Basic: clamp(21.12px, 24px, 28.8px) -->
<p class="leading-fluid-[24px]">Fluid line-height</p>

<!-- With custom bounds -->
<h2 class="fluid-leading-min-[28px] fluid-leading-max-[48px] leading-fluid-[36px]">
  <!-- line-height: clamp(28px, 36px, 48px) -->
</h2>

<!-- Relative values (unitless) -->
<p class="leading-fluid-[1.5]">
  <!-- line-height: clamp(1.32, 1.5, 1.8) -->
</p>
```

**Combining font-size and line-height:**
```html
<div class="fluid-text-min-[14px] fluid-text-max-[72px]
            fluid-leading-min-[20px] fluid-leading-max-[96px]">
  <h1 class="text-fluid-[48px] leading-fluid-[56px]">Title</h1>
  <p class="text-fluid-[16px] leading-fluid-[24px]">
    Text with fully fluid typography
  </p>
</div>
```

---

## Container Queries

All utilities have container query variants that respond to parent container size instead of viewport.

**Requires `@container` on parent element.**

### Layout with Container Queries

```html
<div class="@container">
  <!-- Responds to container size -->
  <div class="w-fluid-cq-[250px]">Container-aware width</div>

  <!-- Max-width variant -->
  <article class="max-w-fluid-cq-[600px]">Container-aware max-width</article>
</div>
```

**Breakpoint behavior:**
- `< 400px`: Compression (85% - 115%)
- `400px - 800px`: Balance (90% - 130%)
- `> 800px`: Fixed value (or custom via `--fluid-override`)

### Typography with Container Queries

```html
<article class="@container">
  <h1 class="text-fluid-cq-[32px] leading-fluid-cq-[40px]">
    Typography that adapts to container width
  </h1>
  <p class="text-fluid-cq-[16px] leading-fluid-cq-[24px]">
    Maintains optimal proportions at any container size
  </p>
</article>
```

---

## Customization

### Global Customization

Define bounds for multiple elements:

```html
<div class="fluid-min-[100px] fluid-max-[500px]">
  <div class="w-fluid-[200px]">Element 1</div>
  <div class="w-fluid-[300px]">Element 2</div>
  <div class="w-fluid-[400px]">Element 3</div>
  <!-- All inherit min: 100px, max: 500px -->
</div>
```

### Override in Large Containers

```html
<div class="@container" style="--fluid-override: 300px">
  <div class="w-fluid-cq-[250px]">
    <!-- Uses 300px fixed in containers > 800px -->
  </div>
</div>
```

### Typography Customization

```html
<div style="--fluid-text-min: 14px;
            --fluid-text-max: 20px;
            --fluid-leading-min: 20px;
            --fluid-leading-max: 32px">
  <p class="text-fluid-cq-[16px] leading-fluid-cq-[24px]">
    Full control over size and line-height bounds
  </p>
</div>
```

---

## Complete API Reference

### Viewport-based Utilities

Respond to viewport/window size.

| Utility | CSS Variable (min) | CSS Variable (max) | Default Behavior |
|---------|-------------------|-------------------|------------------|
| `w-fluid-[value]` | `--fluid-min` | `--fluid-max` | 88% → 120% |
| `h-fluid-[value]` | `--fluid-min` | `--fluid-max` | 88% → 120% |
| `max-w-fluid-[value]` | `--fluid-max-w-min` | `--fluid-max-w-max` | 88% → 120% |
| `max-h-fluid-[value]` | `--fluid-max-w-min` | `--fluid-max-w-max` | 88% → 120% |
| `text-fluid-[value]` | `--fluid-text-min` | `--fluid-text-max` | 88% → 120% |
| `leading-fluid-[value]` | `--fluid-leading-min` | `--fluid-leading-max` | 88% → 120% |

### Container Query Utilities

Respond to parent container size.

| Utility | Breakpoints | Behavior |
|---------|------------|----------|
| `w-fluid-cq-[value]` | `< 400px`: 85%→115%<br>`400-800px`: 90%→130%<br>`> 800px`: Fixed | Container-aware |
| `h-fluid-cq-[value]` | Same as above | Container-aware |
| `max-w-fluid-cq-[value]` | Same as above | Container-aware |
| `max-h-fluid-cq-[value]` | Same as above | Container-aware |
| `text-fluid-cq-[value]` | Same as above | Container-aware |
| `leading-fluid-cq-[value]` | Same as above | Container-aware |

### CSS Variable Utilities

Control bounds for fluid utilities.

| Utility | Sets Variable | Used By |
|---------|--------------|---------|
| `fluid-min-[value]` | `--fluid-min` | `w-fluid-*`, `h-fluid-*` |
| `fluid-max-[value]` | `--fluid-max` | `w-fluid-*`, `h-fluid-*` |
| `fluid-max-w-min-[value]` | `--fluid-max-w-min` | `max-w-fluid-*`, `max-h-fluid-*` |
| `fluid-max-w-max-[value]` | `--fluid-max-w-max` | `max-w-fluid-*`, `max-h-fluid-*` |
| `fluid-text-min-[value]` | `--fluid-text-min` | `text-fluid-*` |
| `fluid-text-max-[value]` | `--fluid-text-max` | `text-fluid-*` |
| `fluid-leading-min-[value]` | `--fluid-leading-min` | `leading-fluid-*` |
| `fluid-leading-max-[value]` | `--fluid-leading-max` | `leading-fluid-*` |

---

## Examples

### Responsive Sidebar

```html
<div class="@container flex">
  <aside class="w-fluid-cq-[250px] bg-gray-800 @container">
    <h3 class="text-fluid-cq-[20px] leading-fluid-cq-[28px]">
      Sidebar Title
    </h3>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px]">
      Text adapts to sidebar width
    </p>
  </aside>
  <main class="flex-1">
    <!-- Main content -->
  </main>
</div>
```

### Article with Fluid Typography

```html
<article class="@container w-full max-w-fluid-cq-[800px] mx-auto px-4">
  <header class="@container">
    <h1 class="text-fluid-cq-[36px] leading-fluid-cq-[44px]">
      Article Title
    </h1>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px] text-gray-600">
      Published on Jan 1, 2025
    </p>
  </header>
  <div class="@container mt-8">
    <p class="text-fluid-cq-[18px] leading-fluid-cq-[28px]">
      Article content with typography that adapts perfectly
      to the container width, maintaining optimal readability.
    </p>
  </div>
</article>
```

### Complete Typography Scale

```html
<div class="fluid-text-min-[12px] fluid-text-max-[96px]
            fluid-leading-min-[16px] fluid-leading-max-[112px]">
  <h1 class="text-fluid-[64px] leading-fluid-[72px]">Display</h1>
  <h2 class="text-fluid-[48px] leading-fluid-[56px]">Heading 1</h2>
  <h3 class="text-fluid-[32px] leading-fluid-[40px]">Heading 2</h3>
  <h4 class="text-fluid-[24px] leading-fluid-[32px]">Heading 3</h4>
  <p class="text-fluid-[16px] leading-fluid-[24px]">Body text</p>
  <small class="text-fluid-[14px] leading-fluid-[20px]">Small text</small>
</div>
```

### Modal with Custom Bounds

```html
<div class="fluid-min-[300px] fluid-max-[90%] w-fluid-[500px]">
  <!-- width: clamp(300px, 500px, 90%) -->
  <h2 class="text-fluid-[24px] leading-fluid-[32px]">Modal Title</h2>
  <p class="text-fluid-[16px] leading-fluid-[24px]">Modal content...</p>
</div>
```

### Grid with Container-Aware Cards

```html
<div class="@container grid grid-cols-[repeat(auto-fit,minmax(200px,1fr))] gap-4">
  <div class="@container p-4 bg-white rounded-lg shadow">
    <h3 class="text-fluid-cq-[20px] leading-fluid-cq-[28px]">Card Title</h3>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px]">
      Each card responds to its grid cell size, not the viewport
    </p>
  </div>
  <div class="@container p-4 bg-white rounded-lg shadow">
    <h3 class="text-fluid-cq-[20px] leading-fluid-cq-[28px]">Card Title</h3>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px]">
      Typography scales perfectly at any card width
    </p>
  </div>
</div>
```

### Reusable Bounds for Consistency

```html
<div class="fluid-min-[100px] fluid-max-[500px]
            fluid-text-min-[14px] fluid-text-max-[24px]">
  <div class="w-fluid-[200px]">
    <h3 class="text-fluid-[20px]">Card 1</h3>
  </div>
  <div class="w-fluid-[300px]">
    <h3 class="text-fluid-[20px]">Card 2</h3>
  </div>
  <div class="w-fluid-[400px]">
    <h3 class="text-fluid-[20px]">Card 3</h3>
  </div>
  <!-- All inherit the same min/max bounds -->
</div>
```

### Dashboard Layout

```html
<div class="@container grid grid-cols-1 md:grid-cols-3 gap-6">
  <!-- Widget 1 -->
  <div class="@container p-6 bg-white rounded-lg">
    <h2 class="text-fluid-cq-[24px] leading-fluid-cq-[32px] font-bold">
      Statistics
    </h2>
    <p class="text-fluid-cq-[48px] leading-fluid-cq-[56px] font-bold text-blue-600">
      1,234
    </p>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px] text-gray-600">
      Total users
    </p>
  </div>

  <!-- Widget 2 -->
  <div class="@container p-6 bg-white rounded-lg">
    <h2 class="text-fluid-cq-[24px] leading-fluid-cq-[32px] font-bold">
      Revenue
    </h2>
    <p class="text-fluid-cq-[48px] leading-fluid-cq-[56px] font-bold text-green-600">
      $45K
    </p>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px] text-gray-600">
      This month
    </p>
  </div>

  <!-- Widget 3 -->
  <div class="@container p-6 bg-white rounded-lg">
    <h2 class="text-fluid-cq-[24px] leading-fluid-cq-[32px] font-bold">
      Growth
    </h2>
    <p class="text-fluid-cq-[48px] leading-fluid-cq-[56px] font-bold text-purple-600">
      +23%
    </p>
    <p class="text-fluid-cq-[14px] leading-fluid-cq-[20px] text-gray-600">
      vs last month
    </p>
  </div>
</div>
```

---

## When to Use What

### Viewport-based (`-fluid-*`)
Use when you need elements to respond to the viewport/window size:
- Global typography scales
- Full-width sections
- Elements that should adapt to screen size
- No specific parent container

### Container Query-based (`-fluid-cq-*`)
Use when elements should respond to their container:
- Modular components (cards, widgets)
- Sidebars and panels
- Grid/flex items
- Nested layouts
- Responsive components that can be placed anywhere

### Width/Height vs Max-Width/Max-Height
- `w-fluid-*` / `h-fluid-*`: Fixed but scalable dimensions
- `max-w-fluid-*` / `max-h-fluid-*`: Fluid upper limit, combine with `w-full` for responsive containers

### Font-Size vs Line-Height
- Always combine them for optimal typography
- Use same bounds for consistency across your scale
- Container queries ensure perfect proportions at any size

---

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
