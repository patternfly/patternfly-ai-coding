# Styling Standards

Essential CSS and styling rules for PatternFly React applications.

## Related Files
- [**PatternFly Guidelines**](./README.md) - Core development principles
- [**Component Rules**](./component-architecture.md) - Component structure patterns
- [**Layout Rules**](../components/layout/README.md) - Page layout styling

## Class Naming Rules

### PatternFly v6 Requirements
- ✅ **ALWAYS use `pf-v6-` prefix** - All PatternFly v6 classes
- ❌ **NEVER use legacy prefixes** - No `pf-v5-`, `pf-v4-`, or `pf-c-`

```css
/* ✅ Correct v6 classes */
.pf-v6-c-button          /* Components */
.pf-v6-u-margin-md       /* Utilities */
.pf-v6-l-grid            /* Layouts */

/* ❌ Wrong - Don't use these */
.pf-v5-c-button
.pf-c-button
```

## Utility-First Rules

> **No inline styles:** Use PatternFly layout and spacing utilities instead of `style` props or custom CSS for layout and spacing.

### Use PatternFly Utilities First
```jsx
// ✅ Correct - Use PatternFly utilities
<div className="pf-v6-u-text-align-center pf-v6-u-margin-md">

// ❌ Wrong - Custom CSS when utilities exist
<div className="custom-centered-title">
```

### Common Utility Patterns
```css
/* Spacing */
.pf-v6-u-margin-{xs|sm|md|lg|xl}
.pf-v6-u-padding-{xs|sm|md|lg|xl}
.pf-v6-u-margin-top-md
.pf-v6-u-padding-left-lg

/* Typography */
.pf-v6-u-text-align-{left|center|right}
.pf-v6-u-font-weight-{light|normal|bold}
.pf-v6-u-font-size-{sm|md|lg}

/* Colors */
.pf-v6-u-color-{primary|secondary|success|warning|danger}
.pf-v6-u-background-color-primary
```

## Design Token Rules

### Use Semantic PatternFly Tokens for Custom CSS
- ✅ **Use semantic tokens** (e.g., `--pf-v6-global--primary-color--light`) for custom CSS. These tokens do not end in numbers and are intended for application-level styling.
- ❌ **Don't use base tokens** (which end in numbers, e.g., `--pf-v6-global--Color--100`) for custom CSS. Base tokens are for internal PatternFly use and may change.

```css
.custom-component {
  /* ✅ Correct - Use semantic tokens */
  color: var(--pf-v6-global--primary-color--light);
  margin: var(--pf-v6-global--spacer--md);
  
  /* ❌ Wrong - Hardcoded values or base tokens */
  /* color: #333333; */
  /* color: var(--pf-v6-global--Color--100); */
  /* margin: 16px; */
}
```

### Essential Token Categories
```css
/* Semantic Colors */
--pf-v6-global--primary-color--light
--pf-v6-global--primary-color--dark
--pf-v6-global--background-color--light

/* Spacing */
--pf-v6-global--spacer--{xs|sm|md|lg|xl}

/* Typography */
--pf-v6-global--FontFamily--text
--pf-v6-global--FontSize--md
```

## Responsive Design Rules

### Use PatternFly Responsive Utilities
```css
/* Mobile-first responsive patterns */
.pf-v6-u-display-none-on-sm      /* Hide on small screens */
.pf-v6-u-display-block-on-md     /* Show on medium+ */
.pf-v6-u-text-align-center-on-lg /* Center on large+ */
```

### Grid Layout Patterns
```jsx
<div className="pf-v6-l-grid pf-v6-m-gutter">
  <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-6-col-on-md">
    Responsive content
  </div>
</div>
```

## Component Styling Rules

> **No emojis or raw icons:** Always use PatternFly's React icon components (from `@patternfly/react-icons`) for all icons, including status, trend, and navigation icons.
> 
> **No direct HTML headings or paragraphs:** Use PatternFly's `Title` for headings and `Content` with `component="p"` for paragraphs.

### Button Styling
```jsx
// ✅ Use PatternFly variants
<Button variant="primary">Primary</Button>
<Button variant="secondary">Secondary</Button>

// ✅ Add utilities for spacing
<Button className="pf-v6-u-margin-right-sm">Save</Button>
```

### Form Styling
```jsx
<Form className="pf-v6-u-margin-md">
  <FormGroup label="Username" isRequired>
    <TextInput className="pf-v6-u-width-100" />
  </FormGroup>
</Form>
```

## Performance Rules

### CSS Efficiency
- ✅ **Use single utility classes** - More efficient than custom CSS
- ✅ **Import only needed CSS** - Tree shake unused styles
- ❌ **Don't create custom classes** - When PatternFly utilities exist

## Troubleshooting Rules

### Common Issues
1. **Missing styles** - Ensure PatternFly CSS is imported
2. **Class conflicts** - PatternFly classes should not be overridden
3. **Version mismatches** - All PatternFly packages must use same version

### Debug Tools
- **Browser DevTools** - Inspect applied PatternFly classes
- **PatternFly DevTools** - Browser extension for debugging

## Utility Class Usage Guidance

> **Caution:** Avoid over-relying on utility classes to style components. Prefer using the component's own props and API for layout and appearance, as these are designed for recommended use cases. Use utility classes only when necessary, and add a comment explaining why the utility class is required. This approach helps ensure your code remains maintainable and aligned with future PatternFly updates.

## Essential Do's and Don'ts

### ✅ Do's
- Use PatternFly v6 classes exclusively
- Prefer component props and API for styling before using utility classes
- Use utility classes minimally, with comments explaining their necessity
- Use PatternFly design tokens for custom styles
- Test responsive behavior on different screen sizes
- Follow mobile-first responsive patterns

### ❌ Don'ts
- Over-rely on utility classes to force component appearance
- Mix PatternFly versions
- Override PatternFly component internals
- Use hardcoded values instead of design tokens
- Create custom CSS when utilities exist
- Ignore responsive design requirements

## Quick Reference
- **[PatternFly Utilities](https://www.patternfly.org/utilities)** - Complete utility documentation
- **[Design Tokens](https://www.patternfly.org/tokens)** - Available design tokens
- **[Responsive Design](https://www.patternfly.org/layouts)** - Layout and responsive patterns

## Do/Don't Examples

### No Inline Styles
**Do:**
```jsx
// Use PatternFly utility classes
<div className="pf-v6-u-margin-md pf-v6-u-text-align-center">Content</div>
```
**Don't:**
```jsx
// Avoid style props for layout/spacing
<div style={{ margin: 16, textAlign: 'center' }}>Content</div>
```

### No Emojis or Raw Icons
**Do:**
```jsx
import ArrowUpIcon from '@patternfly/react-icons/dist/esm/icons/arrow-up-icon';
<ArrowUpIcon title="Trend up" />
```
**Don't:**
```jsx
<span role="img" aria-label="trend up">📈</span>
```

### No Direct HTML Headings or Paragraphs
**Do:**
```jsx
import { Title, Content } from '@patternfly/react-core';
<Title headingLevel="h1">Dashboard</Title>
<Content component="p">This is a PatternFly app.</Content>
```
**Don't:**
```jsx
<h1>Dashboard</h1>
<p>This is a PatternFly app.</p>
```

---

> **Note:** `PageHeader` is not a PatternFly component in v6+. Use `PageSection`, `Title`, and layout components instead.