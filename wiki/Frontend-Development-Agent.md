# Frontend Development Agent

## Overview

The Frontend Development Agent specializes in creating modern, responsive web applications using React, TypeScript, and Bootstrap. It focuses on component architecture, responsive design, accessibility, and consistent user experience across all devices.

**Primary Technologies:**
- React 18+ with functional components
- TypeScript with strict mode
- Bootstrap 5.3+ for responsive UI
- Next.js 15 with App Router
- CSS Modules for component-scoped styling

## Core Capabilities

### 1. Component Development
Creates reusable React functional components with:
- TypeScript interfaces and props
- State management with hooks (useState, useEffect, useContext)
- Component lifecycle handling
- Performance optimization with memoization (memo, useMemo, useCallback)
- Proper error boundaries

### 2. Responsive Design
Implements mobile-first design principles:
- Bootstrap grid system (xs, sm, md, lg, xl breakpoints)
- Viewport-specific styling and layouts
- Touch-friendly interfaces for mobile devices
- Cross-browser compatibility
- Responsive typography and spacing

### 3. Bootstrap Integration
Leverages Bootstrap components and utilities:
- Grid system with Container, Row, Col
- Pre-built components (Navbar, Card, Modal, Button)
- Utility classes for rapid development
- Custom theme integration
- Responsive breakpoint utilities

### 4. Navigation Systems
Builds comprehensive navigation:
- Multi-level navigation hierarchies
- Responsive patterns (desktop mega menus, mobile hamburgers)
- Breadcrumb navigation
- Keyboard accessibility
- Active state management

### 5. Accessibility (WCAG 2.1 AA)
Ensures inclusive design:
- Semantic HTML structure
- ARIA attributes and roles
- Keyboard navigation support
- Screen reader optimization
- Focus management

## Common Commands

Commands that frequently use this agent:

- `/add-component` - Create new React components
- `/add-page` - Build new pages with routing
- `/add-layout` - Generate layout components
- `/add-navigation` - Implement navigation systems
- `/add-modal` - Create modal dialogs
- `/optimize-performance` - Component optimization

## Key Implementation Patterns

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

### Performance Optimization

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

### Code Splitting with Next.js

```tsx
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(
    () => import('./HeavyComponent'),
    {
        loading: () => <LoadingSpinner />,
        ssr: false
    }
);
```

## Platform-Specific Details

### Next.js Integration
- Uses App Router for routing and layouts
- Server Components vs Client Components ('use client')
- Image optimization with next/image
- Metadata API for SEO
- Loading and error states

### Bootstrap Configuration
- Bootstrap 5.3+ via react-bootstrap
- Custom SCSS variables for theming
- CSS Modules for component-specific styles
- Utility classes for rapid prototyping

## Related Agents

- **Forms-Workflow-Agent**: Handles complex form components and validation
- **Content-SEO-Agent**: Manages page metadata and SEO optimization
- **Accessibility-Compliance-Agent**: Ensures WCAG compliance
- **Testing-Quality-Agent**: Creates component tests

## Best Practices Checklist

- [ ] Use TypeScript interfaces for all props
- [ ] Implement proper error boundaries
- [ ] Use semantic HTML elements
- [ ] Add ARIA labels where needed
- [ ] Test on mobile, tablet, and desktop
- [ ] Optimize images and assets
- [ ] Implement loading states
- [ ] Use CSS Modules for styling
- [ ] Avoid hydration mismatches
- [ ] Clean up effects with proper dependencies

## Common Pitfalls

1. **Hydration Mismatches**: Use dynamic imports with `ssr: false` for client-only components
2. **Bootstrap CSS Conflicts**: Use CSS modules to scope styles
3. **Memory Leaks**: Always cleanup timers, subscriptions, and event listeners
4. **Missing Dependencies**: Properly declare useEffect dependencies
5. **Accessibility**: Don't forget alt text, ARIA labels, and keyboard support

## Example Use Cases

### Building a Hero Section
```tsx
import Hero from '@/components/sections/Hero';

<Hero
    title="Welcome to Our Site"
    subtitle="Building the future together"
    ctaText="Get Started"
    ctaLink="/signup"
    backgroundImage="/images/hero-bg.jpg"
/>
```

### Creating a Card Grid
```tsx
<Container>
    <Row>
        {items.map((item) => (
            <Col key={item.id} xs={12} md={6} lg={4} className="mb-4">
                <Card>
                    <Card.Img variant="top" src={item.image} />
                    <Card.Body>
                        <Card.Title>{item.title}</Card.Title>
                        <Card.Text>{item.description}</Card.Text>
                        <Button variant="primary">Learn More</Button>
                    </Card.Body>
                </Card>
            </Col>
        ))}
    </Row>
</Container>
```

## Reference Resources

- [React Documentation](https://react.dev)
- [Bootstrap 5 Documentation](https://getbootstrap.com/docs/5.3/)
- [Next.js Documentation](https://nextjs.org/docs)
- [TypeScript React Patterns](https://react-typescript-cheatsheet.netlify.app)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
