Deploy to Railway production environment with mandatory review gate and validation.

MANDATORY PRE-DEPLOYMENT REVIEW GATE:
- Execute /review-before-deploy command FIRST
- Review must show NO Critical or High severity issues
- Require explicit manual confirmation: "I have reviewed the findings and approve deployment to production"
- STOP DEPLOYMENT if review is not completed or issues are unresolved

WARNING: Deploying to production without completing the review gate bypasses critical safety checks for security vulnerabilities, performance issues, accessibility compliance, and configuration errors. This may result in production incidents, data exposure, or service degradation.

Execute production deployment pipeline ONLY after review approval:
- Run full test suite (unit, integration, e2e) and verify all pass
- Check staging deployment status and health
- Switch to production environment (railway environment production)
- Validate environment variables for production
- Validate monitoring and logging is configured (Railway logs, health endpoints)
- Create database backup before deployment
- Deploy services to production using Railway CLI
- Run database migrations on production database
- Monitor Railway logs for errors (5-minute window)
- Verify production endpoints and health checks
- Provide rollback instructions with previous deployment ID

Include pre-deployment checklist, post-deployment verification, and Railway dashboard monitoring links. Stop deployment if any validation fails.
