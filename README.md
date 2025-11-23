# Xhare Frontend

This is the frontend application for the Xhare decentralized file sharing platform, built with React and Vite.

## Description

The frontend provides a user interface for interacting with the Xhare platform, including:

- Wallet authentication and connection
- File upload and download
- Access control management
- Encryption/decryption operations
- Voice command integration
- Responsive UI with TailwindCSS

## Technology Stack

- **React** - JavaScript library for building user interfaces
- **Vite** - Next generation frontend tooling
- **TypeScript** - Strongly typed programming language
- **TailwindCSS** - Utility-first CSS framework
- **@mysten/dapp-kit** - Sui dApp development kit


## Project setup

```bash
$ pnpm install
```

## Development

```bash
# Start development server
$ pnpm run dev

# Build for production
$ pnpm run build

# Preview production build
$ pnpm run preview
```

## Environment Variables

Create a `.env` file in the frontend directory:

```bash
VITE_BACKEND_URL=http://localhost:3000
VITE_SUI_NETWORK=testnet
```

## Core Features

### Authentication
- Wallet connection via Sui dApp Kit
- Test mode for development
- OAuth login flows

### File Management
- Drag and drop file uploads
- File listing with metadata
- Download files
- Encrypted file handling

### Access Control
- Grant/revoke file access
- Allowlist management
- QR code sharing



### UI Components
- Dashboard layout
- File upload component
- Access control interface
- Responsive design

## License

This project is licensed under the MIT License.
