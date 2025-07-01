# Styling Standards

Essential CSS and styling rules for PatternFly React applications.

## Related Files
- [**PatternFly Guidelines**](./README.md) - Core development principles
- [**Component Rules**](./component-architecture.md) - Component structure patterns
- [**Layout Rules**](../components/layout/README.md) - Page layout styling

## Class Naming Rules

### PatternFly v6 Requirements
- ✅ **ALWAYS use `pf-v6-` prefix** - All PatternFly v6 classes
- ❌ **NEVER use legacy prefixes** - No `pf-v5-`, `pf-v4-`, `pf-u` or `pf-c-`

```css
/* ✅ Correct v6 classes */
.pf-v6-c-button          /* Components */
.pf-v6-u-m-md            /* Utilities */
.pf-v6-l-grid            /* Layouts */

/* ❌ Wrong - Don't use these */
.pf-v5-c-button
.pf-u-m-md
.pf-c-button
```

## Component Composition Rules

> **Component-first approach:** Use proper PatternFly component composition for layout and spacing. Components should be children of appropriate containers like PageSection, ActionGroup, Stack, etc.

### Use Component Composition First
```jsx
// ✅ Correct - Use proper component composition
<PageSection>
  <Stack hasGutter>
    <Title headingLevel="h1">Dashboard</Title>
    <Content>Dashboard content</Content>
  </Stack>
</PageSection>

// ❌ Wrong - Utility classes for basic layout
<div className="pf-v6-u-m-md">
  <div className="pf-v6-u-mb-sm">Dashboard</div>
  <div>Dashboard content</div>
</div>
```

### Use Component Props Second
```jsx
// ✅ Correct - Use component props for spacing and layout
<Table borders={false} gridBreakPoint="grid-lg">
  <Thead>
    <Tr>
      <Th modifier="nowrap">Name</Th>
    </Tr>
  </Thead>
</Table>

<ActionGroup>
  <Button variant="primary">Save</Button>
  <Button variant="secondary">Cancel</Button>
</ActionGroup>

// ❌ Wrong - Utility classes when component props exist
<Table className="pf-v6-u-m-md">
  <Button className="pf-v6-u-mr-sm">Save</Button>
  <Button>Cancel</Button>
</Table>
```

### Common Component Patterns for Layout
```jsx
// Page structure
<PageSection>
  <Stack hasGutter>
    <Title headingLevel="h1">Page Title</Title>
    <Grid hasGutter>
      <GridItem span={8}>
        <Card>
          <CardTitle>Card Title</CardTitle>
          <CardBody>Card content</CardBody>
        </Card>
      </GridItem>
    </Grid>
  </Stack>
</PageSection>

// Form structure
<Form>
  <FormGroup label="Username">
    <TextInput />
  </FormGroup>
  <ActionGroup>
    <Button variant="primary">Submit</Button>
  </ActionGroup>
</Form>
```

### When to Use Utility Classes
Use utility classes only when:
- Component composition doesn't provide the needed layout
- Component props don't offer the required styling
- You need to override specific styling for edge cases

```jsx
// ✅ Acceptable utility usage - when component props aren't sufficient
<Card className="pf-v6-u-h-100"> {/* Force card to full height */}
  <CardBody>
    <Text className="pf-v6-u-text-align-center"> {/* Center text when component doesn't provide prop */}
      Centered content
    </Text>
  </CardBody>
</Card>
```

## Design Token Rules

### Use Semantic PatternFly Tokens for Custom CSS
- ✅ **Use semantic tokens** (e.g., `--pf-t--global--text--color--regular`) for custom CSS. These tokens do not end in numbers and are intended for application-level styling.
- ❌ **Don't use base tokens** (which end in numbers, e.g., `--pf-t--global--text--color--100`) for custom CSS. Base tokens are for internal PatternFly use and may change.

```css
.custom-component {
  /* ✅ Correct - Use semantic tokens */
  color: var(--pf-t--global--text--color--regular);
  margin: var(--pf-t-global--spacer--md);
  
  /* ❌ Wrong - Hardcoded values or base tokens */
  /* color: #333333; */
  /* color: var`--pf-t--global--text--color--100); */
  /* margin: 16px; */
}
```

### Essential Token Categories
```css
/* Semantic Colors */
--pf-t--global--text--color--regular
--pf-t--global--text--color--subtle
--pf-t--global--background--color--primary--default

/* Spacing */
--pf-t-global--spacer--{xs|sm|md|lg|xl}

/* Typography */
--pf-t--global--font--family--body	
--pf-t--global--font--size--md	
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
// ✅ Use PatternFly variants and ActionGroup for spacing
<ActionGroup>
  <Button variant="primary">Save</Button>
  <Button variant="secondary">Cancel</Button>
</ActionGroup>

// ❌ Wrong - Utility classes for button spacing
<div>
  <Button className="pf-v6-u-margin-right-sm">Save</Button>
  <Button>Cancel</Button>
