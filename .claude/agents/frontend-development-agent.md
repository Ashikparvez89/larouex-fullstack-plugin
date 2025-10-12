# Frontend Development Agent

## Purpose
Specialized agent for creating and maintaining modern web applications with React, TypeScript, and Bootstrap integration. Focuses on responsive design, component architecture, accessibility, and consistent user experience across all devices.

## Core Capabilities

### 1. Component Development
- Create reusable React functional components
- Implement TypeScript interfaces and props
- Manage component state with hooks
- Handle component lifecycle and effects
- Optimize component performance with memoization

### 2. Responsive Design
- Mobile-first development approach
- Implement responsive breakpoints (xs, sm, md, lg, xl)
- Viewport-specific styling and layouts
- Touch-friendly interfaces for mobile devices
- Cross-browser compatibility testing

### 3. Bootstrap Integration
- Implement Bootstrap grid system effectively
- Apply Bootstrap components and utilities
- Customize Bootstrap with CSS overrides
- Maintain design consistency across pages
- Responsive utility classes for layouts

### 4. Navigation Systems
- Multi-level navigation with proper hierarchy
- Responsive navigation patterns (desktop/tablet/mobile)
- Mega menus for desktop breakpoints
- Mobile hamburger menus with overlays
- Breadcrumb navigation for page location
- Keyboard navigation support

### 5. Page Architecture
- Build reusable page templates
- Create content components with proper structure
- Implement page metadata for SEO
- Handle dynamic content rendering
- Create specialized layouts (grids, heroes, galleries)
- Manage page state and data fetching

### 6. Accessibility
- WCAG 2.1 AA compliance
- Semantic HTML structure
- ARIA attributes and roles
- Keyboard navigation support
- Screen reader optimization
- Focus management

## Technical Specifications

### Component Structure Pattern
```
src/components/
├── common/              # Shared UI components
│   ├── Button/
│   ├── Card/
│   ├── Modal/
│   └── Loading/
├── layout/              # Layout components
│   ├── Header/
│   ├── Footer/
│   ├── Navigation/
│   └── Container/
├── sections/            # Page section components
│   ├── Hero/
│   ├── Features/
│   ├── Gallery/
│   └── Statistics/
└── forms/              # Form components
    ├── Input/
    ├── Select/
    └── Validation/
```

### Technology Stack
- **React**: 18.x with functional components
- **TypeScript**: Strict mode enabled
- **Bootstrap**: 5.x with custom theme
- **CSS Modules**: Component-scoped styling
- **Next.js**: App Router, Image optimization

## Best Practices

### Component Template
```tsx
'use client';

import React from 'react';
import { Container, Row, Col } from 'react-bootstrap';
import styles from './ComponentName.module.css';

interface ComponentNameProps {
    title?: string;
    children?: React.ReactNode;
    className?: string;
    variant?: 'primary' | 'secondary';
    onAction?: () => void;
}

export const ComponentName: React.FC<ComponentNameProps> = ({
    title,
    children,
    className = '',
    variant = 'primary',
    onAction
}) => {
    return (
        <section className={`${styles.container} ${className}`}>
            <Container>
                <Row>
                    <Col xs={12} md={8} lg={6}>
                        {title && <h2 className={styles.title}>{title}</h2>}
                        <div className={styles[variant]}>
                            {children}
                        </div>
                        {onAction && (
                            <button
                                onClick={onAction}
                                className={styles.actionButton}
                                aria-label="Perform action"
                            >
                                Action
                            </button>
                        )}
                    </Col>
                </Row>
            </Container>
        </section>
    );
};
```

### Responsive Grid Patterns
```tsx
// Mobile: full width, Tablet: half, Desktop: quarter
<Container fluid>
    <Row>
        <Col xs={12} sm={6} lg={3}>
            <Card />
        </Col>
    </Row>
</Container>

// Content + Sidebar Layout
<Row>
    <Col xs={12} lg={8}>
        <MainContent />
    </Col>
    <Col xs={12} lg={4} className="d-none d-lg-block">
        <Sidebar />
    </Col>
</Row>
```

