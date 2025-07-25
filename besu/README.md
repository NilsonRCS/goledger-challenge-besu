# Hyperledger Besu Private Network with Go & Node.js APIs

A complete blockchain development environment featuring Hyperledger Besu with QBFT consensus, PostgreSQL integration, and dual API implementations.

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Go REST API   │    │  Hyperledger     │    │   PostgreSQL    │
│   (Port 8080)   │────│     Besu         │────│    Database     │
│                 │    │  Smart Contract  │    │  (Port 5432)    │
└─────────────────┘    │   4-Node QBFT    │    └─────────────────┘
                       │ (Ports 8545-8548)│             │
┌─────────────────┐    │                  │             │
│ Node.js API +   │────│                  │─────────────┘
│ Swagger UI      │    │                  │
│  (Port 3001)    │    └──────────────────┘
└─────────────────┘
```

## ✨ Features

- **Hyperledger Besu**: 4-node private network with QBFT consensus
- **Dual APIs**: Go and Node.js implementations
- **Smart Contracts**: SimpleStorage contract deployment and interaction
- **Database Integration**: PostgreSQL for data persistence
- **Documentation**: Complete Swagger UI documentation
- **Docker Support**: Containerized infrastructure

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Go 1.23+
- Node.js 16+ (for Node.js API)
- PostgreSQL client (optional)

### 1. Start Infrastructure
```bash
# Start Besu network and database
./startDev.sh

# Verify network is running
docker ps | grep besu
```

### 2. Deploy Smart Contract
```bash
# Quick deployment
node scripts/deploy-web3.js
```

### 3. Start APIs

**Go API:**
```bash
cd go-api
go mod tidy
go run main.go
# Access: http://localhost:8080
```

**Node.js API:**
```bash
cd api
npm install
npm start
# Access: http://localhost:3001
# Swagger: http://localhost:3001/api-docs
```

## 📋 API Endpoints

### Core Operations (Both APIs)

| Endpoint | Method | Description |
|----------|---------|-------------|
| `/api/set` | POST | Set new value in smart contract |
| `/api/get` | GET | Get current value from blockchain |
| `/api/sync` | POST | Sync blockchain value to database |
| `/api/check` | GET | Compare database vs blockchain values |

### Additional Endpoints
- `GET /api/history` - Value change history
- `GET /api/status` - System status
- `GET /api/health` - Health check

## 🔧 Configuration

### Environment Variables

**Go API (.env):**
```env
BESU_RPC_URL=http://localhost:8545
CONTRACT_ADDRESS=0x...
DB_HOST=localhost
DB_PORT=5432
API_PORT=8080
```

**Node.js API (.env):**
```env
PORT=3001
BESU_RPC_URL=http://localhost:8545
DATABASE_URL=postgresql://user:pass@localhost:5432/besu_contracts
```

## 🧪 Testing

### Test Go API Endpoints
```bash
# GET value
curl http://localhost:8080/api/get

# SET value
curl -X POST http://localhost:8080/api/set \
  -H "Content-Type: application/json" \
  -d '{"value": 42}'

# SYNC to database
curl -X POST http://localhost:8080/api/sync

# CHECK synchronization
curl http://localhost:8080/api/check
```

### Test Node.js API
Access Swagger UI at `http://localhost:3001/api-docs` for interactive testing.

## 📁 Project Structure

```
besu/
├── config/                 # Network configuration
├── contracts/              # Smart contracts
├── docker/                 # Docker configurations
├── genesis/               # Genesis block configuration
├── node/                  # Besu node data
├── scripts/               # Deployment scripts
├── api/                   # Node.js API
│   ├── routes/           # API routes
│   ├── services/         # Business logic
│   └── config/           # Swagger configuration
└── go-api/               # Go API
    ├── internal/         # Internal packages
    │   ├── blockchain/   # Blockchain client
    │   ├── database/     # Database operations
    │   ├── handlers/     # HTTP handlers
    │   └── models/       # Data models
    └── main.go           # Application entry point
```

## 🔒 Security Features

- Private key management through environment variables
- Input validation on all endpoints
- CORS headers configured
- Error handling and logging

## 📊 Monitoring

- Health check endpoints
- System status monitoring
- Database connection status
- Blockchain connectivity status

## 🐳 Docker Commands

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f besu-node-0

# Stop services
docker-compose down
```

## 📈 Development

### Adding New Endpoints
1. Define models in `internal/models/`
2. Add database operations in `internal/database/`
3. Implement handlers in `internal/handlers/`
4. Register routes in `main.go`

### Code Style
- Clean, comment-free code
- Error handling for all operations
- Consistent naming conventions

## 🎯 Use Cases

- **Smart Contract Development**: Test and deploy contracts
- **API Development**: REST API with blockchain integration
- **Database Integration**: Persistent data storage
- **Monitoring**: System health and status tracking

## 🤝 Contributing

1. Ensure all tests pass
2. Follow Go naming conventions
3. Update documentation as needed
4. Test both APIs before committing

---

**Built with:** Hyperledger Besu + PostgreSQL + Go + Node.js + Docker
