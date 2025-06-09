# Component Architecture

Essential rules for structuring PatternFly components and organizing component hierarchies.

## Related Files
- [**PatternFly Guidelines**](./README.md) - Core development principles
- [**Styling Rules**](./styling-standards.md) - CSS and styling approaches
- [**Layout Rules**](../components/layout/README.md) - Page structure patterns
- [**Table Component Rules**](../components/data-display/table.md) - Table usage and best practices
- [**Data View Component Rules**](../components/data-display/README.md) - Data view usage and best practices

## Component Composition Rules

### PatternFly-First Approach
- ✅ **Always start with PatternFly components** - Before creating custom solutions
- ✅ **Compose PatternFly components** - Build complex UIs by combining them
- ❌ **Don't create custom components** - When PatternFly components exist

```jsx
// ✅ Correct - Compose PatternFly components
import { Card, CardTitle, CardBody, Button, Content } from '@patternfly/react-core';

const UserCard = ({ user, onEdit }) => (
  <Card>
    <CardTitle>
      <Content component="h3">{user.name}</Content>
    </CardTitle>
    <CardBody>
      <Content component="p">{user.email}</Content>
      <Button variant="secondary" onClick={onEdit}>Edit</Button>
    </CardBody>
  </Card>
);
```

### Page Structure Rules
```jsx
// ✅ Standard page pattern
<React.Fragment>
  <PageSection variant="light">
    <Content component="h1">Page Title</Content>
  </PageSection>
  <PageSection hasBodyWrapper>
    <Toolbar><ToolbarContent>{/* filters */}</ToolbarContent></Toolbar>
    <MainContent />
  </PageSection>
</React.Fragment>
```

### Component Hierarchy
1. **Page Components** - Top-level page structure
2. **Section Components** - Major page sections
3. **Feature Components** - Specific functionality
4. **PatternFly Components** - Base components

## State Management Rules

### Local State
- ✅ **Use useState for component-specific state** - Form inputs, toggles, local UI state
- ✅ **Use useCallback and useMemo** - For performance optimization
- ❌ **Don't lift state unnecessarily** - Keep state as local as possible

### Shared State
- ✅ **Use Context for shared state** - When multiple components need same data
- ✅ **Use useReducer for complex state** - When state logic is complex
- ❌ **Don't use global state for everything** - Only when truly needed

## Common Pattern Rules

### Table with Selection
```jsx
// ✅ Required pattern for selectable tables
import { Table, Thead, Tbody, Tr, Th, Td, Checkbox } from '@patternfly/react-table';

// Use Set for selection state management
const [selectedItems, setSelectedItems] = useState(new Set());

// Handle indeterminate state for "select all"
const isAllSelected = selectedItems.size === data.length && data.length > 0;
const isPartiallySelected = selectedItems.size > 0 && selectedItems.size < data.length;

<Checkbox
  isChecked={isAllSelected ? true : isPartiallySelected ? null : false}
  onChange={handleSelectAll}
/>
```

### Dropdown Actions
```jsx
// ✅ Required pattern for action dropdowns
import { Dropdown, DropdownList, DropdownItem, MenuToggle } from '@patternfly/react-core';
import { EllipsisVIcon } from '@patternfly/react-icons';

// Always use popperProps to prevent clipping
<Dropdown
  popperProps={{ position: 'right', enableFlip: true, appendTo: () => document.body }}
  toggle={(toggleRef) => (
    <MenuToggle ref={toggleRef} variant="plain">
      <EllipsisVIcon />
    </MenuToggle>
  )}
>
```

### Toolbar with Filters
```jsx
// ✅ Required pattern for data filtering
import { Toolbar, ToolbarContent, ToolbarFilter, ToolbarToggleGroup } from '@patternfly/react-core';

<Toolbar clearAllFilters={onClearFilters} collapseListedFiltersBreakpoint="xl">
  <ToolbarContent>
    <ToolbarToggleGroup toggleIcon={<FilterIcon />} breakpoint="xl">
      <ToolbarFilter labels={activeFilters} deleteLabel={removeFilter}>
        {/* Filter components */}
      </ToolbarFilter>
    </ToolbarToggleGroup>
  </ToolbarContent>
</Toolbar>
```

## Error Handling Rules

### Required Error States
- ✅ **Always implement error boundaries** - Catch component errors
- ✅ **Handle loading states** - Show spinners or skeletons
- ✅ **Handle empty states** - Show appropriate empty state messages
- ✅ **Handle error states** - Show error messages with retry options

```jsx
// ✅ Required error boundary pattern
import { EmptyState, EmptyStateHeader, EmptyStateIcon } from '@patternfly/react-core';

if (isLoading) return <Spinner />;
if (error) return <EmptyState><EmptyStateHeader titleText="Error" /></EmptyState>;
if (!data?.length) return <EmptyState><EmptyStateHeader titleText="No data" /></EmptyState>;
```

## Performance Rules

### Required Optimizations
- ✅ **Use React.memo for list items** - Prevent unnecessary re-renders
- ✅ **Use useCallback for event handlers** - Stable references
- ✅ **Use useMemo for expensive calculations** - Cache computed values
- ✅ **Implement virtualization for large lists** - Use react-window for 1000+ items

### Testing Rules
- ✅ **Test component interactions** - User events and state changes
- ✅ **Test accessibility** - ARIA labels and keyboard navigation
- ✅ **Test error states** - Loading, error, and empty states
- ❌ **Don't test PatternFly component internals** - Focus on your component logic

## Essential Do's and Don'ts

### ✅ Do's
- Compose PatternFly components to build complex UIs
- Use proper component hierarchy and separation of concerns
- Implement error boundaries and loading states
- Use React hooks for state management
- Memoize expensive computations and callbacks
- Write tests for component behavior

### ❌ Don'ts
- Create custom components when PatternFly components exist
- Mix state management patterns inconsistently
- Ignore error handling and loading states
- Create deeply nested component hierarchies
- Skip performance optimization for large data sets
- Tightly couple components to specific data structures

## Quick Reference
- **[PatternFly Components](https://www.patternfly.org/components)** - Official component documentation
- **[React Patterns](https://reactpatterns.com/)** - Common React patterns
- **[Testing Library](https://testing-library.com/)** - Component testing best practices