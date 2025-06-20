# Active Context: Indigo Web UI

## Current Work Focus

The project is currently in the initial setup and planning phase. We are establishing the foundation for the Indigo Web UI, which will serve as the web-based interface for controlling astrophotography equipment through the indigosky server.

### Primary Focus Areas

1. **Project Structure Setup**: Establishing the core project structure, including directory organization, configuration files, and build processes.

2. **Technology Stack Implementation**: Setting up the React/TypeScript environment with Vite, configuring Zustand for state management, and integrating the Gravity UI component library.

3. **Core Architecture Design**: Defining the system architecture, component structure, and communication patterns between the UI and the indigosky server.

4. **Connection Layer Development**: Building the WebSocket communication layer that will handle real-time data exchange with the indigosky server.

5. **Basic UI Framework**: Creating the shell of the application with navigation, layout components, and theming support.

## Recent Changes

As this is the initial phase of the project, we are establishing the foundation rather than making changes to existing code. Key recent activities include:

1. **Project Initialization**: Created the basic project structure using Vite with React and TypeScript templates.

2. **Documentation Setup**: Established the memory bank structure to document project context, architecture, and progress.

3. **Dependency Selection**: Evaluated and selected key dependencies including Zustand for state management and Gravity UI for the component library.

4. **Architecture Planning**: Defined the high-level architecture for the application, including the WebSocket communication layer and component organization.

## Next Steps

The immediate next steps for the project are:

1. **Setup Development Environment**:
   - Complete the project configuration (ESLint, Prettier, TypeScript)
   - Configure testing tools (Vitest, Cypress)
   - Set up Storybook for component development

2. **Implement Core Infrastructure**:
   - Create the WebSocket connection manager
   - Implement the basic state management stores
   - Develop the authentication flow

3. **Build Basic UI Framework**:
   - Create the application shell with navigation
   - Implement the theme system (light/dark mode)
   - Develop the layout components

4. **Develop Equipment Connection UI**:
   - Create the server connection interface
   - Implement equipment discovery and display
   - Build the basic dashboard for connected equipment

5. **Create First Equipment Control Panel**:
   - Implement the mount control panel as the first specialized interface
   - Develop the command pattern for equipment control
   - Create real-time status display components

## Active Decisions and Considerations

### Architecture Decisions

1. **WebSocket vs. REST**: We've chosen WebSocket as the primary communication protocol for its real-time capabilities, which are essential for equipment control and monitoring. REST endpoints may be used for non-real-time operations.

2. **State Management Approach**: Zustand was selected over Redux or Context API for its simplicity and performance. We're organizing state by domain (connection, equipment types, UI state) rather than in a single store.

3. **Component Organization**: We're following the container/presentational pattern to separate logic from UI rendering, making components more testable and reusable.

### Open Questions

1. **Offline Capability**: Should the application support offline planning and sequence creation? This would require additional state persistence and synchronization logic.

2. **Image Processing**: To what extent should the UI handle image processing vs. delegating to the server? This affects the client-side performance requirements and library dependencies.

3. **Mobile Experience**: How comprehensive should the mobile experience be? Full feature parity or a subset focused on monitoring and basic control?

4. **Multi-language Support**: Should we implement internationalization from the start, or add it later when the core functionality is stable?

### Technical Debt Considerations

1. **Type Definitions**: We need comprehensive TypeScript interfaces for all equipment parameters and server messages. This is essential but time-consuming work.

2. **Test Coverage**: Establishing good test patterns early will save time later, but we need to balance test writing with feature development in the early stages.

3. **Documentation**: Maintaining up-to-date documentation is crucial, especially for the communication protocol and component APIs.

## Important Patterns and Preferences

### Coding Standards

1. **TypeScript Usage**: 
   - Strict type checking enabled
   - Interfaces preferred over types for object definitions
   - Generics used for reusable components and utilities
   - Explicit return types on all functions

2. **Component Structure**:
   - Functional components with hooks
   - Props interfaces defined for all components
   - Default props specified where appropriate
   - Component files organized by feature, not type

3. **State Management**:
   - Zustand stores organized by domain
   - Selectors used to access state efficiently
   - Actions for state modifications
   - Side effects isolated in middleware or custom hooks

### UI/UX Preferences

1. **Responsive Design**:
   - Mobile-first approach
   - Breakpoints at standard device sizes
   - Flexible layouts that adapt to available space

2. **Accessibility**:
   - WCAG 2.1 AA compliance as a minimum target
   - Keyboard navigation support
   - Screen reader compatibility
   - Sufficient color contrast

3. **Performance**:
   - Code splitting for route-based components
   - Memoization for expensive calculations
   - Virtualization for long lists
   - Optimized re-renders with React.memo and useMemo

## Learnings and Project Insights

As we're in the early stages, we're establishing foundational knowledge:

1. **Domain Complexity**: Astrophotography equipment control involves complex parameters and workflows. We need to balance exposing this complexity with creating an intuitive interface.

2. **Real-time Challenges**: Maintaining a responsive UI while handling frequent updates from equipment will require careful performance optimization.

3. **User Diversity**: Our target users range from beginners to experienced astrophotographers, requiring an interface that scales in complexity based on user expertise.

4. **Environmental Factors**: The application will often be used in dark environments (nighttime astronomy), making dark mode and brightness control essential features.

5. **Connection Reliability**: Users may operate in locations with unreliable internet connections, requiring robust reconnection handling and offline capabilities where possible.

These insights will guide our development approach as we move forward with implementing the core functionality of the Indigo Web UI.
