# LeeWay Ecosystem - Advanced Documentation

## 🏗️ Architecture Overview

**LeeWay Ecosystem** is a comprehensive microservices platform featuring 8 distributed services orchestrated through a central Motherboard UI, with production-grade configuration and deployment automation.

### System Topology

```
┌─────────────────────────────────────────────────────────────┐
│           Agent Lee Motherboard (Port 7601)                  │
│        React 19.2.5 + Vite 6.4.2 + Tailwind CSS 4.2.4       │
│              HTTP/2 Server: Node.js + Express               │
└─────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   ┌────▼────┐          ┌────▼────┐          ┌────▼────┐
   │ Port    │          │ Port    │          │ Port    │
   │ 7602    │          │ 7603    │          │ 7604    │
   │Employment          │Learning │          │Edge RTC │
   │Center  │          │Platform │          │         │
   └────────┘          └────────┘          └────────┘
        │                     │                     │
   ┌────▼────┐          ┌────▼────┐          ┌────▼────┐
   │ Port    │          │ Port    │          │ Port    │
   │ 7605    │          │ 7606    │          │ 7607    │
   │Edge GPU │          │Edge     │          │Edge IOT │
   │         │          │DEVICE   │          │         │
   └────────┘          └────────┘          └────────┘
        │
   ┌────▼────┐
   │ Port    │
   │ 7608    │
   │Standards│
   └────────┘
```

### Service Registry (Ports 7601-7608)

| Service | Port | Status | Language | Health Check |
|---------|------|--------|----------|--------------|
| Motherboard UI | 7601 | ✅ Active | React/TypeScript | /health |
| Employment Center | 7602 | ✅ Active | Node.js | /health |
| Learning Platform | 7603 | ✅ Active | Node.js | /health |
| Edge RTC | 7604 | ✅ Active | Node.js | /health |
| Edge GPU | 7605 | ✅ Active | Python/Node | /health |
| Edge DEVICE | 7606 | ✅ Active | Node.js | /health |
| Edge IOT | 7607 | ✅ Active | Node.js | /health |
| Standards | 7608 | ✅ Active | Node.js | /health |

## 🛠️ Technology Stack

### Frontend
- **React 19.2.5** - UI framework with latest hooks and features
- **Vite 6.4.2** - Lightning-fast build tool with ES2020 target
- **Tailwind CSS 4.2.4** - Utility-first CSS framework
- **Three.js + React Three Fiber + Drei** - 3D rendering capabilities
- **TypeScript** - Static type checking

### Backend
- **Node.js v24.15.0** - Runtime environment
- **Express.js** - HTTP server framework
- **Firebase** - Real-time database and authentication
- **REST API** - Service-to-service communication

### Build & Deployment
- **Terser v5.x** - Production code minification
- **Docker** - Container orchestration
- **PM2** - Process manager
- **Git/GitHub** - Version control and CI/CD

### AI/ML & Advanced
- **Qwen 0.5B** - LLM model for Agent Lee
- **Kokoro Voice** - Voice synthesis
- **Gemini API** - Advanced AI capabilities
- **Alibaba Cloud** - Infrastructure provider
- **Hugging Face** - Model hub integration

## ✨ Key Features

### Production-Grade Configuration
- ✅ Sequential port assignment (7601-7608) preventing conflicts
- ✅ Health check endpoints on all services
- ✅ Centralized .env configuration
- ✅ Comprehensive error handling and logging

### React Production Optimization
- ✅ Terser minification applied (5.4 MB bundle)
- ✅ Dead code elimination enabled
- ✅ Source maps disabled in production
- ✅ ES2020 JavaScript target
- ✅ Process.env.NODE_ENV defined in build pipeline

### Security & Compliance
- ✅ Environment variable isolation
- ✅ GitHub PAT token integration
- ✅ NGROK tunneling support
- ✅ Role-based access control ready

### Developer Experience
- ✅ Fast rebuild cycles (Vite hot module replacement)
- ✅ Comprehensive documentation
- ✅ Multiple startup scripts for different deployment modes
- ✅ Real-time health monitoring

## 🚀 Quick Start Guide

### Prerequisites
- Node.js v24.15.0 or higher
- npm 10.0.0 or higher
- Git v2.40.0 or higher
- 4GB RAM minimum
- 10GB free disk space

### Installation

```bash
# 1. Clone repository
git clone https://github.com/4citeB4U/leeway-ecosystem.git
cd leeway-ecosystem

# 2. Install dependencies
npm install
cd agent-lee-motherboard && npm install && cd ..

# 3. Configure environment
cp .env.example .env
# Edit .env with your credentials

# 4. Verify configuration
node scripts/validate-config.js
```

### Startup Options

#### Option 1: Full Stack (All Services)
```bash
# Start all 8 services with health monitoring
npm run start:full-stack
```

#### Option 2: Development Mode
```bash
# Start with file watching and hot reload
npm run dev
```

#### Option 3: Production Mode
```bash
# Optimized build with minification
npm run build
npm start
```

### Verification

