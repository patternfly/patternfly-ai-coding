# Data Display Rules

Essential rules for PatternFly data display components including lists, data presentation, and data view patterns.

## Related Files
- [**Component Architecture**](../../guidelines/component-architecture.md) - Data component structure rules
- [**Layout Rules**](../layout/README.md) - Page structure patterns
- [**Table Documentation**](./table.md) - Table component rules and best practices

## Dropdown Action Rules

### Required Dropdown Pattern
- ✅ **Use MenuToggle with variant="plain"** - For kebab-style dropdowns
- ✅ **Configure popperProps** - Prevent clipping issues
- ✅ **Use EllipsisVIcon** - Standard kebab menu icon

```jsx
// ✅ Required dropdown pattern
import { Dropdown, DropdownList, DropdownItem, MenuToggle, Divider } from '@patternfly/react-core';
import { EllipsisVIcon } from '@patternfly/react-icons';

<Dropdown
  popperProps={{
    position: 'right',
    enableFlip: true,
    appendTo: () => document.body  // Prevents clipping
  }}
  toggle={(toggleRef) => (
    <MenuToggle ref={toggleRef} variant="plain" aria-label={`Actions for ${item.name}`}>
      <EllipsisVIcon />
    </MenuToggle>
  )}
>
  <DropdownList>
    <DropdownItem onClick={() => onEdit(item)}>Edit</DropdownItem>
    <Divider />
    <DropdownItem onClick={() => onDelete(item)}>Delete</DropdownItem>
  </DropdownList>
</Dropdown>
```

## Toolbar Rules

### Required Toolbar Pattern
- ✅ **Use clearAllFilters prop** - For "Clear all filters" functionality
- ✅ **Use ToolbarFilter with labels** - Display active filters as chips
- ✅ **Use ToolbarToggleGroup** - For responsive filter collapsing
- ✅ **Show bulk actions when items selected** - Conditional bulk action UI

```jsx
// ✅ Required toolbar pattern
import { Toolbar, ToolbarContent, ToolbarFilter, ToolbarToggleGroup } from '@patternfly/react-core';

<Toolbar
  clearAllFilters={onClearFilters}
  clearFiltersButtonText="Clear all filters"
  collapseListedFiltersBreakpoint="xl"
>
  <ToolbarContent>
    {selectedCount > 0 && (
      <ToolbarGroup>
        <ToolbarItem>{selectedCount} selected</ToolbarItem>
        <ToolbarItem><BulkActionsDropdown /></ToolbarItem>
      </ToolbarGroup>
    )}
    <ToolbarToggleGroup toggleIcon={<FilterIcon />} breakpoint="xl">
      <ToolbarFilter labels={activeFilters} deleteLabel={removeFilter}>
        <SearchInput />
      </ToolbarFilter>
    </ToolbarToggleGroup>
  </ToolbarContent>
</Toolbar>
```

## State Management Rules

### Required State Patterns
- ✅ **Use Set for selection** - More efficient than arrays
- ✅ **Handle loading states** - Show spinners or skeletons
- ✅ **Handle empty states** - Show appropriate messages
- ✅ **Handle error states** - Show error messages with retry

```jsx
// ✅ Required state management
const [selectedItems, setSelectedItems] = useState(new Set());
const [isLoading, setIsLoading] = useState(false);
const [error, setError] = useState(null);

if (isLoading) return <Skeleton />;
if (error) return <EmptyState><EmptyStateHeader titleText="Error" /></EmptyState>;
if (!data?.length) return <EmptyState><EmptyStateHeader titleText="No data" /></EmptyState>;
```

## Performance Rules

### Required Optimizations
- ✅ **Use virtualization for 1000+ rows** - react-window library
- ✅ **Use pagination for large datasets** - Better UX than virtualization
- ✅ **Memoize table rows** - React.memo for performance
- ✅ **Use useCallback for handlers** - Stable references

```jsx
// ✅ Required for large datasets
import { FixedSizeList as List } from 'react-window';
import { Pagination } from '@patternfly/react-core';

// For 1000+ items, use virtualization
<List height={400} itemCount={data.length} itemSize={50}>
  {Row}
</List>

// For better UX, use pagination
<Pagination itemCount={data.length} perPage={20} page={page} />
```

## Essential Do's and Don'ts

### ✅ Do's
- Use composable Table components (Thead, Tbody, Tr, Th, Td)
- Implement proper sorting with sort prop on Th components
- Use Checkbox components for selectable rows
- Configure dropdown positioning with popperProps
- Provide empty states for no data and filtered results
- Implement loading states with skeletons or spinners
- Use proper ARIA labels for accessibility

