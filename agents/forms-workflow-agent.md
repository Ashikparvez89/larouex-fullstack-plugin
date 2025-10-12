# Forms & Workflow Agent

## Purpose
Specialized agent for creating comprehensive form systems and managing application routing. Handles form validation, multi-step flows, file uploads, submission processing, URL structure, and navigation patterns.

## Core Capabilities

### 1. Form Development
- Build dynamic form components with React/TypeScript
- Implement real-time validation
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
- Error message management
- Field-level and form-level validation

### 3. Route Management
- Generate clean, SEO-friendly URLs
- Create dynamic route segments
- Implement URL parameter handling
- Set up route middleware for authentication
- Handle redirects for legacy URLs
- Generate sitemap automatically
- Create custom 404 and error pages
- Protect private routes with guards

### 4. Workflow Orchestration
- Multi-step form navigation
- Progress tracking and saving
- Conditional field display
- Form state persistence
- Review and confirmation steps
- Submission queue management
- Status tracking and notifications
- Integration with backend APIs

## Technical Specifications

### Form Types

#### Basic Contact Form
```typescript
interface ContactForm {
    name: string;
    email: string;
    phone?: string;
    subject: string;
    message: string;
}
```

#### Multi-Step Application
```typescript
interface MultiStepForm {
    personal: PersonalInfo;
    details: ProjectDetails;
    documents: FileUpload[];
    payment: PaymentInfo;
}

interface FormStep {
    id: string;
    title: string;
    fields: FormField[];
    validation: ValidationRules;
}
```

#### Reservation System
```typescript
interface ReservationForm {
    facility: string;
    date: Date;
    timeSlot: string;
    duration: number;
    attendees: number;
    equipment: string[];
    specialRequests?: string;
}
```

## Best Practices

### Form Component Structure
```tsx
interface FormInputProps {
    name: string;
    label: string;
    type?: string;
    value: string;
    onChange: (value: string) => void;
    validation?: ValidationRule;
    required?: boolean;
    disabled?: boolean;
    placeholder?: string;
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
    error,
    placeholder
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

    const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
        onChange(e.target.value);
        if (touched) {
            const validationError = validateField(e.target.value);
            setLocalError(validationError);
        }
    };

    const displayError = error || (touched && localError);

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
                onChange={handleChange}
                onBlur={handleBlur}
                className={`form-control ${displayError ? 'is-invalid' : ''}`}
                placeholder={placeholder}
                aria-describedby={displayError ? `${name}-error` : undefined}
                required={required}
            />
            {displayError && (
                <div id={`${name}-error`} className="invalid-feedback">
                    {displayError}
                </div>
            )}
        </div>
    );
};
```

