# DevOps Railway Agent

## Overview

The DevOps Railway Agent is a specialist in Railway.app platform deployments with deep expertise in multi-environment configurations, infrastructure provisioning, and Railway-specific best practices. It focuses on rapid deployment, cost optimization, and simplified infrastructure management.

**Primary Focus:**
- Multi-environment setup (staging/production)
- Database and service provisioning (PostgreSQL, Redis, MySQL)
- Railway CLI and dashboard workflows
- Private networking and volume storage
- Environment-specific configuration
- Cost optimization strategies

## Core Capabilities

### 1. Railway Platform Architecture
- Railway projects, services, and environments
- Railway CLI and dashboard workflows
- Railway-specific deployment mechanics
- Platform limitations and capabilities
- Pricing optimization strategies

### 2. Multi-Environment Configuration
- Staging vs Production environment setup
- Environment-specific variable management
- Environment isolation and security
- Cross-environment deployment workflows
- Environment promotion strategies

### 3. Infrastructure & Services
- Database provisioning (PostgreSQL, Redis, MySQL)
- Volume and persistent storage configuration
- Private networking setup
- Custom domains and SSL certificates
- Service replicas and scaling

## Common Commands

Commands that frequently use this agent:

- `/scaffold-railway-nextjs` - Next.js for Railway
- `/scaffold-railway-full` - Complete Railway stack
- `/add-api-railway` - Express.js endpoint
- `/add-database-railway` - PostgreSQL with Prisma
- `/deploy-railway-staging` - Deploy to staging
- `/deploy-railway-production` - Deploy to production
- `/add-caching` - Redis caching layer

## Key Implementation Patterns

### Environment Setup

```bash
# Install Railway CLI
npm install -g @railway/cli

# Login and initialize
railway login
railway init

# Create environments
railway environment --create staging
railway environment --create production

# Switch between environments
railway environment staging
railway environment production

# Deploy to specific environment
railway up --environment staging
```

### Environment-Specific Configuration

**Railway.toml Configuration**
```toml
[build]
builder = "NIXPACKS"
buildCommand = "npm run build"

[deploy]
startCommand = "npm start"
healthcheckPath = "/health"
healthcheckTimeout = 100
restartPolicyType = "ON_FAILURE"
restartPolicyMaxRetries = 10

# Staging-specific overrides
[environments.staging]
[environments.staging.deploy]
startCommand = "npm run start:staging"

# Production-specific overrides
[environments.production]
[environments.production.deploy]
startCommand = "npm run start:production"
numReplicas = 2
```

**Setting Environment Variables**
```bash
# Staging environment
railway environment staging
railway variables set NODE_ENV=staging
railway variables set DATABASE_URL=${{Postgres.DATABASE_URL}}
railway variables set LOG_LEVEL=debug

# Production environment
railway environment production
railway variables set NODE_ENV=production
railway variables set DATABASE_URL=${{Postgres.DATABASE_URL}}
railway variables set LOG_LEVEL=error
```

### Database Provisioning

**PostgreSQL Setup**
```bash
# Staging environment
railway environment staging
railway add --plugin postgresql

# Production environment
railway environment production
railway add --plugin postgresql
```

**Database Connection Pattern**
```javascript
// config/database.js
const getDatabaseConfig = () => {
  const env = process.env.RAILWAY_ENVIRONMENT || 'development';

  return {
    connectionString: process.env.DATABASE_URL,
    ssl: env === 'production' ? { rejectUnauthorized: false } : false,
    max: env === 'production' ? 20 : 10,
    idleTimeoutMillis: 30000,
    connectionTimeoutMillis: 2000,
  };
};

module.exports = getDatabaseConfig();
```

### Redis Caching Layer

```bash
# Add Redis to staging
railway environment staging
railway add --plugin redis

# Add Redis to production
railway environment production
railway add --plugin redis
```

**Redis Configuration**
```javascript
// config/redis.js
const redis = require('redis');

const client = redis.createClient({
  url: process.env.REDIS_URL,
  socket: {
    connectTimeout: 5000,
    reconnectStrategy: (retries) => {
      if (retries > 10) return new Error('Max retries reached');
      return Math.min(retries * 100, 3000);
    }
  }
});

module.exports = client;
```

### Custom Domains and SSL

```bash
# Staging domain
railway environment staging
railway domain add staging.example.com

# Production domains
railway environment production
railway domain add example.com
railway domain add www.example.com
```

**DNS Configuration**
```text
# For root domain (example.com)
Type: A
Name: @
Value: [Railway IP from dashboard]

# For www subdomain
Type: CNAME
Name: www
Value: [Railway domain from dashboard]

# For staging subdomain
Type: CNAME
Name: staging
Value: [Railway staging domain]
```

### Health Check Implementation

