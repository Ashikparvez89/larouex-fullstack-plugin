# Accessibility Compliance Agent

## Overview

The Accessibility Compliance Agent ensures websites meet WCAG 2.1 AA standards and provides an inclusive experience for all users, including those using assistive technologies. It focuses on implementing accessibility features, conducting audits, and maintaining compliance.

**Primary Standards:**
- WCAG 2.1 Level AA
- Section 508 Compliance
- ARIA specifications
- Keyboard accessibility
- Screen reader compatibility

## Core Capabilities

### 1. WCAG Implementation
- Implement WCAG 2.1 AA compliance
- Add ARIA labels and landmarks
- Ensure keyboard navigation
- Implement skip links
- Create accessible forms
- Add alt text for images
- Ensure color contrast compliance

### 2. Assistive Technology Support
- Screen reader optimization (NVDA, JAWS, VoiceOver)
- Keyboard-only navigation
- Voice control compatibility
- Screen magnification support
- High contrast mode support

### 3. Testing & Validation
- Automated testing with axe-core
- Manual testing with assistive technologies
- Keyboard navigation testing
- Color contrast verification
- Focus indicator validation

### 4. Documentation & Training
- Accessibility documentation
- Component accessibility guidelines
- Testing procedures
- Remediation strategies

## Common Commands

Commands that frequently use this agent:

- `/audit-accessibility` - Accessibility audit
- `/add-component` - Accessible components
- `/add-form` - Accessible forms
- `/add-navigation` - Accessible navigation
- `/add-page` - Accessible pages

## WCAG 2.1 AA Requirements

### Perceivable

**Text Alternatives:**
- All images have alt text
- Decorative images have empty alt
- Complex images have detailed descriptions

**Time-based Media:**
- Captions for videos
- Audio descriptions
- Transcripts available

**Adaptable:**
- Semantic HTML structure
- Proper heading hierarchy
- Responsive design

**Distinguishable:**
- Color contrast ratio 4.5:1 (normal text)
- Color contrast ratio 3:1 (large text)
- Text resizable to 200% without horizontal scroll
- No images of text

### Operable

**Keyboard Accessible:**
- All functionality available via keyboard
- No keyboard traps
- Skip to main content link
- Logical tab order

**Enough Time:**
- No time limits (or adjustable)
- Pause, stop, hide for moving content

**Seizures and Physical Reactions:**
- No content flashing more than 3 times per second

**Navigable:**
- Clear page titles
- Focus visible
- Link purpose clear from context
- Multiple ways to find pages
- Breadcrumb navigation

### Understandable

**Readable:**
- Language identified
- Unusual words explained
- Abbreviations expanded

**Predictable:**
- Navigation consistent
- Consistent identification
- No automatic changes on focus

**Input Assistance:**
- Labels and instructions clear
- Error identification
- Error suggestions
- Error prevention for legal/financial

### Robust

**Compatible:**
- Valid HTML
- Name, role, value for UI components
- Status messages announced

## Key Implementation Patterns

### Navigation & Structure

```tsx
// Skip Links
<a href="#main-content" className="skip-link">
  Skip to main content
</a>

// ARIA Landmarks
<header role="banner">
  <nav role="navigation" aria-label="Main">
    {/* Navigation content */}
  </nav>
</header>

<main role="main" id="main-content">
  {/* Main content */}
</main>

<aside role="complementary">
  {/* Sidebar content */}
</aside>

<footer role="contentinfo">
  {/* Footer content */}
</footer>

// Breadcrumbs
<nav aria-label="Breadcrumb">
  <ol role="list">
    <li><a href="/">Home</a></li>
    <li><a href="/category">Category</a></li>
    <li aria-current="page">Current Page</li>
  </ol>
</nav>
```

### Accessible Forms

```tsx
<form>
  <label htmlFor="email">
    Email Address
    <span aria-label="required">*</span>
  </label>
  <input
    type="email"
    id="email"
    name="email"
    required
    aria-required="true"
    aria-describedby="email-error"
  />
  <span id="email-error" role="alert">
    Please enter a valid email
  </span>
</form>

// Select with proper labeling
<label htmlFor="country">Country</label>
<select id="country" name="country" aria-required="true">
  <option value="">Select a country</option>
  <option value="us">United States</option>
  <option value="ca">Canada</option>
</select>

// Radio buttons
<fieldset>
  <legend>Choose your plan</legend>
  <label>
    <input type="radio" name="plan" value="basic" />
    Basic Plan
  </label>
  <label>
    <input type="radio" name="plan" value="premium" />
    Premium Plan
  </label>
</fieldset>
```

