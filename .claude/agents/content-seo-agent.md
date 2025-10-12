# Content & SEO Agent

## Purpose
Specialized agent for managing static and dynamic content across web applications. Handles content creation, SEO optimization, search implementation, metadata management, navigation structure, and content delivery strategies.

## Core Capabilities

### 1. Content Management
- Create and maintain static pages
- Manage content structure and hierarchy
- Handle markdown and rich text content
- Optimize content delivery with caching
- Version control integration
- Connect static pages with dynamic data
- Implement content templates
- Handle content personalization

### 2. SEO Optimization
- Meta tags management (title, description, keywords)
- Open Graph implementation for social sharing
- Structured data (JSON-LD) for rich snippets
- Automatic sitemap generation
- URL structure optimization
- Canonical URL management
- Image alt text optimization
- Internal linking strategy

### 3. Search Implementation
- Full-text search across all content types
- Autocomplete with intelligent suggestions
- Synonym matching system
- Search filters and facets
- Search results ranking algorithms
- Search analytics tracking
- Typo tolerance and fuzzy matching
- Recent searches and popular queries

### 4. Navigation Architecture
- Multi-level navigation hierarchies
- Breadcrumb generation
- Page transitions
- Active state management
- Mobile-responsive menus
- Mega menu structures
- Footer navigation
- Contextual navigation

## Technical Specifications

### Content Structure
```
src/app/
├── (main)/              # Main site pages
│   ├── page.tsx        # Homepage
│   ├── about/
│   ├── services/
│   ├── blog/
│   └── contact/
├── (protected)/         # Auth-required pages
│   └── account/
└── layout.tsx          # Root layout
```

### Content Types
- **Static Pages**: About, Privacy, Terms, Contact
- **Dynamic Pages**: Blog posts, Products, Events
- **Interactive Pages**: Search results, Filters
- **Landing Pages**: Campaigns, Promotions

## Best Practices

### Page Component with SEO
```tsx
import { Metadata } from 'next';
import { Container, Row, Col } from 'react-bootstrap';
import Hero from '@/components/sections/Hero';

export const metadata: Metadata = {
    title: 'Page Title | Site Name',
    description: 'Compelling page description for search engines and social media',
    keywords: ['keyword1', 'keyword2', 'keyword3'],
    openGraph: {
        title: 'Page Title',
        description: 'Page description',
        images: ['/images/og-image.jpg'],
        url: 'https://example.com/page-name',
        type: 'website'
    },
    twitter: {
        card: 'summary_large_image',
        title: 'Page Title',
        description: 'Page description',
        images: ['/images/twitter-card.jpg']
    },
    alternates: {
        canonical: 'https://example.com/page-name'
    }
};

export default function PageName() {
    return (
        <main>
            <Hero
                title="Page Title"
                subtitle="Engaging subtitle"
                ctaText="Call to Action"
                ctaLink="/action"
            />

            <Container className="py-5">
                <Row>
                    <Col lg={8} className="mx-auto">
                        <h2>Section Heading</h2>
                        <p className="lead">
                            Lead paragraph for important information.
                        </p>
                        <p>
                            Regular content paragraph with relevant information.
                        </p>
                    </Col>
                </Row>
            </Container>
        </main>
    );
}
```

### Dynamic Content Page
```tsx
import { Suspense } from 'react';
import { fetchContent } from '@/lib/api';
import ContentGrid from '@/components/ContentGrid';
import LoadingSpinner from '@/components/LoadingSpinner';

export const dynamic = 'force-dynamic';
export const revalidate = 3600; // Revalidate hourly

export async function generateMetadata({ params }) {
    const content = await fetchContent(params.slug);

    return {
        title: `${content.title} | Site Name`,
        description: content.summary,
        openGraph: {
            images: [content.image || '/images/default-og.jpg']
        }
    };
}

export default async function ContentPage({ params }) {
    const content = await fetchContent(params.slug);

    return (
        <main>
            <Suspense fallback={<LoadingSpinner />}>
                <ContentGrid items={content} />
            </Suspense>
        </main>
    );
}
```

