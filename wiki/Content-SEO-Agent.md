# Content & SEO Agent

## Overview

The Content & SEO Agent specializes in managing static and dynamic content, SEO optimization, search implementation, and content delivery strategies. It ensures your site is discoverable, performs well in search engines, and delivers content efficiently.

**Primary Focus:**
- Content structure and hierarchy
- SEO optimization with meta tags and structured data
- Search implementation with autocomplete
- Navigation architecture
- Sitemap and robots.txt generation
- Content caching strategies

## Core Capabilities

### 1. Content Management
- Create and maintain static pages
- Manage content structure and hierarchy
- Handle markdown and rich text content
- Optimize content delivery with caching
- Version control integration
- Connect static pages with dynamic data
- Implement content templates

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

### 4. Navigation Architecture
- Multi-level navigation hierarchies
- Breadcrumb generation
- Page transitions
- Active state management
- Mobile-responsive menus
- Mega menu structures
- Footer and contextual navigation

## Common Commands

Commands that frequently use this agent:

- `/add-page` - Create new pages with SEO
- `/optimize-seo` - Optimize page SEO
- `/add-search` - Implement search functionality
- `/add-navigation` - Build navigation systems
- `/add-cms-ui` - Content management interface
- `/add-markdown-support` - Markdown rendering

## Key Implementation Patterns

### Page Component with SEO

```tsx
import { Metadata } from 'next';

export const metadata: Metadata = {
    title: 'Page Title | Site Name',
    description: 'Compelling page description for search engines',
    keywords: ['keyword1', 'keyword2', 'keyword3'],
    openGraph: {
        title: 'Page Title',
        description: 'Page description',
        images: ['/images/og-image.jpg'],
        url: 'https://example.com/page',
        type: 'website'
    },
    twitter: {
        card: 'summary_large_image',
        title: 'Page Title',
        description: 'Page description',
        images: ['/images/twitter-card.jpg']
    },
    alternates: {
        canonical: 'https://example.com/page'
    }
};

export default function PageName() {
    return (
        <main>
            {/* Page content */}
        </main>
    );
}
```

### Dynamic Content with Metadata

```tsx
export async function generateMetadata({ params }): Promise<Metadata> {
    const content = await fetchContent(params.slug);

    return {
        title: `${content.title} | Site Name`,
        description: content.summary,
        openGraph: {
            images: [content.image || '/images/default-og.jpg']
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
        logo: 'https://example.com/logo.png',
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
        }
    };

    return (
        <script
            type="application/ld+json"
            dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
        />
    );
}
```

### Search Implementation

```tsx
export default function SearchBar() {
    const [query, setQuery] = useState('');
    const [results, setResults] = useState<SearchResult[]>([]);
    const [showResults, setShowResults] = useState(false);
    const router = useRouter();

    useEffect(() => {
        if (query.length < 2) {
            setResults([]);
            return;
        }

        const timer = setTimeout(async () => {
            const response = await fetch(`/api/search?q=${encodeURIComponent(query)}`);
            const data = await response.json();
            setResults(data.results);
            setShowResults(true);
        }, 300);

        return () => clearTimeout(timer);
    }, [query]);

    return (
        <div className="search-bar">
            <Form.Control
                type="search"
                placeholder="Search..."
                value={query}
                onChange={(e) => setQuery(e.target.value)}
            />
            {showResults && results.length > 0 && (
                <ListGroup className="position-absolute">
                    {results.map((result) => (
                        <ListGroup.Item
                            key={result.id}
                            action
                            onClick={() => router.push(result.url)}
                        >
                            {result.title}
                        </ListGroup.Item>
                    ))}
                </ListGroup>
            )}
        </div>
    );
}
```

### Navigation Component