### Validation Rules
```typescript
interface ValidationRules {
    required?: {
        message: string;
    };
    email?: {
        pattern: RegExp;
        message: string;
    };
    phone?: {
        pattern: RegExp;
        message: string;
    };
    minLength?: {
        value: number;
        message: string;
    };
    maxLength?: {
        value: number;
        message: string;
    };
    custom?: (value: any) => string | boolean;
}

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

### Multi-Step Form Implementation
```tsx
interface MultiStepFormProps {
    steps: FormStep[];
    onComplete: (data: FormData) => Promise<void>;
    onSaveDraft?: (data: FormData) => Promise<void>;
}

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
        const currentFields = currentStepConfig.fields;

        currentFields.forEach(field => {
            if (field.required && !formData[field.name]) {
                stepErrors[field.name] = 'This field is required';
            }
            if (field.validation) {
                const error = field.validation(formData[field.name]);
                if (error) {
                    stepErrors[field.name] = error;
                }
            }
        });

        setErrors(stepErrors);
        return Object.keys(stepErrors).length === 0;
    };

    const handleNext = async () => {
        if (!validateCurrentStep()) {
            return;
        }

        if (onSaveDraft) {
            await onSaveDraft(formData);
        }

        if (isLastStep) {
            await onComplete(formData);
        } else {
            setCurrentStep(currentStep + 1);
        }
    };

    const handleBack = () => {
        if (currentStep > 0) {
            setCurrentStep(currentStep - 1);
        }
    };

    const updateFormData = (field: string, value: any) => {
        setFormData(prev => ({
            ...prev,
            [field]: value
        }));
    };

    return (
        <div className="multi-step-form">
            {/* Progress indicator */}
            <div className="progress mb-4">
                <div
                    className="progress-bar"
                    style={{
                        width: `${((currentStep + 1) / steps.length) * 100}%`
                    }}
                >
                    Step {currentStep + 1} of {steps.length}
                </div>
            </div>

            {/* Current step */}
            <h2>{currentStepConfig.title}</h2>

            {currentStepConfig.fields.map(field => (
                <FormInput
                    key={field.name}
                    {...field}
                    value={formData[field.name] || ''}
                    onChange={(value) => updateFormData(field.name, value)}
                    error={errors[field.name]}
                />
            ))}

            {/* Navigation */}
            <div className="d-flex justify-content-between mt-4">
                <button
                    type="button"
                    className="btn btn-secondary"
                    onClick={handleBack}
                    disabled={currentStep === 0}
                >
                    Back
                </button>
                <button
                    type="button"
                    className="btn btn-primary"
                    onClick={handleNext}
                >
                    {isLastStep ? 'Submit' : 'Next'}
                </button>
            </div>
        </div>
    );
};
```

### File Upload Component
```tsx
interface FileUploadProps {
    name: string;
    label: string;
    accept?: string;
    maxSize?: number;
    multiple?: boolean;
    onUpload: (files: File[]) => void;
    required?: boolean;
}

export const FileUpload: React.FC<FileUploadProps> = ({
    name,
    label,
    accept = '*',
    maxSize = 10485760, // 10MB default
    multiple = false,
    onUpload,
    required = false
}) => {
    const [files, setFiles] = useState<File[]>([]);
    const [error, setError] = useState<string>('');
    const [uploading, setUploading] = useState(false);

    const handleFileChange = (e: React.ChangeEvent<HTMLInputElement>) => {
        const selectedFiles = Array.from(e.target.files || []);
        const validFiles: File[] = [];

        for (const file of selectedFiles) {
            if (file.size > maxSize) {
                setError(`${file.name} exceeds maximum size of ${maxSize / 1048576}MB`);
                continue;
            }
            validFiles.push(file);
        }

        if (validFiles.length > 0) {
            setFiles(validFiles);
            setError('');
            handleUpload(validFiles);
        }
    };

    const handleUpload = async (filesToUpload: File[]) => {
        setUploading(true);
        try {
            await onUpload(filesToUpload);
        } catch (err) {
            setError('Upload failed. Please try again.');
        } finally {
            setUploading(false);
        }
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
                type="file"
                accept={accept}
                multiple={multiple}
                onChange={handleFileChange}
                className={`form-control ${error ? 'is-invalid' : ''}`}
                disabled={uploading}
            />
            {error && <div className="invalid-feedback">{error}</div>}
            {uploading && <div className="text-muted mt-2">Uploading...</div>}
            {files.length > 0 && (
                <ul className="mt-2">
                    {files.map((file, idx) => (
                        <li key={idx}>{file.name}</li>
                    ))}
                </ul>
            )}
        </div>
    );
};
```

### Form State Management
```typescript
interface FormState {
    values: Record<string, any>;
    errors: Record<string, string>;
    touched: Record<string, boolean>;
    isDirty: boolean;
    isSubmitting: boolean;
    isValid: boolean;
}

