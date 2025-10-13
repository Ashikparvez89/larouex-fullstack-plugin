# Forms & Workflow Agent

## Overview

The Forms & Workflow Agent specializes in creating comprehensive form systems, managing application routing, and orchestrating multi-step workflows. It handles form validation, file uploads, submission processing, URL structure, and navigation patterns.

**Primary Focus:**
- Dynamic form components with React/TypeScript
- Real-time client and server-side validation
- Multi-step form workflows with progress tracking
- File upload handling with progress indicators
- Route management and URL structure
- Form state persistence and auto-save

## Core Capabilities

### 1. Form Development
- Build dynamic form components with real-time validation
- Handle file uploads with progress tracking
- Create multi-step form workflows
- Process form submissions with error handling
- Generate confirmation messages
- Implement draft auto-save functionality
- Integrate payment processing

### 2. Form Validation
- Client-side validation with immediate feedback
- Server-side validation for security
- Pattern matching for emails, phones, zip codes
- Custom validation rules
- Cross-field validation
- Async validation for API checks
- Field-level and form-level validation

### 3. Route Management
- Generate clean, SEO-friendly URLs
- Create dynamic route segments
- Implement URL parameter handling
- Set up route middleware for authentication
- Handle redirects for legacy URLs
- Generate sitemap automatically
- Protect private routes with guards

### 4. Workflow Orchestration
- Multi-step form navigation
- Progress tracking and saving
- Conditional field display
- Form state persistence
- Review and confirmation steps
- Submission queue management
- Status tracking and notifications

## Common Commands

Commands that frequently use this agent:

- `/add-form` - Create form with validation
- `/add-form-multi-step` - Multi-step form workflow
- `/add-file-upload` - File upload handling
- `/add-search` - Search functionality
- `/setup-environment` - Route configuration

## Key Implementation Patterns

### Form Component with Validation

```tsx
interface FormInputProps {
    name: string;
    label: string;
    type?: string;
    value: string;
    onChange: (value: string) => void;
    validation?: ValidationRule;
    required?: boolean;
    error?: string;
}

export const FormInput: React.FC<FormInputProps> = ({
    name,
    label,
    type = 'text',
    value,
    onChange,
    validation,
    required = false,
    error
}) => {
    const [touched, setTouched] = useState(false);
    const [localError, setLocalError] = useState<string>('');

    const validateField = (val: string) => {
        if (required && !val.trim()) {
            return 'This field is required';
        }
        if (validation) {
            return validation(val);
        }
        return '';
    };

    const handleBlur = () => {
        setTouched(true);
        const validationError = validateField(value);
        setLocalError(validationError);
    };

    return (
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
                onChange={(e) => onChange(e.target.value)}
                onBlur={handleBlur}
                className={`form-control ${error || (touched && localError) ? 'is-invalid' : ''}`}
                required={required}
            />
            {(error || (touched && localError)) && (
                <div className="invalid-feedback">
                    {error || localError}
                </div>
            )}
        </div>
    );
};
```

### Multi-Step Form Implementation

```tsx
export const MultiStepForm: React.FC<MultiStepFormProps> = ({
    steps,
    onComplete,
    onSaveDraft
}) => {
    const [currentStep, setCurrentStep] = useState(0);
    const [formData, setFormData] = useState<Record<string, any>>({});
    const [errors, setErrors] = useState<Record<string, string>>({});

    const isLastStep = currentStep === steps.length - 1;
    const currentStepConfig = steps[currentStep];

    const validateCurrentStep = (): boolean => {
        const stepErrors: Record<string, string> = {};
        currentStepConfig.fields.forEach(field => {
            if (field.required && !formData[field.name]) {
                stepErrors[field.name] = 'This field is required';
            }
        });
        setErrors(stepErrors);
        return Object.keys(stepErrors).length === 0;
    };

    const handleNext = async () => {
        if (!validateCurrentStep()) return;

        if (onSaveDraft) {
            await onSaveDraft(formData);
        }

        if (isLastStep) {
            await onComplete(formData);
        } else {
            setCurrentStep(currentStep + 1);
        }
    };

    return (
        <div className="multi-step-form">
            <div className="progress mb-4">
                <div
                    className="progress-bar"
                    style={{ width: `${((currentStep + 1) / steps.length) * 100}%` }}
                >
                    Step {currentStep + 1} of {steps.length}
                </div>
            </div>

            <h2>{currentStepConfig.title}</h2>
            {/* Render fields */}

            <div className="d-flex justify-content-between mt-4">
                <button
                    type="button"
                    onClick={() => setCurrentStep(currentStep - 1)}
                    disabled={currentStep === 0}
                >
                    Back
                </button>
                <button type="button" onClick={handleNext}>
                    {isLastStep ? 'Submit' : 'Next'}
                </button>
            </div>
        </div>
    );
};
```

