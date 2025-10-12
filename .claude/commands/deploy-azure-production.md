Deploy to Azure production with mandatory review gate and comprehensive validation.

MANDATORY PRE-DEPLOYMENT REVIEW GATE:
- Execute /review-before-deploy command FIRST
- Review must show NO Critical or High severity issues
- Require explicit manual confirmation: "I have reviewed the findings and approve deployment to production"
- STOP DEPLOYMENT if review is not completed or issues are unresolved

WARNING: Deploying to production without completing the review gate bypasses critical safety checks for security vulnerabilities, performance issues, accessibility compliance, and configuration errors. This may result in production incidents, data exposure, or service degradation.

Execute production deployment pipeline ONLY after review approval:
- Run full test suite (unit, integration, e2e) and verify all pass
- Check staging deployment status and health
- Validate environment variables for production
- Validate Application Insights is configured and monitoring enabled
- Build Next.js with production optimizations
- Create deployment snapshot/backup point
- Deploy to production slot with slot swap preview
- Perform slot swap from staging to production
- Monitor Application Insights for errors (5-minute window)
- Verify production endpoints and health checks
- Provide rollback instructions with slot swap revert commands

Include pre-deployment checklist, post-deployment verification, and monitoring dashboard links. Stop deployment if any validation fails.
