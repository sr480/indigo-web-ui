# Technical Context: Indigo Web UI

## Technologies Used

### Core Technologies

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 18.x | UI library for building component-based interfaces |
| TypeScript | 5.x | Typed superset of JavaScript for improved code quality |
| Vite | 4.x | Build tool and development server |
| Zustand | 4.x | State management library |
| Gravity UI | 2.x | UI component library for consistent design |
| WebSocket API | - | Real-time communication with indigosky server |

### Supporting Libraries

| Library | Purpose |
|---------|---------|
| React Router | Client-side routing |
| date-fns | Date manipulation and formatting |
| zod | Runtime type validation |
| React Query | Data fetching and caching |
| Vitest | Unit and integration testing |
| Cypress | End-to-end testing |
| ESLint | Code quality and style enforcement |
| Prettier | Code formatting |
| Storybook | Component development and documentation |

## Development Setup

### Prerequisites

- Node.js (v18+)
- npm (v9+) or yarn (v1.22+)
- Git
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Local Development Environment

1. **Clone the repository**
   ```bash
   git clone https://github.com/username/indigo-web-ui.git
   cd indigo-web-ui
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Run tests**
   ```bash
   npm run test        # Unit tests
   npm run test:e2e    # End-to-end tests
   ```

5. **Build for production**
   ```bash
   npm run build
   ```

### Development Workflow

1. **Feature branches**: All new features are developed in dedicated branches
2. **Pull requests**: Code review is required before merging to main
3. **Continuous integration**: Automated tests run on all pull requests
4. **Semantic versioning**: Releases follow semver conventions

## Technical Constraints

### Browser Compatibility

The application targets modern browsers with good WebSocket support:
- Chrome/Edge (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)

No support for Internet Explorer is planned.

### Performance Requirements

- Initial load time: < 3 seconds on broadband connections
- Time to interactive: < 5 seconds
- UI response time: < 100ms for most interactions
- Memory usage: < 200MB in typical usage scenarios
- Efficient rendering to support frequent updates from equipment

### Network Requirements

- WebSocket connection to indigosky server
- Stable connection for real-time updates
- Bandwidth for image transfer (varies based on camera resolution)
- Reconnection handling for intermittent connections

### Security Considerations

- Authentication for server connection
- HTTPS for all communications
- Input validation for all user inputs
- Protection against common web vulnerabilities (XSS, CSRF)
- Secure storage of user preferences and credentials

## Dependencies

### External Dependencies

1. **indigosky Server**
   - Must be running and accessible
   - Version compatibility requirements
   - Provides equipment control API
   - Handles direct communication with hardware

2. **Astronomy Equipment**
   - Various telescopes, mounts, cameras, etc.
   - Connected to the indigosky server
   - Each with their own capabilities and limitations

### Internal Dependencies

1. **Component Dependencies**
   - UI components have clear dependency hierarchies
   - Shared components are maintained in a component library
   - Component props are strictly typed

2. **State Dependencies**
   - Global state is organized by domain
   - Components subscribe only to relevant state slices
   - State updates trigger minimal re-renders

## Tool Usage Patterns

### Development Tools

#### Vite

Used for:
- Fast development server with HMR
- Optimized production builds
- TypeScript integration
- Environment variable management

Configuration in `vite.config.ts`

#### TypeScript

Used for:
- Type definitions for all components and functions
- Interface definitions for data structures
- Type guards for runtime type checking
- Utility types for common patterns

Configuration in `tsconfig.json`

#### ESLint & Prettier

Used for:
- Code style enforcement
- Error prevention
- Consistent formatting

Configuration in `.eslintrc.js` and `.prettierrc`

### Testing Tools

#### Vitest

Used for:
- Unit testing of utility functions
- Component testing with React Testing Library
- Mock implementations of external dependencies

#### Cypress

Used for:
- End-to-end testing of user workflows
- Visual regression testing
- API mocking for consistent test environments

### State Management with Zustand

Zustand is used with the following patterns:
- Separate stores for different domains (connection, equipment, UI state)
- Typed selectors for accessing state
- Actions for modifying state
- Middleware for side effects and persistence
- DevTools integration for debugging

Example store structure:
```typescript
interface ConnectionStore {
  status: 'disconnected' | 'connecting' | 'connected' | 'error';
  error: string | null;
  serverUrl: string;
  connect: (url: string) => Promise<void>;
  disconnect: () => void;
}

const useConnectionStore = create<ConnectionStore>((set, get) => ({
  status: 'disconnected',
  error: null,
  serverUrl: '',
  connect: async (url) => {
    set({ status: 'connecting', serverUrl: url });
    try {
      // Connection logic
      set({ status: 'connected', error: null });
    } catch (e) {
      set({ status: 'error', error: e.message });
    }
  },
  disconnect: () => {
    // Disconnection logic
    set({ status: 'disconnected' });
  }
}));
```

### Component Development with Storybook

Storybook is used for:
- Isolated component development
- Visual testing of component states
- Documentation of component APIs
- Showcasing component variations

Each component has:
- Multiple stories showing different states
- Documentation of props and usage
- Controls for interactive testing

## Build and Deployment

### Build Process

1. TypeScript compilation
2. Asset optimization
3. Bundle creation
4. Minification and tree-shaking
5. Generation of static files

### Deployment Options

1. **Static Hosting**
   - Deploy to any static file server
   - Configure for SPA routing

2. **Docker Deployment**
   - Containerized deployment with Nginx
   - Environment variable configuration

3. **Electron Packaging**
   - Desktop application packaging
   - Native integration options

### CI/CD Pipeline

- GitHub Actions for automated builds and tests
- Deployment to staging environments for testing
- Production deployment after approval
- Version tagging and release notes generation
