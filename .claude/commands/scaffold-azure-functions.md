Create an Azure Functions v4 project with TypeScript.

Set up a complete Azure Functions application with:
- TypeScript configuration (tsconfig.json with proper Azure Functions settings)
- host.json with Function Runtime v4 configuration
- local.settings.json template with example connection strings
- package.json with Azure Functions dependencies (@azure/functions, @azure/data-tables)
- Function app structure: /src/functions with example HTTP-triggered functions
- Example functions: GetItems, CreateItem, UpdateItem with Table Storage integration
- Shared utilities: /src/utils with Table Storage client, validation helpers, error handling
- .funcignore and .gitignore files
- README.md with local development and deployment instructions

Include proper error handling, input validation, and CORS configuration for each function.