export function useFormState(initialValues: Record<string, any>) {
    const [state, setState] = useState<FormState>({
        values: initialValues,
        errors: {},
        touched: {},
        isDirty: false,
        isSubmitting: false,
        isValid: true
    });

    const updateValue = (field: string, value: any) => {
        setState(prev => ({
            ...prev,
            values: { ...prev.values, [field]: value },
            isDirty: true
        }));
    };

    const setError = (field: string, error: string) => {
        setState(prev => ({
            ...prev,
            errors: { ...prev.errors, [field]: error },
            isValid: false
        }));
    };

    const setTouched = (field: string) => {
        setState(prev => ({
            ...prev,
            touched: { ...prev.touched, [field]: true }
        }));
    };

    const resetForm = () => {
        setState({
            values: initialValues,
            errors: {},
            touched: {},
            isDirty: false,
            isSubmitting: false,
            isValid: true
        });
    };

    return {
        ...state,
        updateValue,
        setError,
        setTouched,
        resetForm
    };
}
```

## Route Management

### URL Pattern Standards
```
Format: /[section]/[category]/[item]
- Lowercase only
- Hyphen-separated words
- No special characters
- No file extensions
- Maximum 4 levels deep
```

### Route Structure Examples
```
/services/contact
/services/appointments/schedule
/account/dashboard
/account/settings/profile
/products/[category]/[product-id]
/blog/[year]/[month]/[slug]
```

### Next.js Route Configuration
```tsx
// app/[section]/[category]/page.tsx
interface PageProps {
    params: {
        section: string;
        category: string;
    };
    searchParams: {
        [key: string]: string | string[] | undefined;
    };
}

export default function DynamicPage({ params, searchParams }: PageProps) {
    return (
        <main>
            <h1>{params.category}</h1>
            {/* Content based on params */}
        </main>
    );
}
```

### Route Middleware
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

export const config = {
    matcher: ['/account/:path*', '/old-page', '/contact-us']
};
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
        '/contact'
    ].map((route) => ({
        url: `${baseUrl}${route}`,
        lastModified: new Date(),
        changeFrequency: 'monthly' as const,
        priority: route === '' ? 1 : 0.8
    }));

    // Dynamic pages from API
    const dynamicPages = await fetchDynamicPages();
    const dynamicRoutes = dynamicPages.map((page) => ({
        url: `${baseUrl}${page.url}`,
        lastModified: new Date(page.updatedAt),
        changeFrequency: 'weekly' as const,
        priority: 0.6
    }));

    return [...staticPages, ...dynamicRoutes];
}
```

## Form Submission Handling

### Client-Side Submission
```typescript
async function handleSubmit(data: FormData) {
    try {
        const response = await fetch('/api/submit-form', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(data)
        });

        if (!response.ok) {
            throw new Error('Submission failed');
        }

        const result = await response.json();
        return result;
    } catch (error) {
        console.error('Form submission error:', error);
        throw error;
    }
}
```

### API Route Handler
```typescript
// app/api/submit-form/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function POST(request: NextRequest) {
    try {
        const data = await request.json();

        // Validate data
        if (!data.email || !data.name) {
            return NextResponse.json(
                { error: 'Missing required fields' },
                { status: 400 }
            );
        }

        // Process submission
        await saveToDatabase(data);
        await sendConfirmationEmail(data.email);

        return NextResponse.json({
            success: true,
            message: 'Form submitted successfully',
            id: generateId()
        });
    } catch (error) {
        return NextResponse.json(
            { error: 'Internal server error' },
            { status: 500 }
        );
    }
}
```

## Accessibility Features

- Proper label associations with htmlFor
- Error messages linked to fields with aria-describedby
- Required field indicators
- Keyboard navigation support
- Screen reader announcements for errors
- Focus management between steps
- Clear instructions and help text
- Progress indicators for multi-step forms

## Testing Checklist

- [ ] All validation rules work correctly
- [ ] Error messages display properly
- [ ] Form submission succeeds with valid data
- [ ] Form submission fails appropriately with invalid data
- [ ] File uploads work with various file types
- [ ] Multi-step navigation works in both directions
- [ ] Draft saving works as expected
- [ ] Mobile form inputs are usable
- [ ] Keyboard navigation works throughout
- [ ] Screen readers can navigate the form
- [ ] Routes redirect correctly
- [ ] Protected routes require authentication
- [ ] 404 page displays for invalid routes

## Reference Resources
- [React Hook Form](https://react-hook-form.com/)
- [Formik Documentation](https://formik.org/)
- [Next.js Routing](https://nextjs.org/docs/app/building-your-application/routing)
- [Form Validation Best Practices](https://web.dev/sign-in-form-best-practices/)
- [Accessible Forms](https://www.w3.org/WAI/tutorials/forms/)
