# Development Guidelines for Stories Teller App

This document provides guidelines and information for developers working on the Stories Teller App project.

## Build/Configuration Instructions

### Prerequisites
- Node.js (latest LTS version recommended)
- npm or yarn
- Expo CLI (`npm install -g expo-cli`)

### Setup
1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```

### Running the App
- **Development Mode**:
  ```bash
   npx expo start
   ```
   This will start the Expo development server and provide options to run the app on:
   - Android emulator
   - iOS simulator
   - Web browser
   - Physical device using Expo Go app

- **Platform-Specific Commands**:
  ```bash
  # Android
  npm run android

  # iOS
  npm run ios

  # Web
  npm run web
  ```

### Project Structure
- `app/` - Main application code using Expo Router (file-based routing)
  - `(tabs)/` - Tab-based navigation screens
- `assets/` - Static assets like images, fonts, and icons
- `constants/` - Constant values and configurations
- `interfaces/` - TypeScript interface definitions
- `types/` - TypeScript type definitions

### Configuration Files
- `app.json` - Expo configuration
- `babel.config.js` - Babel configuration for transpilation
- `tailwind.config.js` - TailwindCSS/NativeWind configuration
- `tsconfig.json` - TypeScript configuration
- `eslint.config.js` - ESLint configuration

## Testing Information

### Testing Framework
The project uses Jest as the testing framework with React Native Testing Library for component testing.

### Running Tests
```bash
npm test
```

This command will run all tests and generate a coverage report.

### Test Structure
- Tests are located in the `__tests__` directory
- Test files should follow the naming convention: `*.test.ts` or `*.test.tsx`
- Component tests should be placed in files named after the component they test

### Writing Tests

#### Utility Function Tests
```typescript
// __tests__/utils.test.ts
import { myUtilityFunction } from '../utils';

describe('myUtilityFunction', () => {
  it('should do something specific', () => {
    expect(myUtilityFunction(input)).toBe(expectedOutput);
  });
});
```

#### Component Tests
```typescript
// __tests__/MyComponent.test.tsx
import React from 'react';
import { render, fireEvent } from '@testing-library/react-native';
import MyComponent from '../components/MyComponent';

describe('MyComponent', () => {
  it('renders correctly', () => {
    const { getByText } = render(<MyComponent />);
    expect(getByText('Expected Text')).toBeTruthy();
  });

  it('handles user interaction', () => {
    const onPressMock = jest.fn();
    const { getByText } = render(<MyComponent onPress={onPressMock} />);
    fireEvent.press(getByText('Press Me'));
    expect(onPressMock).toHaveBeenCalled();
  });
});
```

### Test Coverage
The Jest configuration is set up to collect coverage information. After running tests, a coverage report will be generated in the `coverage/` directory.

## Additional Development Information

### Code Style
- The project uses ESLint with the Expo configuration for code linting
- Run linting checks with:
  ```bash
  npm run lint
  ```

### TypeScript
- The project uses TypeScript with strict type checking enabled
- Path aliases are configured with the `@/` prefix:
  ```typescript
  // Instead of
  import { something } from '../../constants/values';
  
  // Use
  import { something } from '@/constants/values';
  ```

### Styling
- The project uses NativeWind (TailwindCSS for React Native) for styling
- Custom colors are defined in `tailwind.config.js`:
  - `primary`: #030014
  - `secondary`: #151312
  - `light`: Various light shades
  - `dark`: Various dark shades
  - `accent`: #AB8BFF

### Navigation
- The project uses Expo Router for navigation
- File-based routing is implemented in the `app/` directory
- Tab navigation is configured in `app/(tabs)/_layout.tsx`

### Assets
- Images should be placed in `assets/images/`
- Icons should be placed in `assets/icons/`
- Fonts should be placed in `assets/fonts/`

### Best Practices
1. Follow the existing code structure and naming conventions
2. Write tests for new functionality
3. Use TypeScript types and interfaces for better code quality
4. Use NativeWind classes for styling instead of StyleSheet
5. Keep components small and focused on a single responsibility
6. Use constants for values that might change or are used in multiple places