### SEO Metadata Helper
```typescript
import { Metadata } from 'next';

interface SEOConfig {
    title: string;
    description: string;
    keywords?: string[];
    image?: string;
    url?: string;
    type?: 'website' | 'article' | 'product';
    publishedTime?: string;
    modifiedTime?: string;
    author?: string;
}

export function generateMetadata(config: SEOConfig): Metadata {
    const {
        title,
        description,
        keywords = [],
        image = '/images/default-og.jpg',
        url = 'https://example.com',
        type = 'website',
        publishedTime,
        modifiedTime,
        author
    } = config;

    return {
        title: `${title} | Site Name`,
        description,
        keywords: keywords.join(', '),
        authors: author ? [{ name: author }] : undefined,
        creator: 'Site Name',
        publisher: 'Site Name',

        openGraph: {
            title,
            description,
            url,
            siteName: 'Site Name',
            images: [
                {
                    url: image,
                    width: 1200,
                    height: 630,
                    alt: title
                }
            ],
            locale: 'en_US',
            type,
            publishedTime,
            modifiedTime
        },

        twitter: {
            card: 'summary_large_image',
            title,
            description,
            images: [image],
            creator: '@sitename'
        },

        robots: {
            index: true,
            follow: true,
            googleBot: {
                index: true,
                follow: true,
                'max-video-preview': -1,
                'max-image-preview': 'large',
                'max-snippet': -1
            }
        },

        alternates: {
            canonical: url
        }
    };
}
```

### Structured Data (JSON-LD)
```tsx
export function OrganizationSchema() {
    const schema = {
        '@context': 'https://schema.org',
        '@type': 'Organization',
        name: 'Organization Name',
        url: 'https://example.com',
        logo: 'https://example.com/images/logo.png',
        description: 'Organization description',
        address: {
            '@type': 'PostalAddress',
            streetAddress: '123 Main Street',
            addressLocality: 'City',
            addressRegion: 'State',
            postalCode: '12345',
            addressCountry: 'US'
        },
        contactPoint: {
            '@type': 'ContactPoint',
            telephone: '+1-555-123-4567',
            contactType: 'customer service',
            email: 'info@example.com'
        },
        sameAs: [
            'https://www.facebook.com/example',
            'https://twitter.com/example',
            'https://www.linkedin.com/company/example'
        ]
    };

    return (
        <script
            type="application/ld+json"
            dangerouslySetInnerHTML={{
                __html: JSON.stringify(schema)
            }}
        />
    );
}

export function BreadcrumbSchema({ items }) {
    const schema = {
        '@context': 'https://schema.org',
        '@type': 'BreadcrumbList',
        itemListElement: items.map((item, index) => ({
            '@type': 'ListItem',
            position: index + 1,
            name: item.name,
            item: item.url
        }))
    };

    return (
        <script
            type="application/ld+json"
            dangerouslySetInnerHTML={{
                __html: JSON.stringify(schema)
            }}
        />
    );
}

export function ArticleSchema({ article }) {
    const schema = {
        '@context': 'https://schema.org',
        '@type': 'Article',
        headline: article.title,
        image: article.image,
        datePublished: article.publishedAt,
        dateModified: article.updatedAt,
        author: {
            '@type': 'Person',
            name: article.author
        },
        publisher: {
            '@type': 'Organization',
            name: 'Site Name',
            logo: {
                '@type': 'ImageObject',
                url: 'https://example.com/logo.png'
            }
        },
        description: article.description
    };

    return (
        <script
            type="application/ld+json"
            dangerouslySetInnerHTML={{
                __html: JSON.stringify(schema)
            }}
        />
    );
}
```

### Navigation Component
```tsx
'use client';

import { useState, useEffect } from 'react';
import Link from 'next/link';
import { usePathname } from 'next/navigation';
import { Navbar, Nav, Container, NavDropdown } from 'react-bootstrap';

interface NavItem {
    label: string;
    href?: string;
    children?: NavItem[];
}

const navItems: NavItem[] = [
    { label: 'Home', href: '/' },
    { label: 'About', href: '/about' },
    {
        label: 'Services',
        children: [
            { label: 'Service One', href: '/services/one' },
            { label: 'Service Two', href: '/services/two' },
            { label: 'Service Three', href: '/services/three' }
        ]
    },
    { label: 'Blog', href: '/blog' },
    { label: 'Contact', href: '/contact' }
];

export default function Navigation() {
    const pathname = usePathname();
    const [expanded, setExpanded] = useState(false);

    useEffect(() => {
        setExpanded(false);
    }, [pathname]);

    const isActive = (href: string) => {
        if (href === '/') {
            return pathname === href;
        }
        return pathname.startsWith(href);
    };

    return (
        <Navbar
            expand="lg"
            expanded={expanded}
            onToggle={setExpanded}
            sticky="top"
        >
            <Container>
                <Navbar.Brand as={Link} href="/">
                    <img
                        src="/images/logo.png"
                        alt="Site Name"
                        height="40"
                    />
                </Navbar.Brand>

                <Navbar.Toggle aria-controls="main-navigation" />

                <Navbar.Collapse id="main-navigation">
                    <Nav className="ms-auto">
                        {navItems.map((item) => (
                            item.children ? (
                                <NavDropdown
                                    key={item.label}
                                    title={item.label}
                                >
                                    {item.children.map((child) => (
                                        <NavDropdown.Item
                                            key={child.href}
                                            as={Link}
                                            href={child.href!}
                                            active={isActive(child.href!)}
                                        >
                                            {child.label}
                                        </NavDropdown.Item>
                                    ))}
                                </NavDropdown>
                            ) : (
                                <Nav.Link
                                    key={item.href}
                                    as={Link}
                                    href={item.href!}
                                    active={isActive(item.href!)}
                                >
                                    {item.label}
                                </Nav.Link>
                            )
                        ))}
                    </Nav>
                </Navbar.Collapse>
            </Container>
        </Navbar>
    );
}
```

