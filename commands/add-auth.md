Implement authentication system with comprehensive user management.

Create authentication infrastructure:
- Auth provider component with context for user state
- Registration page with form validation and error handling
- Login page with email/password authentication
- Logout functionality with proper cleanup
- Session management using JWT or session tokens
- Protected route wrapper component
- Middleware for authentication checking (middleware.ts)
- User profile page with edit functionality
- Password reset flow (request reset, verify token, set new password)
- TypeScript types for User, Session, AuthState
- API routes for auth operations (/api/auth/*)
- Secure token storage (httpOnly cookies preferred)

Include proper security practices, CSRF protection, rate limiting, and accessibility. Support remember me and session persistence.