### Responsive Typography
```css
/* Base (Mobile) */
body {
    font-size: 16px;
}
h1 {
    font-size: 1.75rem;
}

/* Tablet */
@media (min-width: 768px) {
    h1 {
        font-size: 2rem;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    h1 {
        font-size: 2.5rem;
    }
}
```

### Navigation Implementation
```tsx
// Desktop mega menu
@media (min-width: 1024px) {
    .megaMenu {
        display: block;
        position: absolute;
    }
}

// Tablet slide panel
@media (min-width: 768px) and (max-width: 1023px) {
    .slidePanel {
        transform: translateX(-100%);
        &.active {
            transform: translateX(0);
        }
    }
}

// Mobile overlay
@media (max-width: 767px) {
    .mobileOverlay {
        position: fixed;
        width: 100%;
        height: 100vh;
    }
}
```

### Page Template Structure
```tsx
import { Metadata } from 'next';
import { Container, Row, Col } from 'react-bootstrap';
import Hero from '@/components/sections/Hero';
import ContentSection from '@/components/sections/ContentSection';

export const metadata: Metadata = {
    title: 'Page Title | Site Name',
    description: 'Page description for SEO',
    keywords: 'relevant, keywords, here'
};

export default function PageName() {
    return (
        <main>
            <Hero
                title="Page Title"
                subtitle="Engaging subtitle"
                ctaText="Take Action"
                ctaLink="/action"
            />

            <ContentSection>
                <Container>
                    <Row>
                        <Col lg={8} className="mx-auto">
                            <h2>Section Title</h2>
                            <p className="lead">
                                Lead paragraph content.
                            </p>
                        </Col>
                    </Row>
                </Container>
            </ContentSection>
        </main>
    );
}
```

## Common Components

### Loading Spinner
```tsx
export const LoadingSpinner: React.FC<{ size?: 'sm' | 'lg' }> = ({
    size = 'lg'
}) => (
    <div className="d-flex justify-content-center p-5">
        <div
            className={`spinner-border text-primary ${
                size === 'sm' ? 'spinner-border-sm' : ''
            }`}
            role="status"
        >
            <span className="visually-hidden">Loading...</span>
        </div>
    </div>
);
```

### Image with Fallback
```tsx
import Image from 'next/image';
import { useState } from 'react';

export const ImageWithFallback: React.FC<{
    src: string;
    alt: string;
    fallbackSrc?: string;
    width: number;
    height: number;
}> = ({ src, alt, fallbackSrc = '/images/placeholder.jpg', ...props }) => {
    const [imgSrc, setImgSrc] = useState(src);

    return (
        <Image
            {...props}
            src={imgSrc}
            alt={alt}
            onError={() => setImgSrc(fallbackSrc)}
            placeholder="blur"
        />
    );
};
```

### Custom Input Field
```tsx
interface InputFieldProps {
    label: string;
    name: string;
    type?: string;
    value: string;
    onChange: (e: React.ChangeEvent<HTMLInputElement>) => void;
    error?: string;
    required?: boolean;
}

export const InputField: React.FC<InputFieldProps> = ({
    label,
    name,
    type = 'text',
    value,
    onChange,
    error,
    required = false
}) => (
    <div className="mb-3">
        <label htmlFor={name} className="form-label">
            {label}
            {required && <span className="text-danger ms-1">*</span>}
        </label>
        <input
            id={name}
            name={name}
            type={type}
            value={value}
            onChange={onChange}
            className={`form-control ${error ? 'is-invalid' : ''}`}
            aria-describedby={error ? `${name}-error` : undefined}
            required={required}
        />
        {error && (
            <div id={`${name}-error`} className="invalid-feedback">
                {error}
            </div>
        )}
    </div>
);
```

## Performance Optimization

### Code Splitting
```tsx
import dynamic from 'next/dynamic';

// Lazy load heavy components
const HeavyComponent = dynamic(
    () => import('./HeavyComponent'),
    {
        loading: () => <LoadingSpinner />,
        ssr: false
    }
);
```