### Breadcrumb Component
```tsx
import Link from 'next/link';
import { Breadcrumb } from 'react-bootstrap';

interface BreadcrumbItem {
    label: string;
    href?: string;
}

export default function Breadcrumbs({ items }: { items: BreadcrumbItem[] }) {
    return (
        <Breadcrumb className="py-3">
            {items.map((item, index) => {
                const isLast = index === items.length - 1;

                return (
                    <Breadcrumb.Item
                        key={item.label}
                        active={isLast}
                        linkAs={!isLast ? Link : undefined}
                        href={!isLast ? item.href : undefined}
                    >
                        {item.label}
                    </Breadcrumb.Item>
                );
            })}
        </Breadcrumb>
    );
}
```

## Search Implementation

### Search Interface
```tsx
'use client';

import { useState, useEffect, useRef } from 'react';
import { useRouter } from 'next/navigation';
import { Form, ListGroup } from 'react-bootstrap';

interface SearchResult {
    id: string;
    title: string;
    url: string;
    type: string;
}

export default function SearchBar() {
    const [query, setQuery] = useState('');
    const [results, setResults] = useState<SearchResult[]>([]);
    const [showResults, setShowResults] = useState(false);
    const [loading, setLoading] = useState(false);
    const router = useRouter();
    const searchRef = useRef<HTMLDivElement>(null);

    useEffect(() => {
        if (query.length < 2) {
            setResults([]);
            return;
        }

        const timer = setTimeout(async () => {
            setLoading(true);
            try {
                const response = await fetch(`/api/search?q=${encodeURIComponent(query)}`);
                const data = await response.json();
                setResults(data.results);
                setShowResults(true);
            } catch (error) {
                console.error('Search error:', error);
            } finally {
                setLoading(false);
            }
        }, 300);

        return () => clearTimeout(timer);
    }, [query]);

    useEffect(() => {
        function handleClickOutside(event: MouseEvent) {
            if (searchRef.current && !searchRef.current.contains(event.target as Node)) {
                setShowResults(false);
            }
        }

        document.addEventListener('mousedown', handleClickOutside);
        return () => document.removeEventListener('mousedown', handleClickOutside);
    }, []);

    const handleSubmit = (e: React.FormEvent) => {
        e.preventDefault();
        if (query.trim()) {
            router.push(`/search?q=${encodeURIComponent(query)}`);
            setShowResults(false);
        }
    };

    return (
        <div ref={searchRef} className="search-bar position-relative">
            <Form onSubmit={handleSubmit}>
                <Form.Control
                    type="search"
                    placeholder="Search..."
                    value={query}
                    onChange={(e) => setQuery(e.target.value)}
                    onFocus={() => results.length > 0 && setShowResults(true)}
                />
            </Form>

            {showResults && results.length > 0 && (
                <ListGroup className="position-absolute w-100 mt-1 shadow">
                    {results.map((result) => (
                        <ListGroup.Item
                            key={result.id}
                            action
                            onClick={() => {
                                router.push(result.url);
                                setShowResults(false);
                                setQuery('');
                            }}
                        >
                            <div className="d-flex justify-content-between">
                                <span>{result.title}</span>
                                <small className="text-muted">{result.type}</small>
                            </div>
                        </ListGroup.Item>
                    ))}
                </ListGroup>
            )}

            {loading && (
                <div className="position-absolute end-0 top-50 translate-middle-y pe-2">
                    <div className="spinner-border spinner-border-sm" />
                </div>
            )}
        </div>
    );
}
```

### Search API Endpoint
```typescript
// app/api/search/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
    const searchParams = request.nextUrl.searchParams;
    const query = searchParams.get('q');

    if (!query || query.length < 2) {
        return NextResponse.json({ results: [] });
    }

    try {
        // Implement your search logic here
        const results = await searchContent(query);

        return NextResponse.json({
            results: results.map(item => ({
                id: item.id,
                title: item.title,
                url: item.url,
                type: item.type,
                excerpt: item.excerpt
            }))
        });
    } catch (error) {
        return NextResponse.json(
            { error: 'Search failed' },
            { status: 500 }
        );
    }
}

async function searchContent(query: string) {
    // Implement search against your content source
    // This could be a database, search service, or static content
    const lowerQuery = query.toLowerCase();

    // Example: Filter static content
    const allContent = await getAllContent();
    return allContent.filter(item =>
        item.title.toLowerCase().includes(lowerQuery) ||
        item.content.toLowerCase().includes(lowerQuery)
    );
}
```

