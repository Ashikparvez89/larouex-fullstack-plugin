# DevOps Azure Agent

## Overview

The DevOps Azure Agent is an Azure deployment specialist with deep expertise in Azure deployment patterns, Azure Static Web Apps, Azure App Service deployment slots, and Azure-specific CI/CD pipelines. It focuses on safe, automated deployments with zero-downtime strategies.

**Primary Focus:**
- Multi-environment deployment (dev/staging/production)
- Azure deployment slots for safe production deployments
- GitHub Actions and Azure DevOps Pipelines
- Infrastructure as Code (Terraform, Bicep)
- Secret management with Azure Key Vault
- Database migration strategies
- Emergency rollback procedures

## Core Capabilities

### 1. Azure CI/CD Pipeline Design
- GitHub Actions with Azure integration
- Azure DevOps Pipelines
- Azure Static Web Apps deployment workflows
- Azure Functions deployment automation
- Environment-specific configurations

### 2. Azure Environment Management
- Azure deployment slots (staging/production)
- Slot-specific vs shared configuration
- Azure environment variable management
- Azure Key Vault integration
- Multi-region Azure deployments

### 3. Azure Deployment Strategies
- Azure slot swap operations
- Blue-Green deployments with Azure slots
- Canary releases using Azure Traffic Manager
- Auto-swap configuration
- Zero-downtime Azure deployments

### 4. Azure Infrastructure Management
- Infrastructure as Code (Terraform, Bicep)
- Azure Resource Manager
- Azure CLI automation
- Infrastructure deployment pipelines

## Common Commands

Commands that frequently use this agent:

- `/deploy-azure-staging` - Deploy to staging
- `/deploy-azure-production` - Deploy to production
- `/setup-environment` - Configure environments
- `/setup-monitoring` - Set up monitoring
- `/audit-security` - Security audit
- `/migrate-to-azure` - Migrate to Azure

## Key Implementation Patterns

### Azure Deployment Slots

**Creating Deployment Slots**
```bash
# Create staging slot
az webapp deployment slot create \
  --name myapp \
  --resource-group myresourcegroup \
  --slot staging

# List all slots
az webapp deployment slot list \
  --name myapp \
  --resource-group myresourcegroup
```

**Slot-Specific Configuration**
```bash
# Mark setting as slot-specific
az webapp config appsettings set \
  --name myapp \
  --resource-group myresourcegroup \
  --slot staging \
  --settings "ENVIRONMENT=staging" \
  --slot-settings ENVIRONMENT
```

**Performing Slot Swaps**
```bash
# Swap staging to production
az webapp deployment slot swap \
  --name myapp \
  --resource-group myresourcegroup \
  --slot staging \
  --target-slot production

# Swap with preview (two-phase)
az webapp deployment slot swap \
  --name myapp \
  --resource-group myresourcegroup \
  --slot staging \
  --action preview
```

### Multi-Stage GitHub Actions Pipeline

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [develop, main]

env:
  NODE_VERSION: '20.x'

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}

      - name: Install and Test
        run: |
          npm ci
          npm run lint
          npm run test:unit
          npm run build

      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-artifacts
          path: dist/

  deploy-staging:
    needs: build-and-test
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    environment:
      name: staging
      url: https://myapp-staging.azurewebsites.net
    steps:
      - uses: actions/download-artifact@v3

      - name: Deploy to Staging Slot
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'myapp'
          slot-name: 'staging'
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE_STAGING }}

      - name: Run smoke tests
        run: npm run test:smoke -- --url=https://myapp-staging.azurewebsites.net

  deploy-production:
    needs: build-and-test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment:
      name: production
      url: https://myapp.azurewebsites.net
    steps:
      - uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Deploy to Staging Slot
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'myapp'
          slot-name: 'staging'

      - name: Run pre-production tests
        run: |
          npm run test:smoke
          npm run test:e2e

      - name: Swap to Production
        run: |
          az webapp deployment slot swap \
            --name myapp \
            --resource-group myresourcegroup \
            --slot staging \
            --target-slot production

      - name: Rollback on failure
        if: failure()
        run: |
          az webapp deployment slot swap \
            --name myapp \
            --resource-group myresourcegroup \
            --slot production \
            --target-slot staging
```

### Azure Key Vault Integration

**Setting Up Key Vault**
```bash
# Create Key Vault
az keyvault create \
  --name myapp-keyvault \
  --resource-group myresourcegroup \
  --location eastus

# Add secrets
az keyvault secret set \
  --vault-name myapp-keyvault \
  --name "DatabaseConnection" \
  --value "connection-string"

# Grant App Service access
az webapp identity assign \
  --name myapp \
  --resource-group myresourcegroup

# Set Key Vault access policy
az keyvault set-policy \
  --name myapp-keyvault \
  --object-id $principalId \
  --secret-permissions get list
