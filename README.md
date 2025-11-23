# Xhare - Decentralized File Sharing Platform

Xhare is a decentralized file sharing platform built on the Sui blockchain that enables secure file storage, sharing, and access control using Walrus storage and Mysten SEAL encryption.

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [Environment Configuration](#environment-configuration)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Testing](#testing)
- [Deployment](#deployment)
- [Smart Contracts](#smart-contracts)

## Architecture Overview

Xhare consists of three main components:

1. **Frontend** - React/Vite application for user interaction
2. **Backend** - NestJS API server handling file operations, authentication, and blockchain integration
3. **Smart Contracts** - Sui Move contracts for access control and registry management

The platform integrates with:
- **Walrus** - Decentralized storage network for file persistence
- **Mysten SEAL** - Identity-based encryption for file security
- **Sui Blockchain** - For access control and smart contract execution
- **zkLogin** - For OAuth-based authentication

## Features

- 🔐 **Secure Authentication**: Wallet-based and OAuth authentication (Google, GitHub, etc.)
- 📁 **File Upload/Download**: Direct file operations with Walrus storage
- 🔒 **File Encryption**: End-to-end encryption using Mysten SEAL
- 🔄 **Access Control**: Granular file access permissions with smart contracts
- 📱 **Wallet Integration**: Seamless Sui wallet connection
- 🌐 **Decentralized Storage**: Files stored on Walrus network

- 📱 **Responsive UI**: Modern React frontend with TailwindCSS

## Technology Stack

### Backend
- **NestJS** - Progressive Node.js framework
- **TypeScript** - Strongly typed programming language
- **@mysten/sui** - Sui blockchain SDK
- **@mysten/walrus** - Walrus storage integration
- **@mysten/seal** - Mysten SEAL encryption library
- **@mysten/zklogin** - Zero-knowledge login implementation

### Frontend
- **React** - JavaScript library for building user interfaces
- **Vite** - Next generation frontend tooling
- **TypeScript** - Strongly typed programming language
- **TailwindCSS** - Utility-first CSS framework
- **@mysten/dapp-kit** - Sui dApp development kit


### Smart Contracts
- **Sui Move** - Smart contract language for Sui blockchain

## Prerequisites

- Node.js >= 18.x
- pnpm (recommended) or npm/yarn
- Sui CLI tools
- Walrus testnet access
- Sui testnet wallet with funded tokens

## Project Structure

```
xhare/
├── backend-main/          # NestJS backend server
│   ├── src/
│   │   ├── auth/          # Authentication services
│   │   ├── file/          # File handling controllers/services
│   │   ├── storage/       # Walrus storage integration
│   │   ├── sui/           # Sui blockchain integration
│   │   └── access-control/ # Access control services
│   ├── data/              # Test data
│   └── ...
├── frontend/              # React frontend application
│   ├── src/
│   │   ├── components/    # UI components
│   │   ├── contexts/      # React contexts
│   │   ├── services/      # API service clients
│   │   └── hooks/         # Custom React hooks
│   └── ...
└── suiCircle/             # Sui Move smart contracts
    ├── sources/           # Move source files
    └── Move.toml          # Move package configuration
```

## Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend-main
   ```

2. Install dependencies:
   ```bash
   pnpm install
   # or
   npm install
   ```

3. Configure environment variables (see [Environment Configuration](#environment-configuration))

4. Start the development server:
   ```bash
   pnpm run start:dev
   # or
   npm run start:dev
   ```

## Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   pnpm install
   # or
   npm install
   ```

3. Start the development server:
   ```bash
   pnpm run dev
   # or
   npm run dev
   ```

## Environment Configuration

### Backend Environment Variables

Create a `.env` file in the `backend-main` directory:

```bash
# Sui Network Configuration
SUI_NETWORK=testnet
SUI_RPC_URL=https://fullnode.testnet.sui.io:443

# Walrus Configuration
WALRUS_NETWORK=testnet
WALRUS_PRIVATE_KEY=suiprivkey1q... # Your funded Walrus private key
WALRUS_STORAGE_EPOCHS=5

# Upload Relay Configuration
WALRUS_UPLOAD_RELAY_URL=https://upload-relay.testnet.walrus.space
WALRUS_USE_UPLOAD_RELAY=true
WALRUS_MAX_TIP=1000

# Smart Contract Configuration
SUICIRCLE_PACKAGE_ID=0x... # Your deployed package ID
SUICIRCLE_REGISTRY_ID=0x... # Your deployed registry ID

# Mysten SEAL Configuration
SUI_PACKAGE_ID=0x... # Your deployed SEAL package ID

# zkLogin Configuration
ZKLOGIN_SALT=your-unique-salt-change-in-production
JWT_SECRET=your-jwt-secret-change-in-production

# OAuth Configuration (for zkLogin)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GOOGLE_REDIRECT_URI=http://localhost:3000/auth/google/callback

GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret
GITHUB_REDIRECT_URI=http://localhost:5174/

# Development
NODE_ENV=development
PORT=3000
```

### Frontend Environment Variables

The frontend uses Vite's environment variable system. Create a `.env` file in the `frontend` directory:

```bash
VITE_BACKEND_URL=http://localhost:3000
VITE_SUI_NETWORK=testnet
```

## Running the Application

### Development Mode

1. Start the backend server:
   ```bash
   cd backend-main
   pnpm run start:dev
   ```

2. In a separate terminal, start the frontend:
   ```bash
   cd frontend
   pnpm run dev
   ```

3. Access the application at `http://localhost:5173`

### Production Build

1. Build the frontend:
   ```bash
   cd frontend
   pnpm run build
   ```

2. Build the backend:
   ```bash
   cd backend-main
   pnpm run build
   ```

3. Start the production server:
   ```bash
   pnpm run start:prod
   ```

## API Endpoints

### Authentication
- `GET /auth/login/:provider` - Initiate OAuth login
- `GET /auth/:provider/callback` - OAuth callback handler
- `POST /auth/wallet` - Authenticate with wallet address
- `GET /auth/verify` - Verify authentication token
- `GET /auth/profile` - Get user profile

### File Operations
- `POST /file/upload` - Upload file with authentication
- `POST /file/upload-wallet` - Upload file with wallet header
- `POST /file/upload-metadata` - Upload file metadata
- `GET /file/:cid/info` - Get file metadata
- `GET /file/:cid/download` - Download file
- `POST /file/:cid/grant-access` - Grant file access
- `POST /file/:cid/revoke-access` - Revoke file access
- `GET /file` - List user files

### Encryption
- `POST /file/upload-encrypted` - Upload encrypted file
- `POST /file/:cid/download-encrypted` - Download and decrypt file
- `GET /file/seal-status` - Get SEAL encryption status

### Walrus
- `GET /file/walrus-status` - Get Walrus configuration status
- `GET /file/wallet-info` - Get wallet information

## Testing

### Backend Tests

Run unit tests:
```bash
cd backend-main
pnpm run test
```

Run end-to-end tests:
```bash
pnpm run test:e2e
```

### Frontend Tests

Run tests:
```bash
cd frontend
pnpm run test
```

## Deployment

### Backend Deployment

1. Ensure all environment variables are set for production
2. Build the application:
   ```bash
   pnpm run build
   ```
3. Start the production server:
   ```bash
   pnpm run start:prod
   ```

### Frontend Deployment

1. Build the production bundle:
   ```bash
   pnpm run build
   ```
2. Deploy the contents of the `dist` folder to your preferred hosting service

### Environment Considerations

For production deployment:
- Set `NODE_ENV=production`
- Use secure, production-ready secrets
- Configure proper CORS origins
- Set up SSL/HTTPS
- Use a reverse proxy (nginx, etc.) for production deployments

## Smart Contracts

The smart contracts are located in the `suiCircle` directory and include:

1. **Registry** - File registry and access control
2. **Access Control** - Granular permission management

### Deployment

1. Navigate to the smart contracts directory:
   ```bash
   cd suiCircle
   ```

2. Build the contracts:
   ```bash
   sui move build
   ```

3. Deploy the contracts:
   ```bash
   sui client publish --gas-budget 1000000000
   ```

4. Update the package ID and registry ID in your backend `.env` file

## Troubleshooting

### Common Issues

1. **Walrus Upload Issues**:
   - Ensure `WALRUS_PRIVATE_KEY` is correctly set and funded
   - Check that `SUI_RPC_URL` points to the correct network
   - Verify the backend restarts after environment changes

2. **Authentication Problems**:
   - Check OAuth configuration in environment variables
   - Ensure redirect URIs match your deployment
   - Verify JWT secret is properly set

3. **Encryption Errors**:
   - Confirm `SUI_PACKAGE_ID` is correctly set
   - Check that SEAL service initializes properly
   - Ensure key servers are accessible

### Logs and Monitoring

- Backend logs are available in the terminal where the server is running
- Frontend logs can be viewed in the browser console
- Check Walrus Scan for transaction verification

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, please open an issue on the GitHub repository or contact the development team.