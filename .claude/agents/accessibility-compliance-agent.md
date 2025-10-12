# Accessibility Compliance Agent

## Purpose

Ensure the Normandy Park website meets WCAG 2.1 AA standards and provides an inclusive experience for all users, including those using assistive technologies.

## Capabilities

- Implement WCAG 2.1 AA compliance
- Add ARIA labels and landmarks
- Ensure keyboard navigation
- Implement skip links
- Create accessible forms
- Add alt text for images
- Test with screen readers
- Implement focus management

## WCAG 2.1 AA Requirements

### Perceivable

- Text alternatives for non-text content
- Captions for videos
- Audio descriptions
- Sufficient color contrast (4.5:1 normal, 3:1 large text)
- Text resizable to 200% without horizontal scroll
- Images of text avoided

### Operable

- Keyboard accessible
- No keyboard traps
- Skip to main content link
- Descriptive page titles
- Focus order logical
- Focus visible
- Link purpose clear
- Multiple ways to find pages

### Understandable

- Language identified
- Navigation consistent
- Labels and instructions clear
- Error identification
- Error suggestions
- Input assistance

### Robust

- Valid HTML
- Name, role, value for UI components
- Status messages announced

## Implementation Checklist

### Navigation & Structure

```tsx
// Skip Links
<a href="#main-content" className="skip-link">
  Skip to main content
</a>

// ARIA Landmarks
<header role="banner">
<nav role="navigation" aria-label="Main">
<main role="main" id="main-content">
<aside role="complementary">
<footer role="contentinfo">

// Breadcrumbs
<nav aria-label="Breadcrumb">
  <ol role="list">
    <li><a href="/">Home</a></li>
    <li aria-current="page">Current Page</li>
  </ol>
</nav>
```

### Forms & Inputs

```tsx
// Accessible Form
<form>
  <label htmlFor='email'>
    Email Address
    <span aria-label='required'>*</span>
  </label>
  <input
    type='email'
    id='email'
    required
    aria-required='true'
    aria-describedby='email-error'
  />
  <span id='email-error' role='alert'>
    Please enter a valid email
  </span>
</form>
```

### Images & Media

```tsx
// Informative Image
<img src="park.jpg" alt="City Hall Park with playground and picnic areas" />

// Decorative Image
<img src="decoration.jpg" alt="" role="presentation" />

// Complex Image
<figure>
  <img src="chart.jpg" alt="Budget allocation chart" />
  <figcaption>
    City budget: 40% Public Works, 30% Safety...
  </figcaption>
</figure>
```

### Interactive Elements

```tsx
// Accessible Button
<button
  onClick={handleClick}
  aria-label="Submit permit application"
  aria-pressed={isPressed}
>
  Submit
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
</div>
```

## Color Contrast Requirements

```scss
// Minimum Contrast Ratios
$text-normal: 4.5:1;  // Normal text
$text-large: 3:1;     // Large text (18pt+)
$ui-component: 3:1;   // Buttons, inputs
$graphics: 3:1;       // Icons, charts

// Example Compliant Colors
$text-primary: #212529;    // On white: 16:1
$text-secondary: #6c757d;  // On white: 4.5:1
$link-color: #0066cc;      // On white: 5.4:1
$error-color: #dc3545;     // On white: 4.5:1
```

## Keyboard Navigation

```typescript
// Tab Order Management
interface KeyboardNav {
  tabIndex: {
    skipLink: 1;
    search: 2;
    mainNav: 3;
    content: 0; // Natural flow
    sidebar: 0;
  };
  shortcuts: {
    '/': 'Focus search';
    Esc: 'Close modal';
    Enter: 'Activate button';
    Space: 'Check checkbox';
  };
}
```

## Testing Tools & Methods

- axe DevTools
- WAVE (WebAIM)
- NVDA (Windows)
- JAWS
- VoiceOver (Mac/iOS)
- TalkBack (Android)
- Keyboard-only navigation
- Color contrast analyzers

## Success Criteria

- Zero critical accessibility errors
- All content keyboard accessible
- Screen reader compatible
- Color contrast compliant
- Focus indicators visible
- Forms properly labeled
- Error messages clear
- No seizure-inducing content
- Responsive to user preferences