### ❌ Don'ts
- Create custom table components when PatternFly Table exists
- Ignore responsive design for data tables
- Skip loading and empty states
- Forget to handle dropdown clipping issues
- Use inconsistent selection patterns
- Skip accessibility considerations for interactive elements

## Common Issues

### Dropdown Clipping
```jsx
// ✅ Solution: Use appendTo to prevent clipping
<Dropdown popperProps={{ appendTo: () => document.body }}>
```

### Performance Issues
- **1000+ rows**: Use virtualization with react-window
- **Large datasets**: Implement pagination
- **Slow rendering**: Memoize components with React.memo

### Selection Issues
- **Use Set not Array**: More efficient for selection state
- **Handle indeterminate**: For "select all" checkbox state
- **Provide feedback**: Show selected count and bulk actions

## Quick Reference
- **[Table Component](https://www.patternfly.org/components/table)** - Official table documentation
- **[Toolbar Component](https://www.patternfly.org/components/toolbar)** - Toolbar with filters
- **[Dropdown Component](https://www.patternfly.org/components/menus/dropdown)** - Dropdown positioning

## Data View Component Rules

PatternFly Data View provides a standardized way to present and interact with tabular or list-based data, following PatternFly design and accessibility guidelines.

### Installation
```bash
npm install @patternfly/react-data-view
```

### Required CSS Import
```jsx
import '@patternfly/react-data-view/dist/css/main.css';
```

### Import Pattern
- ✅ **Use dynamic imports** from `/dist/dynamic/` paths
- ❌ **Don't use standard imports**

```jsx
// ✅ Correct
import DataView from '@patternfly/react-data-view/dist/dynamic/DataView';
```

### Basic Usage Example
```jsx
import DataView from '@patternfly/react-data-view/dist/dynamic/DataView';

<DataView
  data={data}
  columns={columns}
  onRowClick={handleRowClick}
/>
```

### Component API
- Use PatternFly naming conventions for props (e.g., `variant`, `onClick`)
- Extend PatternFly types when possible
- Document all props and usage examples
- Avoid unnecessary external dependencies

#### Example API Extension
```ts
// when possible, extend available PatternFly types
export interface DataViewProps extends TableProps {
  customLabel?: string;
}

export const DataView: React.FunctionComponent<DataViewProps> = ({ customLabel, ...props }) => ( /* ... */ );
```

### Directory Structure
```
src
|- DataView
   |- index.ts
   |- DataView.tsx
```

### OUIA ID Convention
For testing, use the component name as the default OUIA ID, and for subcomponents, use `ComponentName-element-specification`.
```ts
ouiaId="DataView-actions-button"
```

### Testing & Linting
- Add unit tests to `DataView.test.tsx`
- Add Cypress component/E2E tests to `cypress/component/DataView.cy.tsx` and `cypress/e2e/DataView.spec.cy.ts`
- Run tests and linting:
```bash
npm run test
npm run lint
```

### Accessibility
- Provide proper ARIA labels and roles
- Ensure keyboard navigation and screen reader support
- Run accessibility tests:
```bash
npm run build:docs
npm run serve:docs
npm run test:a11y
npm run serve:a11y
```

### Documentation Example (Markdown)
```md
---
section: extensions
subsection: Data view
id: DataView
propComponents: ['DataView']
sourceLink: https://github.com/patternfly/react-data-view/blob/main/packages/module/patternfly-docs/content/extensions/data-view/examples/DataView/DataView.md
---

import DataView from "@patternfly/react-data-view/dist/dynamic/DataView";

## Component usage

<DataView ... />

### DataView component example label

```js file="./DataViewExample.tsx"```
```

### References
- [PatternFly React Data View GitHub](https://github.com/patternfly/react-data-view)
- [PatternFly Data View NPM](https://www.npmjs.com/package/@patternfly/react-data-view)

> **Note:** Always consult the latest PatternFly Data View documentation and demo source code for up-to-date usage patterns and best practices.

### Real-World Example: OpenShift Console

A production example of PatternFly Data View usage can be found in the OpenShift Console codebase:
- [DataViewPodList.tsx on GitHub](https://github.com/openshift/console/blob/79d29bca8440a5ad82b5257bb0f37bc24384eb0e/frontend/public/components/data-view-poc/DataViewPodList.tsx)

**Key integration patterns and best practices from this example:**
- Integrates Data View with live Kubernetes data (pods) and application state.
- Demonstrates how to pass dynamic data and columns to the Data View component.
- Shows how to handle loading, error, and empty states in a real product context.
- Illustrates the use of PatternFly composable components for custom row rendering and actions.
- Provides a template for connecting Data View to Redux or other state management solutions.

> For advanced usage, review the linked file to see how Data View is composed with other PatternFly and application-specific components.