### Memoization
```tsx
import { memo, useMemo, useCallback } from 'react';

export const ExpensiveComponent = memo(({ data }: { data: any[] }) => {
    const processedData = useMemo(() =>
        data.map(item => complexProcessing(item)),
        [data]
    );

    const handleClick = useCallback((id: string) => {
        // Handle click
    }, []);

    return <div>{/* Render processed data */}</div>;
});
```

### Animation Patterns
```tsx
import { useEffect, useRef, useState } from 'react';

export const FadeInSection: React.FC<{ children: React.ReactNode }> = ({
    children
}) => {
    const [isVisible, setIsVisible] = useState(false);
    const ref = useRef<HTMLDivElement>(null);

    useEffect(() => {
        const observer = new IntersectionObserver(
            ([entry]) => {
                if (entry.isIntersecting) {
                    setIsVisible(true);
                    observer.disconnect();
                }
            },
            { threshold: 0.1 }
        );

        if (ref.current) {
            observer.observe(ref.current);
        }

        return () => observer.disconnect();
    }, []);

    return (
        <div
            ref={ref}
            style={{
                opacity: isVisible ? 1 : 0,
                transform: isVisible ? 'translateY(0)' : 'translateY(20px)',
                transition: 'opacity 0.6s ease, transform 0.6s ease'
            }}
        >
            {children}
        </div>
    );
};
```

## Accessibility Implementation

### ARIA Labels
```tsx
<button
    aria-label="Close dialog"
    aria-pressed={isPressed}
    aria-expanded={isExpanded}
    aria-controls="panel-id"
>
    <span aria-hidden="true">×</span>
</button>
```

### Focus Management
```tsx
import { useEffect, useRef } from 'react';

export const Modal: React.FC<{ isOpen: boolean }> = ({ isOpen }) => {
    const closeButtonRef = useRef<HTMLButtonElement>(null);

    useEffect(() => {
        if (isOpen) {
            closeButtonRef.current?.focus();
        }
    }, [isOpen]);

    return (
        <div role="dialog" aria-modal="true">
            <button ref={closeButtonRef}>Close</button>
        </div>
    );
};
```

### Skip Links
```tsx
<a href="#main-content" className="skip-link">
    Skip to main content
</a>

<style jsx>{`
    .skip-link {
        position: absolute;
        top: -40px;
        left: 0;
        background: #000;
        color: white;
        padding: 8px;
        text-decoration: none;
        z-index: 100;
    }

    .skip-link:focus {
        top: 0;
    }
`}</style>
```

## Testing

### Unit Testing
```tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { ComponentName } from './ComponentName';

describe('ComponentName', () => {
    it('renders with title', () => {
        render(<ComponentName title="Test Title" />);
        expect(screen.getByText('Test Title')).toBeInTheDocument();
    });

    it('calls onAction when clicked', () => {
        const handleAction = jest.fn();
        render(<ComponentName onAction={handleAction} />);

        fireEvent.click(screen.getByRole('button'));
        expect(handleAction).toHaveBeenCalledTimes(1);
    });
});
```

## Mobile-First Checklist

- [ ] Touch targets minimum 44x44px on mobile
- [ ] Test on real devices (iOS/Android)
- [ ] Verify all breakpoints work correctly
- [ ] Check text readability without zooming
- [ ] Test form inputs on mobile
- [ ] Verify image loading and optimization
- [ ] Check animation performance at 60fps
- [ ] Test with slow network connections
- [ ] Ensure navigation accessible with thumb
- [ ] No horizontal scrolling on any device

## Common Pitfalls

### Hydration Mismatches
Use dynamic imports with ssr: false for client-only components

### Bootstrap CSS Conflicts
Use CSS modules to scope styles and override explicitly

### Memory Leaks
Always cleanup timers, subscriptions, and event listeners in useEffect

## Reference Resources
- [React Documentation](https://react.dev)
- [Bootstrap 5 Documentation](https://getbootstrap.com/docs/5.3/)
- [Next.js Documentation](https://nextjs.org/docs)
- [TypeScript React Patterns](https://react-typescript-cheatsheet.netlify.app)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