```tsx
export default function Navigation() {
    const pathname = usePathname();
    const [expanded, setExpanded] = useState(false);

    const navItems = [
        { label: 'Home', href: '/' },
        { label: 'About', href: '/about' },
        {
            label: 'Services',
            children: [
                { label: 'Service One', href: '/services/one' },
                { label: 'Service Two', href: '/services/two' }
            ]
        }
    ];

    const isActive = (href: string) => {
        if (href === '/') return pathname === href;
        return pathname.startsWith(href);
    };

    return (
        <Navbar expand="lg" expanded={expanded} onToggle={setExpanded}>
            <Container>
                <Navbar.Brand as={Link} href="/">
                    Site Name
                </Navbar.Brand>
                <Navbar.Toggle />
                <Navbar.Collapse>
                    <Nav className="ms-auto">
                        {navItems.map((item) => (
                            item.children ? (
                                <NavDropdown key={item.label} title={item.label}>
                                    {item.children.map((child) => (
                                        <NavDropdown.Item
                                            key={child.href}
                                            as={Link}
                                            href={child.href}
                                            active={isActive(child.href)}
                                        >
                                            {child.label}
                                        </NavDropdown.Item>
                                    ))}
                                </NavDropdown>
                            ) : (
                                <Nav.Link
                                    key={item.href}
                                    as={Link}
                                    href={item.href}
                                    active={isActive(item.href)}
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

### Sitemap Generation

```typescript
// app/sitemap.ts
import { MetadataRoute } from 'next';

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
    const baseUrl = 'https://example.com';

    // Static pages
    const staticPages = ['', '/about', '/services', '/contact'].map((route) => ({
        url: `${baseUrl}${route}`,
        lastModified: new Date(),
        changeFrequency: 'monthly' as const,
        priority: route === '' ? 1 : 0.8
    }));

    // Dynamic pages
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

## Platform-Specific Details

### Next.js Configuration
- Metadata API for SEO
- Automatic sitemap generation
- Static and dynamic rendering
- Image optimization
- Caching strategies (ISR, SSG, SSR)

### Content Caching Strategies
```tsx
// Static Generation
export const dynamic = 'force-static';
export const revalidate = 86400; // Revalidate daily

// Dynamic Rendering
export const dynamic = 'force-dynamic';

// Incremental Static Regeneration
export const revalidate = 3600; // Revalidate hourly
```

## Related Agents

- **Frontend-Development-Agent**: Builds page components
- **Forms-Workflow-Agent**: Handles dynamic routing
- **Accessibility-Compliance-Agent**: Ensures content accessibility
- **Monitoring-Observability-Agent**: Tracks content performance

## SEO Best Practices Checklist

- [ ] Unique title tags (50-60 characters)
- [ ] Meta descriptions (150-160 characters)
- [ ] Open Graph tags for social sharing
- [ ] Structured data (JSON-LD) for rich snippets
- [ ] Canonical URLs to prevent duplicates
- [ ] Alt text for all images
- [ ] Internal linking between pages
- [ ] Mobile-friendly responsive design
- [ ] Fast page load times (< 3 seconds)
- [ ] HTTPS enabled
- [ ] XML sitemap generated and submitted
- [ ] Robots.txt properly configured
- [ ] 404 page with helpful navigation
- [ ] Clean, descriptive URLs
- [ ] Proper heading hierarchy (H1, H2, H3)

## Common Pitfalls

1. **Missing Meta Tags**: Always include title and description
2. **Duplicate Content**: Use canonical URLs
3. **Broken Links**: Regular audits for 404s
4. **Slow Load Times**: Optimize images and code
5. **Poor Mobile Experience**: Test on real devices

## Example Use Cases

### Blog Post with SEO
```tsx
export async function generateMetadata({ params }): Promise<Metadata> {
    const post = await getPost(params.slug);

    return {
        title: post.title,
        description: post.excerpt,
        openGraph: {
            type: 'article',
            publishedTime: post.publishedAt,
            authors: [post.author]
        }
    };
}
```

### Product Page with Schema
```tsx
export function ProductSchema({ product }) {
    const schema = {
        '@context': 'https://schema.org',
        '@type': 'Product',
        name: product.name,
        description: product.description,
        image: product.image,
        offers: {
            '@type': 'Offer',
            price: product.price,
            priceCurrency: 'USD'
        }
    };

    return (
        <script
            type="application/ld+json"
            dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
        />
    );
}
```

## Reference Resources

- [Next.js SEO Guide](https://nextjs.org/learn/seo/introduction-to-seo)
- [Google Search Central](https://developers.google.com/search)
- [Schema.org](https://schema.org)
- [Open Graph Protocol](https://ogp.me)
- [Web Content Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
