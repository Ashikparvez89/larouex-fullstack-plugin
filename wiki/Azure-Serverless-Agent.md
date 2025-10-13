# Azure Serverless Agent

## Overview

The Azure Serverless Agent specializes in developing, deploying, and managing Azure serverless applications including Azure Functions, Azure Static Web Apps, and Azure Table Storage. It handles API development, deployment automation, CI/CD pipelines, and cloud infrastructure management.

**Primary Technologies:**
- Azure Functions v4 (TypeScript/Node.js 20)
- Azure Static Web Apps
- Azure Table Storage (NoSQL)
- Application Insights
- GitHub Actions for CI/CD

## Core Capabilities

### 1. Azure Functions Development
- Create HTTP-triggered functions in TypeScript
- Implement request/response handling with type safety
- Configure function bindings and triggers
- Manage function app settings and environment variables
- Implement CORS policies and security headers
- Handle authentication and authorization
- Optimize cold start performance

### 2. Azure Table Storage Operations
- Design efficient table storage schemas
- Create optimal PartitionKey and RowKey strategies
- Implement CRUD operations with error handling
- Manage storage connections and credentials
- Optimize queries for performance
- Handle batch operations
- Implement data validation and sanitization

### 3. Azure Static Web Apps
- Deploy Next.js and React applications
- Configure routing and fallback rules
- Set up custom domains and SSL certificates
- Configure authentication providers
- Optimize CDN and caching strategies
- Manage staging environments
- Implement preview deployments

### 4. CI/CD Pipeline Management
- GitHub Actions workflows for automation
- Automated testing integration
- Environment-specific deployments
- Release management and rollback procedures
- Blue-green deployments
- Infrastructure as code

## Common Commands

Commands that frequently use this agent:

- `/scaffold-azure-nextjs` - Next.js for Azure
- `/scaffold-azure-functions` - Azure Functions API
- `/scaffold-azure-full` - Complete Azure stack
- `/add-api-azure` - Azure Function endpoint
- `/add-database-azure` - Azure Table Storage
- `/deploy-azure-staging` - Deploy to staging
- `/deploy-azure-production` - Deploy to production

## Key Implementation Patterns

### Azure Function Template

```typescript
import { app, HttpRequest, HttpResponseInit, InvocationContext } from "@azure/functions";

export async function functionName(
    request: HttpRequest,
    context: InvocationContext
): Promise<HttpResponseInit> {
    context.log(`HTTP function ${request.method} ${request.url}`);

    try {
        // Validate request
        const body = await request.json();

        if (!body.requiredField) {
            return {
                status: 400,
                jsonBody: { error: 'Missing required field' }
            };
        }

        // Process business logic
        const result = await processData(body);

        return {
            status: 200,
            jsonBody: {
                success: true,
                data: result
            }
        };
    } catch (error) {
        context.error('Error processing request:', error);
        return {
            status: 500,
            jsonBody: { error: 'Internal server error' }
        };
    }
}

app.http('functionName', {
    methods: ['GET', 'POST'],
    authLevel: 'function',
    route: 'custom-route',
    handler: functionName
});
```

### Azure Table Storage Operations

```typescript
import { TableClient, AzureNamedKeyCredential } from "@azure/data-tables";

const accountName = process.env.AZURE_STORAGE_ACCOUNT!;
const accountKey = process.env.AZURE_STORAGE_KEY!;
const credential = new AzureNamedKeyCredential(accountName, accountKey);

const tableClient = new TableClient(
    `https://${accountName}.table.core.windows.net`,
    "myTable",
    credential
);

// Create entity
export async function createEntity(data: any) {
    const entity = {
        partitionKey: data.category,
        rowKey: data.id,
        ...data,
        timestamp: new Date().toISOString()
    };

    await tableClient.createEntity(entity);
    return entity;
}

// Get entity
export async function getEntity(partitionKey: string, rowKey: string) {
    return await tableClient.getEntity(partitionKey, rowKey);
}

// Query entities
export async function queryEntities(filter: string) {
    const entities = tableClient.listEntities({
        queryOptions: { filter }
    });

    const results = [];
    for await (const entity of entities) {
        results.push(entity);
    }
    return results;
}
```

### Health Check Endpoint

```typescript
interface HealthStatus {
    status: 'healthy' | 'unhealthy';
    timestamp: string;
    checks: {
        database: 'healthy' | 'unhealthy';
        storage: 'healthy' | 'unhealthy';
    };
}