</div>
```

### Form Styling
```jsx
// ✅ Use PageSection and proper form structure
<PageSection>
  <Form>
    <FormGroup label="Username" isRequired>
      <TextInput />
    </FormGroup>
    <ActionGroup>
      <Button variant="primary">Submit</Button>
    </ActionGroup>
  </Form>
</PageSection>

// ❌ Wrong - Utility classes for form layout
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
- Use proper PatternFly component composition (PageSection, Stack, Grid, ActionGroup)
- Leverage component props for spacing, borders, and layout (Table borders, ActionGroup spacing)
- Use PatternFly v6 components and design patterns exclusively
- Use utility classes only as a last resort when composition and props aren't sufficient
- Use PatternFly design tokens for any custom styles
- Test responsive behavior on different screen sizes

### ❌ Don'ts
- Use utility classes for basic layout when proper component composition exists
- Skip using component props in favor of utility classes
- Mix PatternFly versions
- Override PatternFly component internals
- Use hardcoded values instead of design tokens
- Create custom layout when PatternFly layout components exist

## Quick Reference
- **[PatternFly Utilities](https://www.patternfly.org/utilities)** - Complete utility documentation
- **[Design Tokens](https://www.patternfly.org/tokens)** - Available design tokens
- **[Responsive Design](https://www.patternfly.org/layouts)** - Layout and responsive patterns

## Do/Don't Examples

### Proper Layout and Spacing
**Do:**
```jsx
// Use proper component composition
<PageSection>
  <Stack hasGutter>
    <Title headingLevel="h1" size="lg">Content Title</Title>
    <Content>Content goes here</Content>
  </Stack>
</PageSection>
```
**Don't:**
```jsx
// Avoid inline styles or utility classes for basic layout
<div style={{ margin: 16, textAlign: 'center' }}>Content</div>
<div className="pf-v6-u-margin-md pf-v6-u-text-align-center">Content</div>
```

### Use Component Props for Spacing
**Do:**
```jsx
// Use component props when available
<Table borders={false} gridBreakPoint="grid-md">
  <Thead>
    <Tr>
      <Th modifier="nowrap">Name</Th>
    </Tr>
  </Thead>
</Table>
```
**Don't:**
```jsx
// Don't use utility classes when component props exist
<Table className="pf-v6-u-margin-md">
  <Thead>
    <Tr>
      <Th className="pf-v6-u-white-space-nowrap">Name</Th>
    </Tr>
  </Thead>
</Table>
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

## Spacing and Inline Styles

- ✅ **Always use PatternFly spacing variables (design tokens) for all spacing, including in inline style props.**
- ❌ **Do not use hardcoded numbers for margin, padding, or other spacing in inline styles.**

**Correct:**
```jsx
<div style={{ marginBottom: 'var(--pf-t--global--spacer-lg)' }} />
```

**Incorrect:**
```jsx
<div style={{ marginBottom: 24 }} />
```

## Utility Classes vs Inline Styles

- ✅ **Prefer using PatternFly utility classes for spacing, alignment, and layout instead of inline styles.**
- ❌ **Only use inline styles if a PatternFly utility class does not exist for the required spacing or layout.**

**Correct:**
```jsx
<div className="pf-v6-u-mb-lg" />
```

**Incorrect:**
```jsx
<div style={{ marginBottom: 'var(--pf-t--global--spacer-lg)' }} />
```

## External Link Buttons

- ✅ **Always add an external link icon to the right of the text for external link buttons.**
- ❌ **Do not omit the external link icon for buttons that open external sites.**

**Correct:**
```jsx
import { ExternalLinkAltIcon } from '@patternfly/react-icons';
<Button
  variant="link"
  component="a"
  href="https://patternfly.org"
  target="_blank"
  rel="noopener noreferrer"
  icon={<ExternalLinkAltIcon />}
  iconPosition="right"
>
  Learn more
</Button>
```

**Incorrect:**
```jsx
<Button
  variant="link"
  component="a"
  href="https://patternfly.org"
  target="_blank"
  rel="noopener noreferrer"
>
  Learn more
</Button>
```

## Toolbar Alignment

- ✅ **When right-aligning content in a PatternFly Toolbar, use the ToolbarItem align={{ default: 'alignEnd' }} prop.**
- ❌ **Do not use custom Flex wrappers or utility classes to right-align Toolbar content.**

**Correct:**
```jsx
<Toolbar>
  <ToolbarContent>
    <ToolbarItem>Left content</ToolbarItem>
    <ToolbarItem align={{ default: 'alignEnd' }}>Right-aligned content</ToolbarItem>
  </ToolbarContent>
</Toolbar>
```

**Incorrect:**
```jsx
<Toolbar>
  <ToolbarContent>
    <ToolbarItem>Left content</ToolbarItem>
    <Flex style={{ flex: 1 }} justifyContent={{ default: 'justifyContentFlexEnd' }}>
      <FlexItem>Right-aligned content</FlexItem>
    </Flex>
  </ToolbarContent>
</Toolbar>
```