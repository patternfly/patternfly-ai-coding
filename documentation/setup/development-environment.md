# Development Environment

This guide covers the configuration of development tools and environment settings for optimal PatternFly React development.

## Introduction

A properly configured development environment enhances productivity and ensures consistent code quality when working with PatternFly React applications. This guide covers IDE setup, debugging tools, and development workflow optimization.

## Related Files

- [**Setup Guide**](./README.md) - Initial project setup
- [**Quick Start**](./quick-start.md) - Project initialization steps
- [**Styling Standards**](../guidelines/styling-standards.md) - CSS and styling configuration
- [**Performance Optimization**](../troubleshooting/performance.md) - Development performance tips

## Development Server Configuration

### Default Configuration
- **Port**: `9000` (default for PatternFly React Seed)
- **Hot Reload**: Enabled by default
- **Source Maps**: Available for debugging
- **Proxy Settings**: Configurable for API integration

### Server Management
```bash
# Start development server
npm run start:dev

# Start in background (recommended for AI development)
npm run start:dev &

# Stop server (if running in foreground)
Ctrl+C
```

### Environment Variables
Create a `.env` file in the project root for environment-specific settings:
```env
# Development server port
PORT=9000

# API endpoint configuration
REACT_APP_API_URL=http://localhost:3001

# Enable/disable specific features
REACT_APP_DEBUG_MODE=true
```

## IDE and Editor Configuration

### Recommended Extensions (VS Code)
- **ES7+ React/Redux/React-Native snippets**: React development shortcuts
- **Auto Rename Tag**: Automatic HTML/JSX tag renaming
- **Bracket Pair Colorizer**: Visual bracket matching
- **GitLens**: Enhanced Git integration
- **Prettier**: Code formatting
- **ESLint**: Code linting

### TypeScript Configuration
If using TypeScript with PatternFly:
```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"]
}
```

## Debugging Configuration

### Browser DevTools Setup
1. **React Developer Tools**: Install browser extension for React debugging
2. **PatternFly DevTools**: Use browser inspector to examine PatternFly classes
3. **Network Tab**: Monitor API calls and resource loading
4. **Console**: Check for PatternFly-specific warnings or errors

### VS Code Debugging
Create `.vscode/launch.json` for debugging:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Launch Chrome",
      "request": "launch",
      "type": "pwa-chrome",
      "url": "http://localhost:9000",
      "webRoot": "${workspaceFolder}/src",
      "breakOnLoad": true,
      "sourceMapPathOverrides": {
        "webpack:///src/*": "${webRoot}/*"
      }
    }
  ]
}
```

## Build and Testing Environment

### Build Scripts
```bash
# Development build
npm run build:dev

# Production build
npm run build

# Analyze bundle size
npm run analyze
```

### Testing Configuration
```bash
# Run tests
npm test

# Run tests with coverage
npm run test:coverage

# Run tests in watch mode
npm run test:watch
```

## Package Management

### Dependency Management
- **Core Dependencies**: PatternFly React components
- **Peer Dependencies**: React, React-DOM
- **Dev Dependencies**: Build tools, testing utilities

### Version Compatibility
Ensure compatible versions between:
- React and PatternFly React
- PatternFly Core CSS and PatternFly React
- Node.js and npm versions

### Update Strategy
```bash
# Check for outdated packages
npm outdated

# Update PatternFly packages
npm update @patternfly/react-core @patternfly/react-table

# Verify compatibility after updates
npm test
```

## Performance Optimization

### Development Performance
- **Code Splitting**: Implement lazy loading for large components
- **Bundle Analysis**: Regular bundle size monitoring
- **Memory Management**: Monitor for memory leaks during development

### Hot Module Replacement (HMR)
- Enabled by default in PatternFly React Seed
- Preserves component state during development
- Faster development iteration cycles

## Environment-Specific Configuration

### Development Environment
- Source maps enabled
- Detailed error messages
- Hot reloading active
- Debug mode available

### Production Environment
- Minified bundles
- Optimized assets
- Error boundaries
- Performance monitoring

## Workflow Integration

### Git Hooks
Set up pre-commit hooks for code quality:
```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "src/**/*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

### Continuous Integration
Configure CI/CD for:
- Automated testing
- Build verification
- Dependency security scanning
- Performance regression testing

## Troubleshooting Development Environment

### Common Issues
- **Port conflicts**: Change port in package.json or environment variables
- **Memory issues**: Increase Node.js memory limit
- **Slow builds**: Optimize webpack configuration
- **Hot reload failures**: Clear cache and restart development server

### Performance Monitoring
- Monitor build times
- Track bundle size changes
- Profile component rendering
- Analyze network requests

## Best Practices

1. **Keep dependencies updated** but test thoroughly
2. **Use environment variables** for configuration
3. **Enable source maps** for debugging
4. **Configure linting and formatting** for consistency
5. **Set up proper debugging tools** for efficient development
6. **Monitor performance** during development
7. **Use version control** for environment configuration files