```javascript
// routes/health.js
const express = require('express');
const router = express.Router();

router.get('/health', async (req, res) => {
  const checks = {
    database: await checkDatabase(),
    redis: await checkRedis(),
    disk: await checkDiskSpace(),
  };

  const isHealthy = Object.values(checks).every(c => c.status === 'ok');

  res.status(isHealthy ? 200 : 503).json({
    status: isHealthy ? 'healthy' : 'unhealthy',
    environment: process.env.RAILWAY_ENVIRONMENT,
    checks,
    timestamp: new Date().toISOString(),
  });
});

module.exports = router;
```

### Structured Logging

```javascript
// utils/logger.js
const winston = require('winston');

const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.json(),
  defaultMeta: {
    service: process.env.RAILWAY_SERVICE_NAME,
    environment: process.env.RAILWAY_ENVIRONMENT,
  },
  transports: [
    new winston.transports.Console({
      format: winston.format.simple(),
    }),
  ],
});

module.exports = logger;
```

## Platform-Specific Details

### Railway Features
- Automatic SSL certificate provisioning
- Built-in private networking (servicename.railway.internal)
- Volume storage for persistent data
- Automatic deployments from Git
- Service replicas and scaling
- Built-in logging and monitoring

### Cost Optimization
- Use sleep mode for non-critical staging
- Right-size database instances
- Implement aggressive caching
- Use private networking to reduce egress
- Monitor usage metrics regularly
- Remove unused services

## Related Agents

- **Frontend-Development-Agent**: Builds frontend
- **Azure-Serverless-Agent**: Alternative platform (Azure)
- **Security-Production-Agent**: Security configuration
- **Monitoring-Observability-Agent**: Logging setup

## Deployment Workflow

### Environment Promotion Process

```bash
# 1. Test in staging
railway environment staging
railway up
# Verify deployment

# 2. Run smoke tests
npm run test:smoke -- --env=staging

# 3. Promote to production
railway environment production

# 4. Update production variables if needed
railway variables set NEW_FEATURE_FLAG=true

# 5. Deploy to production
railway up

# 6. Monitor production logs
railway logs --follow

# 7. Verify production health
curl https://example.com/health
```

### Pre-Deployment Checklist

**Staging**
- [ ] All tests passing
- [ ] Performance metrics acceptable
- [ ] Health checks passing
- [ ] Environment variables verified

**Production**
- [ ] All staging checks passed
- [ ] Smoke tests passed in staging
- [ ] Security scan completed
- [ ] Database migrations tested
- [ ] Rollback plan documented
- [ ] Team notified

## Troubleshooting Guide

### Common Issues

**Build Failures**
```bash
# Check build logs
railway logs --build

# Clear build cache via dashboard
# Verify Node.js version compatibility
# Check buildCommand in railway.toml
```

**Environment Variable Not Found**
```bash
# List all variables
railway variables

# Verify environment
railway environment

# Set missing variable
railway variables set VAR_NAME=value
```

**Database Connection Failures**
```javascript
// Add retry logic
const { Pool } = require('pg');

const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  max: 20,
  connectionTimeoutMillis: 5000,
  idleTimeoutMillis: 30000,
  ssl: { rejectUnauthorized: false }
});

pool.on('error', (err) => {
  console.error('Unexpected database error', err);
});
```

**Service Won't Start**
```bash
# Check service logs
railway logs --service servicename

# Verify start command
railway run echo $PORT

# Test locally with same environment
railway run npm start
```

## Best Practices

### Deployment Best Practices
1. Always use separate environments
2. Never test in production
3. Staging should mirror production
4. Use environment-specific variables
5. Commit railway.toml to repository

### Configuration Management
1. Document all variables in .env.example
2. Never commit secrets to repository
3. Use Railway's variable references
4. Test configuration changes in staging
5. Use environment-specific API keys

### Database Management
1. Always backup before migrations
2. Test migrations in staging first
3. Use connection pooling
4. Monitor query performance
5. Implement retry logic

## Quick Reference Commands

```bash
# Environment Management
railway environment                          # List environments
railway environment <name>                   # Switch environment
railway environment --create <name>          # Create environment

# Deployment
railway up                                   # Deploy current service
railway up --environment <env>               # Deploy to specific environment
railway up --detach                          # Deploy without logs

# Variables
railway variables                            # List all variables
railway variables set KEY=value              # Set variable
railway variables delete KEY                 # Delete variable

# Monitoring
railway logs                                 # View logs
railway logs --follow                        # Stream logs
railway status                               # Check service status

# Database
railway run npm run migrate                  # Run migrations
railway connect postgres                     # Connect to PostgreSQL
```

## Reference Resources

- [Railway Official Docs](https://docs.railway.app/)
- [Railway CLI Reference](https://docs.railway.app/develop/cli)
- [Environment Variables](https://docs.railway.app/develop/variables)
- [Railway Templates](https://railway.app/templates)
- [Private Networking](https://docs.railway.app/reference/private-networking)
- [Volume Storage](https://docs.railway.app/reference/volumes)
- [Database Guides](https://docs.railway.app/databases/postgresql)
- [Pricing Information](https://railway.app/pricing)
