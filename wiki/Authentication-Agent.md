# Authentication Agent

## Overview

The Authentication Agent is a specialized AI assistant that implements secure authentication and user account management for web applications. It handles user registration, login, session management, protected routes, and role-based access control.

## Core Capabilities

### User Management
- User registration with email verification
- Secure login/logout flows
- Password reset functionality
- Profile management
- Account settings

### Security Features
- JWT token management
- Session handling
- OAuth provider integration
- Multi-factor authentication
- Role-based access control (RBAC)
- Protected route implementation

### Integration Support
- NextAuth.js configuration
- Social login providers (Google, GitHub, etc.)
- Database session storage
- Cookie management
- CSRF protection

## Common Commands

The Authentication Agent works with these commands:

- `/add-auth` - Complete authentication system
- `/add-protected-route` - Protected pages with auth guards
- `/add-social-login` - OAuth provider integration
- `/add-user-management` - User administration panel

## Implementation Patterns

### NextAuth.js Setup

```typescript
// pages/api/auth/[...nextauth].ts
import NextAuth from 'next-auth'
import GoogleProvider from 'next-auth/providers/google'
import GitHubProvider from 'next-auth/providers/github'

export default NextAuth({
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    }),
    GitHubProvider({
      clientId: process.env.GITHUB_ID!,
      clientSecret: process.env.GITHUB_SECRET!,
    }),
  ],
  session: {
    strategy: 'jwt',
    maxAge: 30 * 24 * 60 * 60, // 30 days
  },
  callbacks: {
    async session({ session, token }) {
      session.user.id = token.sub!
      return session
    },
  },
})
```

### Protected Route Middleware

```typescript
// middleware.ts
import { withAuth } from 'next-auth/middleware'

export default withAuth({
  pages: {
    signIn: '/auth/login',
    error: '/auth/error',
  },
})

export const config = {
  matcher: [
    '/dashboard/:path*',
    '/admin/:path*',
    '/api/protected/:path*',
  ],
}
```

### User Authentication Hook

```tsx
// hooks/useAuth.tsx
import { useSession } from 'next-auth/react'

export function useAuth() {
  const { data: session, status } = useSession()

  return {
    user: session?.user,
    isLoading: status === 'loading',
    isAuthenticated: status === 'authenticated',
  }
}
```

## Security Best Practices

### Password Security
- Bcrypt hashing with salt rounds
- Minimum password complexity requirements
- Password strength indicators
- Secure password reset tokens

### Session Management
- HTTP-only cookies
- Secure flag for HTTPS
- SameSite protection
- Session rotation
- Automatic logout on inactivity

### Rate Limiting
- Login attempt limiting
- Account lockout after failures
- CAPTCHA after repeated failures
- IP-based rate limiting

## Platform-Specific Implementation

### Azure Implementation
- Azure Active Directory integration
- Azure B2C for consumer identity
- Key Vault for secret storage
- Application Insights for monitoring

### Railway Implementation
- PostgreSQL session storage
- Redis for session caching
- Environment-based configuration
- Railway secrets management

## Common Use Cases

### 1. E-commerce Authentication
```typescript
// User registration with profile
interface UserRegistration {
  email: string
  password: string
  firstName: string
  lastName: string
  acceptTerms: boolean
  newsletter?: boolean
}
```

### 2. SaaS Application
```typescript
// Multi-tenant authentication
interface TenantUser {
  userId: string
  tenantId: string
  roles: string[]
  permissions: string[]
}
```

### 3. Admin Panel
```typescript
// Role-based access
enum UserRole {
  SUPER_ADMIN = 'super_admin',
  ADMIN = 'admin',
  EDITOR = 'editor',
  VIEWER = 'viewer',
}
```

## Error Handling

### Common Auth Errors
- Invalid credentials
- Account locked
- Email not verified
- Token expired
- Session invalid

### Error Responses
```typescript
interface AuthError {
  code: string
  message: string
  field?: string
  redirect?: string
}
```

## Testing Authentication

### Unit Tests
- Password hashing
- Token generation
- Session validation
- Permission checks

### Integration Tests
- Login flow
- Registration process
- Password reset
- Social login

### E2E Tests
- Complete auth journey
- Protected route access
- Session timeout
- Logout flow

## Accessibility

- Keyboard navigation for all auth forms
- Screen reader announcements
- Error message association
- Focus management
- High contrast support

## Performance Considerations

- Lazy load auth providers
- Cache user sessions
- Optimize database queries
- Minimize token payload
- Use refresh tokens wisely

## Related Agents

- [Security & Production Agent](Security-Production-Agent) - Security audits
- [Forms Workflow Agent](Forms-Workflow-Agent) - Form handling
- [Frontend Development Agent](Frontend-Development-Agent) - UI components

## Commands That Use This Agent

- `/add-auth` - Complete authentication system
- `/add-protected-route` - Protected pages
- `/add-social-login` - Social authentication
- `/add-user-management` - User admin
- `/add-admin-panel` - Admin dashboard
- `/audit-security` - Security review

---

For more information, see:
- [Commands Overview](Commands-Overview)
- [Security Best Practices](Security-Production-Agent)
- [Testing Strategies](Testing-Quality-Agent)