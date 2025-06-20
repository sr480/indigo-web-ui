# Indigo Web UI

A modern web-based user interface for controlling astrophotography equipment through the indigosky server.

![License](https://img.shields.io/badge/license-MIT-blue.svg)

## Overview

Indigo Web UI is a comprehensive web application designed to provide astronomers and astrophotographers with a unified interface for controlling various astronomical equipment. It connects to the indigosky server, which handles direct communication with telescopes, cameras, mounts, focusers, and other devices.

### Key Features

- **Equipment Control**: Specialized panels for different equipment types (mounts, cameras, focusers, etc.)
- **Real-time Monitoring**: Live status updates from all connected devices
- **Imaging Workflow**: Tools for planning and executing astrophotography sessions
- **Responsive Design**: Works on desktop and mobile devices
- **Dark Mode**: Optimized for use in nighttime environments

## Screenshots

*Coming soon*

## Technologies

- **Frontend**: React 18, TypeScript 5
- **Build Tool**: Vite 4
- **State Management**: Zustand 4
- **UI Components**: Gravity UI 2
- **Communication**: WebSocket for real-time updates
- **Testing**: Vitest, Cypress

## Getting Started

### Prerequisites

- Node.js (v18+)
- npm (v9+) or yarn (v1.22+)
- indigosky server (running and accessible)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/username/indigo-web-ui.git
   cd indigo-web-ui
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to:
   ```
   http://localhost:5173
   ```

### Building for Production

```bash
npm run build
```

The built files will be in the `dist` directory, ready to be deployed to a web server.

## Usage

### Connecting to the indigosky Server

1. Launch the application
2. Enter the indigosky server address (e.g., `ws://localhost:7624`)
3. Click "Connect"

### Equipment Control

Once connected, the UI will display control panels for all detected equipment:

- **Mount Panel**: Control telescope movement, tracking, and alignment
- **Camera Panel**: Configure exposure settings and capture images
- **Focuser Panel**: Adjust focus position manually or automatically
- **Filter Wheel Panel**: Select and change filters

### Imaging Workflow

1. Connect to all required equipment
2. Use the mount control to point to your target
3. Adjust focus using the focuser panel
4. Set up an imaging sequence with the desired exposures and filters
5. Start the sequence and monitor progress

## Project Structure

```
indigo-web-ui/
├── public/            # Static assets
├── src/
│   ├── assets/        # Images, fonts, etc.
│   ├── components/    # Reusable UI components
│   ├── hooks/         # Custom React hooks
│   ├── pages/         # Page components
│   ├── services/      # API and WebSocket services
│   ├── stores/        # Zustand state stores
│   ├── types/         # TypeScript type definitions
│   ├── utils/         # Utility functions
│   ├── App.tsx        # Main application component
│   └── main.tsx       # Application entry point
├── memory-bank/       # Project documentation
├── .eslintrc.js       # ESLint configuration
├── .prettierrc        # Prettier configuration
├── tsconfig.json      # TypeScript configuration
├── vite.config.ts     # Vite configuration
└── package.json       # Project dependencies and scripts
```

## Documentation

Comprehensive project documentation is available in the `memory-bank` directory:

- `projectbrief.md` - Project overview and requirements
- `productContext.md` - Why this project exists and problems it solves
- `systemPatterns.md` - System architecture and design patterns
- `techContext.md` - Technical details and development setup
- `activeContext.md` - Current work focus and next steps
- `progress.md` - Project status and roadmap

## Roadmap

See the [progress.md](memory-bank/progress.md) file for the detailed development roadmap.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- The indigosky server team for providing the equipment control backend
- All contributors and testers who help improve this project