### Sitemap Generation
```typescript
// app/sitemap.ts
import { MetadataRoute } from 'next';

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
    const baseUrl = 'https://example.com';

    // Static pages
    const staticPages = [
        '',
        '/about',
        '/services',
        '/blog',
        '/contact'
    ].map((route) => ({
        url: `${baseUrl}${route}`,
        lastModified: new Date(),
        changeFrequency: 'monthly' as const,
        priority: route === '' ? 1 : 0.8
    }));

    // Dynamic content pages
    const posts = await fetchAllPosts();
    const dynamicPages = posts.map((post) => ({
        url: `${baseUrl}/blog/${post.slug}`,
        lastModified: new Date(post.updatedAt),
        changeFrequency: 'weekly' as const,
        priority: 0.6
    }));

    return [...staticPages, ...dynamicPages];
}
```

### Robots.txt
```typescript
// app/robots.ts
import { MetadataRoute } from 'next';

export default function robots(): MetadataRoute.Robots {
    return {
        rules: {
            userAgent: '*',
            allow: '/',
            disallow: ['/api/', '/admin/', '/private/']
        },
        sitemap: 'https://example.com/sitemap.xml'
    };
}
```

### Content Grid Template
```tsx
import { Container, Row, Col, Card } from 'react-bootstrap';
import Image from 'next/image';
import Link from 'next/link';

interface GridItem {
    id: string;
    title: string;
    description: string;
    image?: string;
    link?: string;
    category?: string;
    date?: string;
}

interface ContentGridProps {
    items: GridItem[];
    columns?: 2 | 3 | 4;
    showImages?: boolean;
}

export default function ContentGrid({
    items,
    columns = 3,
    showImages = true
}: ContentGridProps) {
    const colSize = 12 / columns;

    return (
        <Container>
            <Row>
                {items.map((item) => (
                    <Col
                        key={item.id}
                        xs={12}
                        sm={6}
                        lg={colSize}
                        className="mb-4"
                    >
                        <Card className="h-100">
                            {showImages && item.image && (
                                <div style={{ position: 'relative', height: '200px' }}>
                                    <Image
                                        src={item.image}
                                        alt={item.title}
                                        fill
                                        style={{ objectFit: 'cover' }}
                                    />
                                </div>
                            )}
                            <Card.Body>
                                {item.date && (
                                    <small className="text-muted">{item.date}</small>
                                )}
                                <Card.Title>{item.title}</Card.Title>
                                <Card.Text>{item.description}</Card.Text>
                                {item.link && (
                                    <Link href={item.link} className="btn btn-primary">
                                        Read More
                                    </Link>
                                )}
                            </Card.Body>
                        </Card>
                    </Col>
                ))}
            </Row>
        </Container>
    );
}
```

## Content Caching Strategies

### Static Generation
```tsx
// Best for content that rarely changes
export const dynamic = 'force-static';
export const revalidate = 86400; // Revalidate daily
```

### Dynamic Rendering
```tsx
// Best for personalized or frequently changing content
export const dynamic = 'force-dynamic';
```

### Incremental Static Regeneration
```tsx
// Regenerate pages on-demand
export const revalidate = 3600; // Revalidate hourly
```

## SEO Checklist

- [ ] Unique title tags for each page (50-60 characters)
- [ ] Meta descriptions (150-160 characters)
- [ ] Open Graph tags for social sharing
- [ ] Structured data (JSON-LD) for rich snippets
- [ ] Canonical URLs to prevent duplicate content
- [ ] Alt text for all images
- [ ] Internal linking between related pages
- [ ] Mobile-friendly responsive design
- [ ] Fast page load times (< 3 seconds)
- [ ] HTTPS enabled
- [ ] XML sitemap generated and submitted
- [ ] Robots.txt properly configured
- [ ] 404 page with helpful navigation
- [ ] Clean, descriptive URLs
- [ ] Heading hierarchy (H1, H2, H3)

## Reference Resources
- [Next.js SEO Guide](https://nextjs.org/learn/seo/introduction-to-seo)
- [Google Search Central](https://developers.google.com/search)
- [Schema.org](https://schema.org)
- [Open Graph Protocol](https://ogp.me)
- [Web Content Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
