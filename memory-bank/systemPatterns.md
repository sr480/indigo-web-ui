# System Patterns: Indigo Web UI

## System Architecture

The Indigo Web UI follows a client-side single-page application (SPA) architecture that communicates with the indigosky server via a WebSocket connection. The architecture is designed to provide real-time updates and responsive control of astrophotography equipment.

### High-Level Architecture

```
┌─────────────────────────────────────────┐
│                                         │
│               Web Browser               │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │         Indigo Web UI           │    │
│  │                                 │    │
│  │  ┌─────────┐     ┌─────────┐   │    │
│  │  │   UI    │     │  State  │   │    │
│  │  │ Components    │ Management   │    │
│  │  └─────────┘     └─────────┘   │    │
│  │                                 │    │
│  │  ┌─────────────────────────┐   │    │
│  │  │    WebSocket Client     │   │    │
│  │  └─────────────────────────┘   │    │
│  │                                 │    │
│  └─────────────────────────────────┘    │
│                    ▲                    │
└────────────────────┼────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────┐
│                                         │
│           indigosky Server              │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │      Device Management          │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│  │ Mount   │ │ Camera  │ │ Focuser │    │
│  │ Drivers │ │ Drivers │ │ Drivers │    │
│  └─────────┘ └─────────┘ └─────────┘    │
│                                         │
└─────────────────────────────────────────┘
```

### Client-Server Communication

The UI communicates with the indigosky server through a WebSocket connection, which allows for:

1. **Bidirectional Communication**: The server can push updates to the client without polling
2. **Real-time Updates**: Equipment status changes are immediately reflected in the UI
3. **Efficient Protocol**: Minimal overhead for frequent status updates
4. **Connection Resilience**: Automatic reconnection handling for network interruptions

## Key Technical Decisions

### Frontend Framework: React with TypeScript

React was chosen for its:
- Component-based architecture that maps well to equipment control panels
- Virtual DOM for efficient UI updates when equipment status changes
- Large ecosystem of libraries and tools
- Strong community support

TypeScript adds:
- Type safety for complex equipment parameters and configurations
- Better developer experience with autocomplete and compile-time error checking
- Improved maintainability for a complex application
- Self-documenting code through interfaces and type definitions

### UI Component Library: Gravity UI

Gravity UI was selected because it provides:
- A comprehensive set of UI components that match the application's needs
- Consistent design language across the application
- Accessibility compliance out of the box
- Responsive components that work well on various device sizes
- Theming capabilities for light/dark mode and customization

### State Management: Zustand

Zustand was chosen over alternatives like Redux for:
- Simplicity and minimal boilerplate
- Easy integration with React hooks
- Efficient updates for real-time data
- Built-in middleware for side effects
- Good TypeScript support
- Ability to create multiple stores for different concerns

## Design Patterns

### Container/Presentational Pattern

The UI components are organized using the container/presentational pattern:
- **Container Components**: Handle state management, data fetching, and business logic
- **Presentational Components**: Focus on rendering UI elements based on props
- This separation allows for better testing, reusability, and maintenance

### Command Pattern

Equipment control operations follow the command pattern:
- Commands are serialized and sent to the server
- Each command has a unique identifier for tracking
- Commands can be queued, canceled, or prioritized
- Command history is maintained for undo/redo functionality

### Observer Pattern

The application uses the observer pattern for real-time updates:
- UI components subscribe to relevant state changes
- The WebSocket connection observes server-side events
- State updates trigger re-renders of affected components only

### Facade Pattern

A facade layer abstracts the complexity of the WebSocket communication:
- Provides a simple API for equipment control
- Handles connection management, reconnection, and error handling
- Translates between UI-friendly data structures and server protocol

## Component Relationships

### Core Component Structure

```
┌─────────────────────────────────────────────┐
│                  App                        │
│                                             │
│  ┌─────────────┐        ┌──────────────┐    │
│  │ Navigation  │        │ Notification │    │
│  │             │        │ System       │    │
│  └─────────────┘        └──────────────┘    │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │             Dashboard               │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ┌──────────┐ ┌──────────┐ ┌────────────┐   │
│  │  Mount   │ │  Camera  │ │  Focuser   │   │
│  │  Panel   │ │  Panel   │ │  Panel     │   │
│  └──────────┘ └──────────┘ └────────────┘   │
│                                             │
│  ┌──────────────────┐ ┌─────────────────┐   │
│  │ Sequence Editor  │ │ Image Viewer    │   │
│  │                  │ │                 │   │
│  └──────────────────┘ └─────────────────┘   │
│                                             │
└─────────────────────────────────────────────┘
```

### State Management Structure

```
┌─────────────────────────────────────────────┐
│                Global State                 │
│                                             │
│  ┌─────────────┐        ┌──────────────┐    │
│  │ Connection  │        │ Notification │    │
│  │ State       │        │ State        │    │
│  └─────────────┘        └──────────────┘    │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │         Equipment State              │    │
│  │                                     │    │
│  │  ┌──────────┐ ┌──────────┐ ┌─────┐  │    │
│  │  │  Mount   │ │  Camera  │ │ ... │  │    │
│  │  │  State   │ │  State   │ │     │  │    │
│  │  └──────────┘ └──────────┘ └─────┘  │    │
│  └─────────────────────────────────────┘    │
│                                             │
│  ┌─────────────────┐  ┌─────────────────┐   │
│  │ Workflow State  │  │ User Preferences│   │
│  │                 │  │                 │   │
│  └─────────────────┘  └─────────────────┘   │
│                                             │
└─────────────────────────────────────────────┘
```

## Critical Implementation Paths

### Connection Establishment

1. Application initialization
2. WebSocket connection attempt
3. Authentication with server
4. Equipment discovery
5. Initial state synchronization
6. UI rendering based on available equipment

### Equipment Control Flow

1. User interacts with UI control
2. UI component updates local state
3. Command is created and dispatched
4. Command is serialized and sent via WebSocket
5. Server processes command and sends acknowledgment
6. Server sends equipment state updates
7. UI updates to reflect new equipment state

### Imaging Sequence Execution

1. User configures imaging sequence
2. Sequence is validated and saved
3. Execution is initiated
4. Individual commands are dispatched to equipment
5. Progress is monitored and displayed
6. Images are downloaded and displayed
7. Sequence completion or error handling

### Error Handling Path

1. Error occurs (connection loss, equipment failure, etc.)
2. Error is detected and categorized
3. Recovery attempt is made if possible
4. User is notified with appropriate context
5. UI updates to reflect error state
6. Guidance is provided for resolution

These critical paths are designed to be resilient, with appropriate error handling, retry logic, and user feedback at each step.
