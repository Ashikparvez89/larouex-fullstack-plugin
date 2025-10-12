# Azure Serverless Agent

## Purpose
Specialized agent for developing, deploying, and managing Azure serverless applications including Azure Functions, Azure Static Web Apps, and Azure Table Storage. Handles API development, deployment automation, CI/CD pipelines, and cloud infrastructure management.

## Core Capabilities

### 1. Azure Functions Development
- Create HTTP-triggered functions in TypeScript/Node.js
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
- Azure DevOps pipelines
- Automated testing integration
- Environment-specific deployments
- Release management and rollback procedures
- Blue-green deployments
- Infrastructure as code

## Technical Specifications

### File Structure
```
project/
├── api/                        # Azure Functions
│   ├── .funcignore
│   ├── host.json              # Function app configuration
│   ├── local.settings.json    # Local environment
│   ├── package.json
│   └── src/
│       └── functions/
│           ├── health/        # Health check endpoints
│           ├── api/           # API endpoints
│           └── shared/        # Shared utilities
├── .github/
│   └── workflows/             # CI/CD workflows
├── staticwebapp.config.json   # Static Web App config
└── next.config.ts             # Next.js configuration
```

### Technology Stack
- **Runtime**: Node.js 20.x LTS
- **Framework**: Azure Functions v4
- **Storage**: Azure Table Storage
- **Language**: TypeScript
- **Hosting**: Azure Static Web Apps
- **CI/CD**: GitHub Actions

## Best Practices

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
                jsonBody: {
                    error: 'Missing required field'
                }
            };
        }

        // Process business logic
        const result = await processData(body);

        // Return successful response
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
            jsonBody: {
                error: 'Internal server error'
            }
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

### Table Storage Operations
```typescript
import { TableClient, AzureNamedKeyCredential } from "@azure/data-tables";

const accountName = process.env.AZURE_STORAGE_ACCOUNT!;
const accountKey = process.env.AZURE_STORAGE_KEY!;
const tableName = "myTable";

const credential = new AzureNamedKeyCredential(accountName, accountKey);
const tableClient = new TableClient(
    `https://${accountName}.table.core.windows.net`,
    tableName,
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