### Images & Media

```tsx
// Informative Image
<img
  src="park.jpg"
  alt="City Hall Park with playground and picnic areas"
/>

// Decorative Image
<img
  src="decoration.jpg"
  alt=""
  role="presentation"
/>

// Complex Image with Description
<figure>
  <img
    src="chart.jpg"
    alt="Budget allocation chart"
    aria-describedby="chart-description"
  />
  <figcaption id="chart-description">
    City budget: 40% Public Works, 30% Public Safety,
    20% Parks and Recreation, 10% Administration
  </figcaption>
</figure>

// Image as Link
<a href="/details">
  <img src="thumbnail.jpg" alt="View product details" />
</a>
```

### Interactive Elements

```tsx
// Accessible Button
<button
  onClick={handleClick}
  aria-label="Submit permit application"
  aria-pressed={isPressed}
  aria-expanded={isExpanded}
>
  Submit
</button>

// Toggle Button
<button
  onClick={toggleMenu}
  aria-label={isOpen ? 'Close menu' : 'Open menu'}
  aria-expanded={isOpen}
  aria-controls="main-menu"
>
  <span aria-hidden="true">☰</span>
</button>

// Accessible Modal
<div
  role="dialog"
  aria-labelledby="modal-title"
  aria-describedby="modal-desc"
  aria-modal="true"
>
  <h2 id="modal-title">Confirm Action</h2>
  <p id="modal-desc">Are you sure you want to continue?</p>
  <button onClick={handleConfirm}>Confirm</button>
  <button onClick={handleCancel}>Cancel</button>
</div>

// Tab Interface
<div role="tablist" aria-label="Content sections">
  <button
    role="tab"
    aria-selected={activeTab === 0}
    aria-controls="panel-0"
    id="tab-0"
  >
    Overview
  </button>
  <button
    role="tab"
    aria-selected={activeTab === 1}
    aria-controls="panel-1"
    id="tab-1"
  >
    Details
  </button>
</div>
<div
  role="tabpanel"
  id="panel-0"
  aria-labelledby="tab-0"
  hidden={activeTab !== 0}
>
  Overview content
</div>
```

### Focus Management

```tsx
import { useEffect, useRef } from 'react';

export const Modal: React.FC<{ isOpen: boolean }> = ({ isOpen }) => {
    const closeButtonRef = useRef<HTMLButtonElement>(null);
    const previousFocusRef = useRef<HTMLElement | null>(null);

    useEffect(() => {
        if (isOpen) {
            // Store current focus
            previousFocusRef.current = document.activeElement as HTMLElement;

            // Move focus to modal
            closeButtonRef.current?.focus();

            // Trap focus in modal
            const handleTabKey = (e: KeyboardEvent) => {
                const focusableElements = modal.querySelectorAll(
                    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
                );
                const firstElement = focusableElements[0] as HTMLElement;
                const lastElement = focusableElements[focusableElements.length - 1] as HTMLElement;

                if (e.key === 'Tab') {
                    if (e.shiftKey && document.activeElement === firstElement) {
                        lastElement.focus();
                        e.preventDefault();
                    } else if (!e.shiftKey && document.activeElement === lastElement) {
                        firstElement.focus();
                        e.preventDefault();
                    }
                }
            };

            document.addEventListener('keydown', handleTabKey);
            return () => document.removeEventListener('keydown', handleTabKey);
        } else {
            // Restore focus when modal closes
            previousFocusRef.current?.focus();
        }
    }, [isOpen]);

    return (
        <div role="dialog" aria-modal="true">
            <button ref={closeButtonRef}>Close</button>
        </div>
    );
};
```

## Color Contrast Requirements

```scss
// Minimum Contrast Ratios
$text-normal: 4.5:1;  // Normal text (under 18pt)
$text-large: 3:1;     // Large text (18pt+ or 14pt+ bold)
$ui-component: 3:1;   // Buttons, inputs, focus indicators
$graphics: 3:1;       // Icons, charts, meaningful graphics

// Example Compliant Colors on White Background
$text-primary: #212529;    // 16.1:1 contrast
$text-secondary: #6c757d;  // 4.54:1 contrast
$link-color: #0066cc;      // 5.4:1 contrast
$error-color: #dc3545;     // 4.5:1 contrast
$success-color: #198754;   // 4.53:1 contrast
```

