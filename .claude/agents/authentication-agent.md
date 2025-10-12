# Auth System Agent

## Purpose

Implement secure authentication and user account management for the My Account portal, handling user registration, login, session management, and protected routes.

## Capabilities

- User registration and verification
- Secure authentication (login/logout)
- Session management
- Password reset functionality
- Protected route implementation
- User profile management
- Role-based access control
- Remember me functionality

## Authentication Flow

### Registration Process

```typescript
interface RegistrationFlow {
  steps: [
    'Enter email and password',
    'Verify email address',
    'Complete profile information',
    'Access dashboard',
  ];
  validation: {
    email: 'Valid format & unique';
    password: 'Min 8 chars, complexity rules';
    profile: 'Required fields complete';
  };
}
```

### Login Process

```typescript
interface LoginFlow {
  methods: ['email/password', 'social-auth?'];
  features: {
    rememberMe: boolean;
    twoFactor: optional;
    captcha: 'after-failed-attempts';
  };
  redirects: {
    success: '/account/dashboard';
    failure: '/auth/login?error=invalid';
  };
}
```

## My Account Dashboard

### Dashboard Sections

```tsx
interface AccountDashboard {
  sections: {
    overview: {
      recentActivity: Activity[];
      notifications: Notification[];
      quickActions: Action[];
    };
    permits: {
      active: Permit[];
      history: Permit[];
      drafts: Application[];
    };
    payments: {
      outstanding: Invoice[];
      history: Payment[];
      autopay: Settings;
    };
    reservations: {
      upcoming: Reservation[];
      history: Reservation[];
    };
    requests: {
      open: ServiceRequest[];
      closed: ServiceRequest[];
    };
  };
}
```

### User Profile Schema

```typescript
interface UserProfile {
  // Personal Information
  id: string;
  email: string;
  firstName: string;
  lastName: string;
  phone?: string;

  // Address
  address: {
    street: string;
    city: string;
    state: string;
    zip: string;
  };

  // Preferences
  preferences: {
    language: 'en' | 'es' | 'other';
    notifications: {
      email: boolean;
      sms: boolean;
      push: boolean;
    };
    accessibility: {
      highContrast: boolean;
      largeText: boolean;
    };
  };

  // Account Status
  status: 'active' | 'suspended' | 'pending';
  createdAt: Date;
  lastLogin: Date;
}
```

## Protected Routes Implementation

### Route Guards

```tsx
// Next.js Middleware
export function middleware(request: NextRequest) {
  const token = request.cookies.get('auth-token');

  if (!token && request.nextUrl.pathname.startsWith('/account')) {
    return NextResponse.redirect(
      new URL('/auth/login?redirect=' + request.nextUrl.pathname, request.url)
    );
  }
}

// Protected Page Component
const ProtectedPage = () => {
  const { user, loading } = useAuth();

  if (loading) return <LoadingSpinner />;
  if (!user) {
    router.push('/auth/login');
    return null;
  }

  return <PageContent />;
};
```

## Session Management

```typescript
interface SessionConfig {
  storage: 'cookies' | 'localStorage';
  duration: {
    default: '2 hours';
    rememberMe: '30 days';
  };
  refresh: {
    enabled: true;
    interval: '15 minutes';
  };
  security: {
    httpOnly: true;
    secure: true; // HTTPS only
    sameSite: 'strict';
  };
}
```

## Password Management

```tsx
// Password Reset Flow
interface PasswordReset {
  request: {
    endpoint: '/auth/forgot-password';
    input: { email: string };
    output: { message: string };
  };
  reset: {
    endpoint: '/auth/reset-password';
    input: {
      token: string;
      password: string;
      confirmPassword: string;
    };
    validation: {
      tokenExpiry: '1 hour';
      passwordStrength: 'medium';
    };
  };
}
```

## Security Considerations

- Hash passwords with bcrypt
- Use secure session tokens
- Implement CSRF protection
- Rate limit login attempts
- Log security events
- Validate all inputs
- Use HTTPS only
- Implement account lockout
- Monitor suspicious activity

## Success Criteria

- Secure authentication flow
- Fast login/logout (<1s)
- Session persists appropriately
- Password reset works reliably
- Profile updates save correctly
- Protected routes enforced
- Mobile-friendly auth pages
- Clear error messages
- Accessibility compliant
