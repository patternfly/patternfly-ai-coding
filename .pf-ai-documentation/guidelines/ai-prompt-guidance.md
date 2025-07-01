# AI Prompt Guidance for PatternFly Development

Guidelines for creating effective prompts when using AI coding assistants with PatternFly React applications.

## Why Specific Prompts Matter

Based on workshop feedback, AI coding assistants work best with PatternFly when given specific, detailed prompts. Vague prompts often result in:
- Non-existent component usage → See [Common Issues](../troubleshooting/common-issues.md#ai-coding-specific-issues)
- Incorrect styling approaches → See [Styling Standards](./styling-standards.md)
- Missing accessibility features → See [Guidelines](./README.md#accessibility-requirements)

## Essential Prompt Template

```
Create a [FEATURE] using PatternFly v6 React components. Requirements:
- Follow PatternFly component composition patterns (see styling-standards.md)
- Use component props for spacing/layout before considering utility classes
- Ensure keyboard accessibility with proper ARIA labels
- Verify all components exist in PatternFly packages before using
- [SPECIFIC_FEATURE_REQUIREMENTS]
- Reference: [LINK_TO_RELEVANT_DOCS]
```

## Prompt Strategy by Use Case

### Dashboard/Data Pages
**Key prompt additions:**
```
- Use proper component hierarchy: PageSection > Stack > Grid > Card
- For tabular data, use PatternFly Table component (see data-display/table.md)
- For charts, follow charts/README.md import requirements (/victory path)
```

### Forms
**Key prompt additions:**
```
- Follow form structure: PageSection > Form > FormGroup > ActionGroup
- Use ActionGroup component for button spacing (see styling-standards.md)
```

### Navigation/Layout
**Key prompt additions:**
```
- Use existing AppLayout structure in src/app/AppLayout/
- Follow routing patterns in src/app/routes.tsx
- Reference layout/README.md for proper component usage
```

### Charts Integration
**Key prompt additions:**
```
- CRITICAL: Import from @patternfly/react-charts/victory (see charts/README.md)
- Follow chart color guidance in charts/README.md
```

### Chatbot Integration
**Key prompt additions:**
```
- Follow dynamic import patterns from chatbot/README.md
- Reference official PatternFly chatbot demos (links in chatbot/README.md)
```

## Error Prevention Strategies

### Component Existence
**Prompt addition:**
```
"Before using any component, verify it exists by checking:
- Core components: @patternfly/react-core documentation
- Tables: @patternfly/react-table documentation  
- Charts: @patternfly/react-charts documentation
See troubleshooting/common-issues.md for common non-existent components to avoid."
```

### Styling Approach
**Prompt addition:**
```
"Follow the component-first approach from styling-standards.md:
1. Use proper component composition first
2. Use component props second  
3. Use utility classes only as last resort
Do NOT use CSS modules syntax (className={styles.*}) - this project doesn't support them."
```

### Import Paths
**Prompt addition:**
```
"Use correct import paths as documented in:
- Charts: charts/README.md (must include /victory)
- Chatbot: chatbot/README.md (dynamic imports)
- Core: standard @patternfly/react-core imports"
```

## Deployment Prompting

**When requesting deployment guidance:**
```
"After creating the prototype, provide deployment instructions following deployment-guide.md. 
Include build command and choose appropriate service (Surge for quick sharing, Vercel for professional demos)."
```

## Complete Example Prompt

```
Create a user management page using PatternFly v6 with these requirements:

Component Structure:
- Follow component hierarchy from styling-standards.md: PageSection > Stack > Toolbar + Table
- Use Table component with proper props (borders, gridBreakPoint) - see data-display/table.md
- Use ActionGroup for buttons (provides spacing automatically)

Technical Requirements:
- Verify all components exist in PatternFly packages before using
- Follow accessibility guidelines from guidelines/README.md
- Handle loading/error/empty states as shown in troubleshooting/common-issues.md

Project Integration:
- Follow existing routing patterns in src/app/routes.tsx
- Integrate with existing AppLayout structure
- Match patterns from existing pages in src/app/

References:
- Component patterns: styling-standards.md
- Table specifics: data-display/table.md  
- Accessibility: guidelines/README.md
- Error handling: troubleshooting/common-issues.md
```

## Quick Reference for Prompts

- **Component composition patterns**: [styling-standards.md](./styling-standards.md)
- **Table usage**: [data-display/table.md](../components/data-display/table.md)
- **Chart requirements**: [charts/README.md](../charts/README.md)
- **Chatbot implementation**: [chatbot/README.md](../chatbot/README.md)
- **Common errors to avoid**: [common-issues.md](../troubleshooting/common-issues.md)
- **Deployment options**: [deployment-guide.md](./deployment-guide.md)

## Best Practices Summary

1. **Reference documentation** - Include links to relevant .md files in your prompts
2. **Be specific about structure** - Mention component hierarchy requirements
3. **Prevent common errors** - Reference troubleshooting guide proactively  
4. **Verify existence** - Ask AI to confirm components exist before using
5. **Include context** - Reference existing project files when applicable

The key is combining specific prompting with references to the detailed guidance already documented in this project's other files. 