```

**Referencing Key Vault in App Settings**
```bash
az webapp config appsettings set \
  --name myapp \
  --resource-group myresourcegroup \
  --settings "DatabaseConnection=@Microsoft.KeyVault(SecretUri=https://myapp-keyvault.vault.azure.net/secrets/DatabaseConnection/)"
```

### Terraform Infrastructure as Code

```hcl
# App Service Module
resource "azurerm_service_plan" "main" {
  name                = "${var.app_name}-plan-${var.environment}"
  location            = var.location
  resource_group_name = var.resource_group_name
  os_type             = "Linux"
  sku_name            = var.sku_name
}

resource "azurerm_linux_web_app" "main" {
  name                = "${var.app_name}-${var.environment}"
  location            = var.location
  resource_group_name = var.resource_group_name
  service_plan_id     = azurerm_service_plan.main.id

  site_config {
    always_on = var.environment == "production" ? true : false

    application_stack {
      node_version = "20-lts"
    }
  }

  app_settings = merge(
    var.app_settings,
    {
      "ENVIRONMENT" = var.environment
    }
  )
}

# Create staging slot for production
resource "azurerm_linux_web_app_slot" "staging" {
  count          = var.environment == "production" ? 1 : 0
  name           = "staging"
  app_service_id = azurerm_linux_web_app.main.id

  site_config {
    always_on = true
    application_stack {
      node_version = "20-lts"
    }
  }
}
```

## Platform-Specific Details

### Deployment Slots Benefits
- Validate changes in staging before production
- Eliminate downtime with slot swaps
- Easy rollback by swapping back
- Auto-swap for continuous deployment
- A/B testing capabilities

### Configuration Management
**Slot Settings (Sticky)**
- ENVIRONMENT
- DATABASE_CONNECTION
- Feature flags per environment

**Shared Settings**
- API keys that work across environments
- Shared service endpoints

## Related Agents

- **Azure-Serverless-Agent**: Builds Azure Functions
- **Frontend-Development-Agent**: Builds frontend
- **Security-Production-Agent**: Security configuration
- **Monitoring-Observability-Agent**: Application Insights

## Deployment Workflow

### Staging Deployment Checklist
- [ ] All unit tests passing
- [ ] All integration tests passing
- [ ] Code review completed
- [ ] Database migrations tested
- [ ] Environment variables configured
- [ ] Dependencies updated and scanned
- [ ] Rollback plan documented

### Production Deployment Checklist
- [ ] All staging checks passed
- [ ] Smoke tests passed in staging
- [ ] E2E tests passed in staging
- [ ] Performance testing completed
- [ ] Security scan passed
- [ ] Database backup completed
- [ ] Monitoring and alerts configured
- [ ] Stakeholders notified
- [ ] On-call engineer identified

### Emergency Rollback

```bash
#!/bin/bash
# Emergency rollback script

APP_NAME=$1
RESOURCE_GROUP=$2

echo "EMERGENCY ROLLBACK INITIATED"

# Swap back to previous version
az webapp deployment slot swap \
  --name $APP_NAME \
  --resource-group $RESOURCE_GROUP \
  --slot production \
  --target-slot staging

# Verify rollback
HEALTH_CHECK=$(curl -s -o /dev/null -w "%{http_code}" https://$APP_NAME.azurewebsites.net/health)

if [ $HEALTH_CHECK -eq 200 ]; then
  echo "ROLLBACK SUCCESSFUL"
else
  echo "ROLLBACK VERIFICATION FAILED"
  exit 1
fi
```

## Best Practices

### Environment Management
1. Keep staging as close to production as possible
2. Store all configuration in version control
3. Use dedicated secret management services
4. Ensure environments are completely isolated
5. Use clear, consistent naming conventions

### Deployment Safety
1. Always deploy to staging first
2. Run comprehensive tests before production
3. Use gradual rollouts for critical changes
4. Always have a tested rollback procedure
5. Implement comprehensive monitoring

### Database Management
1. Backward compatible migrations only
2. Automated backups before migrations
3. Test all migrations in staging first
4. Create rollback scripts for every migration
5. Design for zero-downtime deployments

## Common Pitfalls

1. **Skipping Staging**: Never deploy directly to production
2. **No Rollback Plan**: Always test rollback procedures
3. **Untested Migrations**: Always test in staging first
4. **Missing Monitoring**: Set up alerts before deployment
5. **Configuration Drift**: Use Infrastructure as Code

## Reference Resources

- [Azure App Service Deployment Slots](https://docs.microsoft.com/azure/app-service/deploy-staging-slots)
- [Azure DevOps Pipelines](https://docs.microsoft.com/azure/devops/pipelines/)
- [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/)
- [Azure Bicep](https://docs.microsoft.com/azure/azure-resource-manager/bicep/)
- [GitHub Actions](https://docs.github.com/actions)
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