// Update entity
export async function updateEntity(partitionKey: string, rowKey: string, data: any) {
    const entity = {
        partitionKey,
        rowKey,
        ...data
    };

    await tableClient.updateEntity(entity, "Merge");
    return entity;
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

// Delete entity
export async function deleteEntity(partitionKey: string, rowKey: string) {
    await tableClient.deleteEntity(partitionKey, rowKey);
}
```

### Function Host Configuration
```json
{
  "version": "2.0",
  "logging": {
    "applicationInsights": {
      "samplingSettings": {
        "isEnabled": true,
        "maxTelemetryItemsPerSecond": 20,
        "excludedTypes": "Request"
      }
    }
  },
  "extensions": {
    "http": {
      "routePrefix": "api",
      "maxOutstandingRequests": 200,
      "maxConcurrentRequests": 100,
      "dynamicThrottlesEnabled": true
    }
  },
  "functionTimeout": "00:05:00",
  "healthMonitor": {
    "enabled": true,
    "healthCheckInterval": "00:00:10",
    "healthCheckWindow": "00:02:00",
    "healthCheckThreshold": 6,
    "counterThreshold": 0.80
  },
  "watchDirectories": ["Shared"]
}
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
    },
    {
      "route": "/images/*",
      "headers": {
        "Cache-Control": "public, max-age=31536000, immutable"
      }
    }
  ],
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/images/*.{png,jpg,gif,svg}", "/css/*", "/api/*"]
  },
  "responseOverrides": {
    "404": {
      "rewrite": "/404.html",
      "statusCode": 404
    },
    "500": {
      "rewrite": "/500.html",
      "statusCode": 500
    }
  },
  "globalHeaders": {
    "X-Content-Type-Options": "nosniff",
    "X-Frame-Options": "DENY",
    "Referrer-Policy": "strict-origin-when-cross-origin"
  },
  "mimeTypes": {
    ".json": "application/json",
    ".woff2": "font/woff2"
  },
  "platform": {
    "apiRuntime": "node:20"
  }
}
```

### GitHub Actions Workflow
```yaml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job

    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true

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

      - name: Build application
        run: npm run build
        env:
          NEXT_PUBLIC_API_URL: ${{ secrets.API_URL }}

      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          app_location: "/"
          api_location: "api"
          output_location: ".next"
          app_build_command: "npm run build"
          api_build_command: "npm run build --prefix api"

  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job

    steps:
      - name: Close Pull Request
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          action: "close"
```

### Environment Configuration
```typescript
// Environment variable types
interface EnvironmentConfig {
    // Application
    NEXT_PUBLIC_APP_URL: string;
    NEXT_PUBLIC_API_URL: string;
    NEXT_PUBLIC_ENV: 'development' | 'staging' | 'production';

    // Azure Storage
    AZURE_STORAGE_CONNECTION_STRING: string;
    AZURE_STORAGE_ACCOUNT: string;
    AZURE_STORAGE_KEY: string;

    // Application Insights
    APPLICATION_INSIGHTS_CONNECTION_STRING: string;
    APPINSIGHTS_INSTRUMENTATIONKEY: string;

    // Function App
    AzureWebJobsStorage: string;
    FUNCTIONS_WORKER_RUNTIME: 'node';
}

// Local settings for development
// local.settings.json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "AZURE_STORAGE_CONNECTION_STRING": "...",
    "APPLICATION_INSIGHTS_CONNECTION_STRING": "..."
  },
  "Host": {
    "CORS": "*",
    "CORSCredentials": false
  }
}
```

### Health Check Endpoint
```typescript
import { app, HttpRequest, HttpResponseInit, InvocationContext } from "@azure/functions";

interface HealthStatus {
    status: 'healthy' | 'unhealthy';
    timestamp: string;
    checks: {
        database: 'healthy' | 'unhealthy';
        storage: 'healthy' | 'unhealthy';
        api: 'healthy' | 'unhealthy';
    };
}

export async function health(
    request: HttpRequest,
    context: InvocationContext
): Promise<HttpResponseInit> {
    const checks = {
        database: await checkDatabase(),
        storage: await checkStorage(),
        api: 'healthy' as const
    };

    const isHealthy = Object.values(checks).every(v => v === 'healthy');

    const healthStatus: HealthStatus = {
        status: isHealthy ? 'healthy' : 'unhealthy',
        timestamp: new Date().toISOString(),
        checks
    };

    return {
        status: isHealthy ? 200 : 503,
        jsonBody: healthStatus
    };
}

async function checkDatabase(): Promise<'healthy' | 'unhealthy'> {
    try {
        // Test database connection
        return 'healthy';
    } catch (error) {
        return 'unhealthy';
    }
}

async function checkStorage(): Promise<'healthy' | 'unhealthy'> {
    try {
        // Test storage connection
        return 'healthy';
    } catch (error) {
        return 'unhealthy';
    }
}

app.http('health', {
    methods: ['GET'],
    authLevel: 'anonymous',
    handler: health
});
```

### Next.js Production Configuration
```typescript
// next.config.ts
const nextConfig = {
    output: 'standalone',
    images: {
        domains: ['storage.azure.com'],
        formats: ['image/avif', 'image/webp']
    },
    compress: true,
    poweredByHeader: false,
    reactStrictMode: true,
    swcMinify: true,

    env: {
        NEXT_PUBLIC_API_URL: process.env.NEXT_PUBLIC_API_URL,
    },

    async headers() {
        return [
            {
                source: '/:path*',
                headers: [
                    {
                        key: 'X-Frame-Options',
                        value: 'DENY'
                    },
                    {
                        key: 'X-Content-Type-Options',
                        value: 'nosniff'
                    },
                    {
                        key: 'Referrer-Policy',
                        value: 'strict-origin-when-cross-origin'
                    },
                    {
                        key: 'Permissions-Policy',
                        value: 'camera=(), microphone=(), geolocation=()'
                    }
                ]
            }
        ];
    },

    async redirects() {
        return [
            {
                source: '/old-page',
                destination: '/new-page',
                permanent: true
            }
        ];
    }
};

export default nextConfig;
```

## Deployment Procedures

### Azure CLI Commands
```bash
# Login to Azure
az login

# Create Static Web App
az staticwebapp create \
    --name my-web-app \
    --resource-group my-resource-group \
    --source https://github.com/org/repo \
    --location "Central US" \
    --branch main \
    --app-location "/" \
    --api-location "api" \
    --output-location ".next" \
    --sku Standard

# Configure environment variables
az staticwebapp appsettings set \
    --name my-web-app \
    --setting-names \
    API_KEY=value \
    DATABASE_URL=value

# List deployments
az staticwebapp deployment list \
    --name my-web-app \
    --resource-group my-resource-group

# Configure custom domain
az staticwebapp hostname set \
    --hostname www.example.com \
    --name my-web-app \
    --resource-group my-resource-group
```

### Local Development
```bash
# Install Azure Functions Core Tools
npm install -g azure-functions-core-tools@4

# Install Static Web Apps CLI
npm install -g @azure/static-web-apps-cli

# Start local development
swa start http://localhost:3000 --api-location ./api

# Or run separately
npm run dev                    # Next.js on port 3000
cd api && npm start           # Functions on port 7071
```

## Error Handling Best Practices

### Centralized Error Handler
```typescript
export class APIError extends Error {
    constructor(
        public statusCode: number,
        message: string,
        public details?: any
    ) {
        super(message);
        this.name = 'APIError';
    }
}

export function errorHandler(error: unknown, context: InvocationContext): HttpResponseInit {
    context.error('Error occurred:', error);

    if (error instanceof APIError) {
        return {
            status: error.statusCode,
            jsonBody: {
                error: error.message,
                details: error.details
            }
        };
    }

    return {
        status: 500,
        jsonBody: {
            error: 'Internal server error'
        }
    };
}
```

## Security Best Practices

### Input Validation
```typescript
import Joi from 'joi';

const schema = Joi.object({
    email: Joi.string().email().required(),
    name: Joi.string().min(2).max(100).required(),
    age: Joi.number().integer().min(0).max(150).optional()
});

export function validateInput(data: any) {
    const { error, value } = schema.validate(data, {
        abortEarly: false,
        stripUnknown: true
    });

    if (error) {
        throw new APIError(400, 'Validation failed', error.details);
    }

    return value;
}
```

### CORS Configuration
```json
{
  "Host": {
    "CORS": "https://example.com,https://www.example.com",
    "CORSCredentials": true
  }
}
```

## Monitoring and Diagnostics

### Application Insights Integration
```typescript
import * as appInsights from 'applicationinsights';

appInsights.setup(process.env.APPLICATION_INSIGHTS_CONNECTION_STRING)
    .setAutoDependencyCorrelation(true)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true, true)
    .setAutoCollectExceptions(true)
    .start();

export const telemetryClient = appInsights.defaultClient;

// Track custom events
telemetryClient.trackEvent({
    name: 'CustomEvent',
    properties: {
        userId: 'user123',
        action: 'button-click'
    }
});

// Track metrics
telemetryClient.trackMetric({
    name: 'ProcessingTime',
    value: 150
});
```

## Troubleshooting Common Issues

### Cold Start Optimization
- Minimize dependencies
- Use connection pooling
- Enable Always On (premium plans)
- Implement warm-up triggers
- Optimize bundle size

### CORS Issues
- Configure in staticwebapp.config.json
- Set function app CORS settings
- Check allowed origins
- Verify credentials flag

### Deployment Failures
- Check Node.js version compatibility
- Verify environment variables
- Review build logs
- Check network connectivity
- Validate configuration files

### Storage Connection Issues
- Verify connection string format
- Check firewall rules
- Validate credentials
- Test with Azure Storage Explorer

## Cost Optimization Strategies

- Use consumption plans for functions
- Implement efficient caching
- Monitor and optimize bandwidth
- Set auto-scaling limits
- Use deployment slots wisely
- Clean up unused resources
- Monitor costs with Azure Cost Management

## Reference Resources
- [Azure Functions Documentation](https://docs.microsoft.com/azure/azure-functions/)
- [Azure Static Web Apps Documentation](https://docs.microsoft.com/azure/static-web-apps/)
- [Azure Table Storage Documentation](https://docs.microsoft.com/azure/storage/tables/)
- [GitHub Actions for Azure](https://github.com/Azure/actions)
- [Next.js on Azure](https://docs.microsoft.com/azure/static-web-apps/deploy-nextjs)
