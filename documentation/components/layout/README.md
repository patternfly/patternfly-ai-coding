# Layout Components

This section covers PatternFly layout components and page structure patterns for building consistent application layouts.

## Introduction

PatternFly layout components provide the foundation for structuring application pages and organizing content. These components ensure consistent spacing, responsive behavior, and proper semantic structure across your application.

## Reference Documentation

- [PatternFly Layouts on PatternFly.org](https://www.patternfly.org/layouts)
- [PatternFly React GitHub Repository](https://github.com/patternfly/patternfly-react)

> For the most up-to-date documentation and code examples, consult both PatternFly.org and the official GitHub repository. When using AI tools, leverage context7 to fetch the latest docs from these sources.

## Related Files

- [**Page Sections**](./page-sections.md) - PageSection component usage and patterns
- [**Grid System**](./grid-system.md) - Grid layout and responsive design
- [**Component Architecture**](../../guidelines/component-architecture.md) - Component structure patterns
- [**Styling Standards**](../../guidelines/styling-standards.md) - Layout styling guidelines

## Core Layout Components

### PageSection Component

The [`PageSection`](https://www.patternfly.org/components/page/page-section) component is the primary building block for page content structure.

#### Basic Usage
```jsx
import { PageSection, Content } from '@patternfly/react-core';

const BasicPage = () => (
  <React.Fragment>
    {/* Page Title Section */}
    <PageSection variant="light">
      <Content component="h1">Page Title</Content>
    </PageSection>
    
    {/* Main Content Section */}
    <PageSection hasBodyWrapper>
      <Content component="p">Main page content goes here</Content>
    </PageSection>
  </React.Fragment>
);
```

#### PageSection Variants
```jsx
// Light background for headers/titles
<PageSection variant="light">
  <Content component="h1">Application Title</Content>
</PageSection>

// Default background for main content
<PageSection variant="default">
  <MainContent />
</PageSection>

// Secondary background for supporting content
<PageSection variant="secondary">
  <SupportingContent />
</PageSection>

// Dark background for special sections
<PageSection variant="dark">
  <SpecialContent />
</PageSection>
```

#### Padding Configuration
```jsx
// Standard padding
<PageSection padding={{ default: 'padding' }}>
  <Content>Standard padded content</Content>
</PageSection>

// No padding
<PageSection padding={{ default: 'noPadding' }}>
  <Content>Content with no padding</Content>
</PageSection>

// Responsive padding
<PageSection 
  padding={{ 
    default: 'padding', 
    md: 'paddingLg',
    lg: 'paddingXl' 
  }}
>
  <Content>Responsive padding content</Content>
</PageSection>
```

#### Body Wrapper
```jsx
// Adds pf-vX-c-page__main-body wrapper for standard content padding
<PageSection hasBodyWrapper={true}>
  <div className="pf-v6-u-margin-top-lg">
    Content with body wrapper styling
  </div>
</PageSection>
```

## Common Layout Patterns

### Standard Page Layout
```jsx
import { 
  PageSection, 
  Content, 
  Toolbar, 
  ToolbarContent 
} from '@patternfly/react-core';

const StandardPageLayout = () => (
  <React.Fragment>
    {/* 1. Page Title Section */}
    <PageSection variant="light">
      <Content component="h1">User Management</Content>
      <Content component="p">Manage user accounts and permissions</Content>
    </PageSection>
    
    {/* 2. Toolbar Section */}
    <PageSection padding={{ default: 'noPadding' }}>
      <Toolbar>
        <ToolbarContent>
          {/* Filters, search, actions */}
        </ToolbarContent>
      </Toolbar>
    </PageSection>
    
    {/* 3. Main Content Section */}
    <PageSection hasBodyWrapper>
      <UserTable />
    </PageSection>
  </React.Fragment>
);
```

### Dashboard Layout
```jsx
const DashboardLayout = () => (
  <React.Fragment>
    {/* Dashboard Header */}
    <PageSection variant="light" padding={{ default: 'padding' }}>
      <Content component="h1">Dashboard</Content>
      <Content component="p">System overview and key metrics</Content>
    </PageSection>
    
    {/* Metrics Cards */}
    <PageSection>
      <div className="pf-v6-l-grid pf-v6-m-gutter">
        <div className="pf-v6-l-grid__item pf-v6-m-6-col pf-v6-m-3-col-on-lg">
          <MetricCard title="Users" value="1,234" />
        </div>
        <div className="pf-v6-l-grid__item pf-v6-m-6-col pf-v6-m-3-col-on-lg">
          <MetricCard title="Orders" value="5,678" />
        </div>
        <div className="pf-v6-l-grid__item pf-v6-m-6-col pf-v6-m-3-col-on-lg">
          <MetricCard title="Revenue" value="$12,345" />
        </div>
        <div className="pf-v6-l-grid__item pf-v6-m-6-col pf-v6-m-3-col-on-lg">
          <MetricCard title="Growth" value="+15%" />
        </div>
      </div>
    </PageSection>
    
    {/* Charts and Detailed Content */}
    <PageSection hasBodyWrapper>
      <div className="pf-v6-l-grid pf-v6-m-gutter">
        <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-8-col-on-lg">
          <ChartSection />
        </div>
        <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-4-col-on-lg">
          <ActivityFeed />
        </div>
      </div>
    </PageSection>
  </React.Fragment>
);
```

### Form Layout
```jsx
const FormPageLayout = () => (
  <React.Fragment>
    {/* Form Header */}
    <PageSection variant="light">
      <Content component="h1">Create User</Content>
      <Content component="p">Add a new user to the system</Content>
    </PageSection>
    
    {/* Form Content */}
    <PageSection hasBodyWrapper>
      <div className="pf-v6-l-grid pf-v6-m-gutter">
        <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-8-col-on-lg pf-v6-m-6-col-on-xl">
          <Card>
            <CardTitle>User Information</CardTitle>
            <CardBody>
              <UserForm />
            </CardBody>
          </Card>
        </div>
        <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-4-col-on-lg pf-v6-m-6-col-on-xl">
          <Card>
            <CardTitle>Help</CardTitle>
            <CardBody>
              <HelpContent />
            </CardBody>
          </Card>
        </div>
      </div>
    </PageSection>
  </React.Fragment>
);
```

## Grid System Integration

### Basic Grid Layout
```jsx
import { PageSection } from '@patternfly/react-core';

const GridLayout = () => (
  <PageSection>
    <div className="pf-v6-l-grid pf-v6-m-gutter">
      <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-6-col-on-md">
        <Card>Left Content</Card>
      </div>
      <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-6-col-on-md">
        <Card>Right Content</Card>
      </div>
    </div>
  </PageSection>
);
```

### Responsive Grid Patterns
```jsx
// Three-column responsive layout
<div className="pf-v6-l-grid pf-v6-m-gutter">
  <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-6-col-on-md pf-v6-m-4-col-on-lg">
    <Card>Column 1</Card>
  </div>
  <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-6-col-on-md pf-v6-m-4-col-on-lg">
    <Card>Column 2</Card>
  </div>
  <div className="pf-v6-l-grid__item pf-v6-m-12-col pf-v6-m-12-col-on-md pf-v6-m-4-col-on-lg">
    <Card>Column 3</Card>
  </div>
</div>
```

## Responsive Design Considerations

### Breakpoint-Aware Layouts
```jsx
const ResponsiveLayout = () => (
  <PageSection>
    {/* Mobile: Stack vertically, Desktop: Side by side */}
    <div className="pf-v6-l-flex pf-v6-m-column pf-v6-m-row-on-lg pf-v6-m-gap-md">
      <div className="pf-v6-l-flex__item pf-v6-m-flex-1">
        <MainContent />
      </div>
      <div className="pf-v6-l-flex__item pf-v6-m-flex-none-on-lg" style={{ flexBasis: '300px' }}>
        <Sidebar />
      </div>
    </div>
  </PageSection>
);
```

### Mobile-First Approach
```jsx
// Start with mobile layout, enhance for larger screens
<PageSection>
  <div className="pf-v6-u-display-block pf-v6-u-display-flex-on-lg">
    <div className="pf-v6-u-flex-grow-1 pf-v6-u-margin-bottom-md pf-v6-u-margin-bottom-0-on-lg pf-v6-u-margin-right-lg-on-lg">
      <PrimaryContent />
    </div>
    <div className="pf-v6-u-flex-shrink-0" style={{ width: '250px' }}>
      <SecondaryContent />
    </div>
  </div>
</PageSection>
```

## Accessibility Considerations

### Semantic Structure
```jsx
// Use proper heading hierarchy
<PageSection variant="light">
  <Content component="h1">Main Page Title</Content>  {/* h1 for page title */}
</PageSection>

<PageSection>
  <Content component="h2">Section Title</Content>    {/* h2 for major sections */}
  <div>
    <Content component="h3">Subsection</Content>     {/* h3 for subsections */}
  </div>
</PageSection>
```

### Skip Links and Navigation
```jsx
// Add skip links for keyboard navigation
<PageSection className="pf-v6-u-screen-reader">
  <a href="#main-content" className="pf-v6-c-button pf-m-primary">
    Skip to main content
  </a>
</PageSection>

<PageSection id="main-content" tabIndex="-1">
  <MainContent />
</PageSection>
```

### ARIA Landmarks
```jsx
// Use proper ARIA landmarks
<PageSection component="main" aria-label="Main content">
  <PrimaryContent />
</PageSection>

<PageSection component="aside" aria-label="Sidebar">
  <SidebarContent />
</PageSection>
```

## Performance Optimization

### Lazy Loading Sections
```jsx
import { lazy, Suspense } from 'react';
import { Spinner } from '@patternfly/react-core';

const LazySection = lazy(() => import('./HeavySection'));

const OptimizedLayout = () => (
  <React.Fragment>
    <PageSection variant="light">
      <Content component="h1">Page Title</Content>
    </PageSection>
    
    <PageSection>
      <Suspense fallback={<Spinner />}>
        <LazySection />
      </Suspense>
    </PageSection>
  </React.Fragment>
);
```

### Conditional Rendering
```jsx
const ConditionalLayout = ({ showSidebar, isLoading }) => (
  <PageSection>
    <div className="pf-v6-l-flex pf-v6-m-gap-md">
      <div className="pf-v6-l-flex__item pf-v6-m-flex-1">
        {isLoading ? <LoadingSpinner /> : <MainContent />}
      </div>
      {showSidebar && (
        <div className="pf-v6-l-flex__item pf-v6-m-flex-none">
          <Sidebar />
        </div>
      )}
    </div>
  </PageSection>
);
```

## Best Practices

### Layout Do's
- ✅ Use PageSection for all major page areas
- ✅ Follow consistent page structure patterns
- ✅ Implement responsive design from mobile-first
- ✅ Use proper semantic HTML structure
- ✅ Maintain consistent spacing with PatternFly utilities
- ✅ Test layouts across different screen sizes
- ✅ Use hasBodyWrapper for standard content padding

### Layout Don'ts
- ❌ Skip PageSection for page structure
- ❌ Mix layout systems inconsistently
- ❌ Ignore responsive design requirements
- ❌ Use custom CSS when PatternFly layout classes exist
- ❌ Create overly complex nested layouts
- ❌ Forget accessibility considerations
- ❌ Hardcode spacing values instead of using utilities

## Common Layout Issues

### Troubleshooting
1. **Spacing Issues**: Use PatternFly spacing utilities instead of custom margins
2. **Responsive Problems**: Test on actual devices, not just browser resize
3. **Overflow Issues**: Check container widths and use proper flex/grid properties
4. **Accessibility Violations**: Validate semantic structure and ARIA labels
5. **Performance Problems**: Implement lazy loading for heavy sections

For detailed troubleshooting, see [Common Issues](../../troubleshooting/common-issues.md#layout-issues).