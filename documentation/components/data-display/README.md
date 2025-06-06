# Data Display Rules

Essential rules for PatternFly data display components including tables, lists, and data presentation.

## Related Files
- [**Component Architecture**](../../guidelines/component-architecture.md) - Data component structure rules
- [**Layout Rules**](../layout/README.md) - Page structure patterns

## Table Component Rules

### Required Table Structure
- ✅ **Use composable Table components** - `Table`, `Thead`, `Tbody`, `Tr`, `Th`, `Td`
- ✅ **Import from @patternfly/react-table** - Not @patternfly/react-core
- ❌ **Don't create custom table components** - Use PatternFly's composable approach

```jsx
// ✅ Correct table structure
import { Table, Thead, Tbody, Tr, Th, Td } from '@patternfly/react-table';

<Table>
  <Thead>
    <Tr>
      <Th>Name</Th>
      <Th>Email</Th>
    </Tr>
  </Thead>
  <Tbody>
    {data.map(item => (
      <Tr key={item.id}>
        <Td>{item.name}</Td>
        <Td>{item.email}</Td>
      </Tr>
    ))}
  </Tbody>
</Table>
```

### Sorting Rules
- ✅ **Use sort prop on Th components** - Configure sorting via the `sort` prop
- ✅ **Manage sort state with useState** - Track sortBy state
- ✅ **Use useMemo for sorted data** - Performance optimization

```jsx
// ✅ Required sorting pattern
const [sortBy, setSortBy] = useState({});

<Th sort={{ sortBy, onSort: handleSort, columnIndex: 0 }}>
  Name
</Th>
```

### Selection Rules
- ✅ **Use Set for selection state** - More efficient than arrays
- ✅ **Handle indeterminate state** - For "select all" checkbox
- ✅ **Use proper ARIA labels** - For accessibility

```jsx
// ✅ Required selection pattern
const [selectedItems, setSelectedItems] = useState(new Set());

const isAllSelected = selectedItems.size === data.length && data.length > 0;
const isPartiallySelected = selectedItems.size > 0 && selectedItems.size < data.length;

<Checkbox
  isChecked={isAllSelected ? true : isPartiallySelected ? null : false}
  onChange={handleSelectAll}
  aria-label="Select all rows"
/>
```

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