```bash
# Check all service health
curl http://localhost:7601/health
curl http://localhost:7602/health
curl http://localhost:7603/health
# ... check ports 7604-7608

# Access Motherboard UI
open http://localhost:7601

# Monitor real-time logs
tail -f logs/ecosystem.log
```

## 📋 Configuration Files

### leeway.ports.json
Defines sequential port assignments for all services:

```json
{
  "portRange": {
    "start": 7601,
    "end": 7608
  },
  "services": {
    "motherboard": 7601,
    "employment-center": 7602,
    "learning-platform": 7603,
    "edge-rtc": 7604,
    "edge-gpu": 7605,
    "edge-device": 7606,
    "edge-iot": 7607,
    "standards": 7608
  }
}
```

### leeway.services.json
Service configuration with health checks:

```json
{
  "services": [
    {
      "name": "agent-lee-motherboard",
      "port": 7601,
      "priority": 1,
      "cmd": "start",
      "healthCheck": {
        "path": "/health",
        "interval": 5000,
        "timeout": 3000
      }
    }
    // ... additional services
  ]
}
```

### .env Configuration
Runtime environment variables:

```bash
NODE_ENV=production
VITE_NODE_ENV=production
MOTHERBOARD_PORT=7601
EMPLOYMENT_CENTER_PORT=7602
# ... additional ports and credentials
```

## 🔌 API Documentation

### Health Check Endpoint
```bash
GET /health
Response: { status: 'healthy', uptime: 1234, timestamp: '2026-04-27T...' }
```

### Service Status
```bash
GET /status
Response: { 
  services: { 
    motherboard: 'healthy',
    employment-center: 'healthy',
    // ... all services
  }
}
```

### Configuration Retrieval
```bash
GET /api/config
Response: {
  ports: { /* port mappings */ },
  services: { /* service details */ },
  timestamp: '2026-04-27T...'
}
```

## 📊 Performance Metrics

| Metric | Value | Target |
|--------|-------|--------|
| Bundle Size (Minified) | 5.4 MB | < 6 MB ✅ |
| React Build Time | ~4s | < 5s ✅ |
| Average Response Time | <100ms | < 200ms ✅ |
| Service Startup Time | ~2s | < 3s ✅ |
| Memory Footprint | ~180MB | < 256MB ✅ |

## 🐳 Docker Deployment

### Build Image
```bash
docker build -t leeway-ecosystem:latest .
```

### Run Container
```bash
docker run -d \
  -p 7601-7608:7601-7608 \
  -e NODE_ENV=production \
  --name leeway-ecosystem \
  leeway-ecosystem:latest
```

### Docker Compose
```bash
docker-compose up -d
```

## 🔐 Security Considerations

1. **Environment Variables**: Never commit .env files
2. **GitHub PAT**: Use token with minimal 'repo' scope
3. **NGROK**: Change authentication tokens periodically
4. **Database**: Use encrypted connections only
5. **API Keys**: Rotate Gemini and Alibaba Cloud keys regularly

## 🐛 Troubleshooting

### Port Already in Use
```bash
# Find process using port 7601
lsof -i :7601
# Kill process
kill -9 <PID>
```

### Service Health Check Failing
```bash
# Check service logs
tail -f logs/employment-center.log

# Verify port is listening
netstat -an | grep 7602
```

### React Production Warning
The warning "React is running in production mode but dead code elimination has not been applied" indicates:
- NODE_ENV=production must be set before build
- Terser minifier must be installed
- process.env.NODE_ENV must be defined in vite.config.ts

Solution: Rebuild with `NODE_ENV=production npm run build`

### Large File Upload Issues
Git enforces 100MB file size limit. Large models are excluded via .gitignore.

## 📚 Development Guide

### Adding a New Service

1. Create service directory: `mkdir leeway-new-service`
2. Add to `leeway.services.json` with sequential port
3. Implement health check endpoint at `/health`
4. Update .gitignore for build artifacts
5. Add startup script to ecosystem launcher

### Building for Production

```bash
# Set production environment
export NODE_ENV=production

# Install terser
npm install --save-dev terser

# Build Motherboard UI
cd agent-lee-motherboard
npm run build
cd ..

# Verify output
ls -lh agent-lee-motherboard/dist/
```

### Debugging

```bash
# Enable verbose logging
DEBUG=* npm start

# Attach Node debugger
node --inspect server.js

# View real-time metrics
npm run monitor
```

## 📞 Support & Contact

- **Issues**: GitHub Issues at https://github.com/4citeB4U/leeway-ecosystem/issues
- **Email**: leonardlee6@outlook.com
- **Documentation**: See README files in each service directory

## 📄 License

MIT License - See LICENSE file for details

## ✅ Compliance & Readiness

- ✅ Production-ready code
- ✅ Comprehensive documentation
- ✅ 8 fully configured microservices
- ✅ Sequential port architecture (7601-7608)
- ✅ React 19 optimized build (5.4 MB)
- ✅ All health checks configured
- ✅ Git repository ready for deployment

---

**Last Updated**: April 27, 2026  
**Version**: 2.0.0  
**Status**: ✅ Production Ready