### Common Validation Rules

```typescript
export const commonValidations = {
    email: {
        pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
        message: "Please enter a valid email address"
    },
    phone: {
        pattern: /^\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$/,
        message: "Please enter a valid phone number"
    },
    zip: {
        pattern: /^\d{5}(-\d{4})?$/,
        message: "Please enter a valid ZIP code"
    },
    url: {
        pattern: /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/,
        message: "Please enter a valid URL"
    }
};
```

### File Upload Component

```tsx
export const FileUpload: React.FC<FileUploadProps> = ({
    name,
    label,
    accept = '*',
    maxSize = 10485760, // 10MB
    multiple = false,
    onUpload
}) => {
    const [files, setFiles] = useState<File[]>([]);
    const [error, setError] = useState<string>('');
    const [uploading, setUploading] = useState(false);

    const handleFileChange = (e: React.ChangeEvent<HTMLInputElement>) => {
        const selectedFiles = Array.from(e.target.files || []);
        const validFiles: File[] = [];

        for (const file of selectedFiles) {
            if (file.size > maxSize) {
                setError(`${file.name} exceeds maximum size`);
                continue;
            }
            validFiles.push(file);
        }

        if (validFiles.length > 0) {
            setFiles(validFiles);
            handleUpload(validFiles);
        }
    };

    return (
        <div className="mb-3">
            <label htmlFor={name}>{label}</label>
            <input
                id={name}
                type="file"
                accept={accept}
                multiple={multiple}
                onChange={handleFileChange}
                disabled={uploading}
            />
            {error && <div className="text-danger">{error}</div>}
            {uploading && <div>Uploading...</div>}
        </div>
    );
};
```

### Route Middleware (Next.js)

```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
    // Protected routes
    if (request.nextUrl.pathname.startsWith('/account')) {
        const token = request.cookies.get('auth-token');
        if (!token) {
            return NextResponse.redirect(new URL('/login', request.url));
        }
    }

    // Legacy redirects
    const redirects: Record<string, string> = {
        '/old-page': '/new-page',
        '/contact-us': '/services/contact'
    };

    const redirect = redirects[request.nextUrl.pathname];
    if (redirect) {
        return NextResponse.redirect(new URL(redirect, request.url), 301);
    }

    return NextResponse.next();
}
```

## Platform-Specific Details

### Next.js App Router
- Uses App Router for routing
- Dynamic segments with [slug]
- Route groups with (folder)
- Parallel routes and intercepting routes
- Middleware for authentication

### Form State Management
- React hooks (useState, useReducer)
- Context API for global state
- Session storage for persistence
- Custom hooks for reusable logic

## Related Agents

- **Frontend-Development-Agent**: Builds UI components
- **Azure-Serverless-Agent**: Creates form submission API endpoints (Azure)
- **DevOps-Railway-Agent**: Creates API endpoints (Railway)
- **Testing-Quality-Agent**: Tests form validation and workflows

## Best Practices Checklist

- [ ] Validate on both client and server
- [ ] Provide clear error messages
- [ ] Show field-level validation feedback
- [ ] Implement proper focus management
- [ ] Support keyboard navigation
- [ ] Add loading states for async operations
- [ ] Implement auto-save for long forms
- [ ] Test with screen readers
- [ ] Handle network failures gracefully
- [ ] Sanitize user input

## Common Pitfalls

1. **Client-Only Validation**: Always validate on server
2. **Poor Error Messages**: Be specific about what's wrong
3. **Missing Loading States**: Show progress indicators
4. **No Auto-Save**: Implement for long forms
5. **Accessibility Issues**: Test with keyboard and screen readers

## Example Use Cases

### Contact Form
```tsx
<ContactForm
    onSubmit={async (data) => {
        await fetch('/api/contact', {
            method: 'POST',
            body: JSON.stringify(data)
        });
    }}
/>
```

### Multi-Step Application
```tsx
<MultiStepForm
    steps={[
        { id: 'personal', title: 'Personal Info', fields: [...] },
        { id: 'details', title: 'Project Details', fields: [...] },
        { id: 'review', title: 'Review', fields: [...] }
    ]}
    onComplete={handleSubmit}
    onSaveDraft={saveDraft}
/>
```

## Reference Resources

- [React Hook Form](https://react-hook-form.com/)
- [Formik Documentation](https://formik.org/)
- [Next.js Routing](https://nextjs.org/docs/app/building-your-application/routing)
- [Form Validation Best Practices](https://web.dev/sign-in-form-best-practices/)
- [Accessible Forms](https://www.w3.org/WAI/tutorials/forms/)