export async function health(
    request: HttpRequest,
    context: InvocationContext
): Promise<HttpResponseInit> {
    const checks = {
        database: await checkDatabase(),
        storage: await checkStorage()
    };

    const isHealthy = Object.values(checks).every(v => v === 'healthy');

    return {
        status: isHealthy ? 200 : 503,
        jsonBody: {
            status: isHealthy ? 'healthy' : 'unhealthy',
            timestamp: new Date().toISOString(),
            checks
        }
    };
}
```

### GitHub Actions Workflow

```yaml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: |
          npm ci
          cd api && npm ci

      - name: Run tests
        run: npm test

      - name: Build And Deploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          app_location: "/"
          api_location: "api"
          output_location: ".next"
```

### Static Web App Configuration

```json
{
  "routes": [
    {
      "route": "/api/*",
      "allowedRoles": ["anonymous"]
    },
    {
      "route": "/admin/*",
      "allowedRoles": ["authenticated", "administrator"]
    }
  ],
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/images/*.{png,jpg,gif}", "/api/*"]
  },
  "globalHeaders": {
    "X-Content-Type-Options": "nosniff",
    "X-Frame-Options": "DENY",
    "Referrer-Policy": "strict-origin-when-cross-origin"
  },
  "platform": {
    "apiRuntime": "node:20"
  }
}
```

## Platform-Specific Details

### File Structure
```
project/
├── api/                     # Azure Functions
│   ├── host.json
│   ├── local.settings.json
│   └── src/functions/
├── .github/workflows/       # CI/CD
├── staticwebapp.config.json # Static Web App config
└── next.config.ts
```

### Environment Configuration
```typescript
interface EnvironmentConfig {
    // Application
    NEXT_PUBLIC_APP_URL: string;
    NEXT_PUBLIC_API_URL: string;

    // Azure Storage
    AZURE_STORAGE_CONNECTION_STRING: string;
    AZURE_STORAGE_ACCOUNT: string;
    AZURE_STORAGE_KEY: string;

    // Application Insights
    APPLICATION_INSIGHTS_CONNECTION_STRING: string;
    APPINSIGHTS_INSTRUMENTATIONKEY: string;
}
```

### Cold Start Optimization
- Minimize dependencies
- Use connection pooling
- Enable Always On (premium plans)
- Implement warming triggers
- Optimize bundle size

## Related Agents

- **DevOps-Azure-Agent**: Handles deployment pipelines
- **Frontend-Development-Agent**: Builds frontend for Azure
- **Monitoring-Observability-Agent**: Application Insights setup
- **Security-Production-Agent**: Security configuration

## Best Practices Checklist

- [ ] Use TypeScript for type safety
- [ ] Implement comprehensive error handling
- [ ] Add input validation with schemas
- [ ] Configure CORS properly
- [ ] Set up Application Insights
- [ ] Use environment variables for secrets
- [ ] Implement health check endpoints
- [ ] Add structured logging
- [ ] Optimize for cold starts
- [ ] Test locally before deploying

## Common Pitfalls

1. **Cold Starts**: Minimize dependencies and use connection pooling
2. **CORS Issues**: Configure in both function.json and staticwebapp.config.json
3. **Environment Variables**: Set in Azure Portal for production
4. **Storage Connections**: Use proper connection string format
5. **Deployment Failures**: Check Node.js version compatibility

## Deployment Procedures

### Azure CLI Commands
```bash
# Login to Azure
az login

# Create Static Web App
az staticwebapp create \
    --name my-web-app \
    --resource-group my-resource-group \
    --location "Central US" \
    --sku Standard

# Configure environment variables
az staticwebapp appsettings set \
    --name my-web-app \
    --setting-names API_KEY=value

# Configure custom domain
az staticwebapp hostname set \
    --hostname www.example.com \
    --name my-web-app
```

### Local Development
```bash
# Install Azure Functions Core Tools
npm install -g azure-functions-core-tools@4

# Install Static Web Apps CLI
npm install -g @azure/static-web-apps-cli

# Start local development
swa start http://localhost:3000 --api-location ./api
```

## Reference Resources

- [Azure Functions Documentation](https://docs.microsoft.com/azure/azure-functions/)
- [Azure Static Web Apps Documentation](https://docs.microsoft.com/azure/static-web-apps/)
- [Azure Table Storage Documentation](https://docs.microsoft.com/azure/storage/tables/)
- [GitHub Actions for Azure](https://github.com/Azure/actions)
- [Next.js on Azure](https://docs.microsoft.com/azure/static-web-apps/deploy-nextjs)