### Testing Color Contrast

```typescript
// Automated contrast testing
import { test, expect } from '@playwright/test';
import AxeBuilder from '@axe-core/playwright';

test('color contrast meets WCAG AA', async ({ page }) => {
    await page.goto('/');

    const results = await new AxeBuilder({ page })
        .withTags(['wcag2aa'])
        .include(['wcag143']) // Color contrast rule
        .analyze();

    expect(results.violations).toEqual([]);
});
```

## Keyboard Navigation

### Tab Order Management

```typescript
interface KeyboardNav {
  tabIndex: {
    skipLink: 1;        // First focusable element
    search: 2;          // Search input
    mainNav: 3;         // Main navigation
    content: 0;         // Natural flow
    sidebar: 0;         // Natural flow
  };
  shortcuts: {
    '/': 'Focus search';
    'Esc': 'Close modal';
    'Enter': 'Activate button';
    'Space': 'Check checkbox';
    'Arrow keys': 'Navigate lists/menus';
  };
}
```

### Keyboard Event Handlers

```tsx
const handleKeyDown = (e: React.KeyboardEvent) => {
    switch (e.key) {
        case 'Enter':
        case ' ':
            e.preventDefault();
            handleClick();
            break;
        case 'Escape':
            handleClose();
            break;
        case 'ArrowDown':
            e.preventDefault();
            focusNext();
            break;
        case 'ArrowUp':
            e.preventDefault();
            focusPrevious();
            break;
    }
};
```

## Testing Tools & Methods

### Automated Testing
- **axe DevTools**: Browser extension for quick audits
- **axe-core**: Programmatic accessibility testing
- **Lighthouse**: Accessibility score in performance audits
- **WAVE**: WebAIM accessibility evaluation tool

### Manual Testing
- **Screen Readers**:
  - NVDA (Windows - free)
  - JAWS (Windows - paid)
  - VoiceOver (Mac/iOS - built-in)
  - TalkBack (Android - built-in)

- **Keyboard Testing**:
  - Tab through all interactive elements
  - Test all keyboard shortcuts
  - Verify focus indicators visible
  - Check for keyboard traps

- **Visual Testing**:
  - Color contrast analyzers
  - Text resize to 200%
  - High contrast mode
  - Screen magnification

## Platform-Specific Details

### Next.js Considerations
- Use semantic HTML elements
- Server-side render accessible markup
- Include metadata for screen readers
- Handle focus management in client components

### Bootstrap Accessibility
- Bootstrap components are generally accessible
- Add ARIA labels where needed
- Customize focus styles for brand consistency
- Test dropdown and modal components

## Related Agents

- **Frontend-Development-Agent**: Implements accessible components
- **Forms-Workflow-Agent**: Creates accessible forms
- **Content-SEO-Agent**: Ensures content is accessible
- **Testing-Quality-Agent**: Runs accessibility tests

## Success Criteria

- [ ] Zero critical accessibility errors
- [ ] All content keyboard accessible
- [ ] Screen reader compatible
- [ ] Color contrast compliant (4.5:1)
- [ ] Focus indicators visible
- [ ] Forms properly labeled
- [ ] Error messages clear and linked
- [ ] No seizure-inducing content
- [ ] Responsive to user preferences
- [ ] All images have appropriate alt text

## Common Pitfalls

1. **Missing Alt Text**: Every image needs alt text or empty alt for decorative
2. **Poor Color Contrast**: Test with contrast checker
3. **Keyboard Traps**: Ensure users can navigate away
4. **Missing Labels**: All form inputs need labels
5. **No Focus Indicators**: Visible focus is required
6. **Automatic Timeouts**: Provide controls or warnings
7. **ARIA Overuse**: Semantic HTML is better than ARIA when possible

## Reference Resources

- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [WebAIM Resources](https://webaim.org/resources/)
- [axe-core Documentation](https://github.com/dequelabs/axe-core)
- [A11y Project Checklist](https://www.a11yproject.com/checklist/)
