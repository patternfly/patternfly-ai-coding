# Table Component Rules

Essential rules for PatternFly table components, including usage, sorting, selection, performance, accessibility, and best practices.

## Required Table Structure
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

## Sorting Rules
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

## Selection Rules
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

## Performance Rules
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