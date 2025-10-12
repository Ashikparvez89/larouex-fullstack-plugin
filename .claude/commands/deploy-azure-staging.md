Deploy the current project to Azure staging environment.

Execute deployment workflow:
- Check if Azure Static Web Apps staging slot exists, create if missing
- Configure staging-specific environment variables and app settings
- Build Next.js application with production optimization
- Deploy frontend to Azure Static Web Apps staging slot
- Deploy Azure Functions API to staging environment
- Run smoke tests on staging endpoints
- Verify deployment health and function app status
- Generate deployment summary with staging URL
- Create rollback instructions if issues occur

Use Azure CLI (az staticwebapp) for deployment operations. Provide clear status updates and verification steps. Include staging URL for immediate testing.
