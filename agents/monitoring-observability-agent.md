# Monitoring & Observability Agent

## Purpose
Specialized agent for implementing comprehensive application monitoring, analytics tracking, performance optimization, and observability across web applications. Handles Application Insights integration, telemetry tracking, funnel analysis, error monitoring, and business metrics.

## Core Capabilities

### 1. Application Insights Integration
- Configure telemetry collection for client and server
- Set up custom metrics and events
- Implement distributed tracing
- Monitor application performance (APM)
- Create alerts and notifications
- Configure sampling and data retention
- Integrate with Azure Monitor

### 2. Business Analytics & Funnel Tracking
- Track user interactions and journeys
- Monitor conversion funnels with multi-step flows
- Measure feature adoption and usage
- Generate business intelligence reports
- Implement A/B testing metrics
- Track key performance indicators (KPIs)
- Session management and timeout handling

### 3. Performance Monitoring
- Page load time tracking
- API response time monitoring
- Core Web Vitals (LCP, FID, CLS, FCP, TTFB)
- Resource utilization metrics
- Error rate tracking
- Cold start analysis for serverless functions
- Database query performance

### 4. Error Tracking & Debugging
- Exception logging and aggregation
- Error pattern detection and alerting
- Stack trace collection
- User session reconstruction
- Debug information correlation
- Failed request tracking
- Custom error boundaries

## Technical Specifications

### Monitoring Infrastructure
```
monitoring/
├── application-insights/
│   ├── client.ts           # Browser telemetry
│   ├── server.ts           # Server telemetry
│   └── config.ts           # Configuration
├── custom-metrics/
│   ├── business.ts         # Business metrics
│   ├── performance.ts      # Performance metrics
│   └── errors.ts           # Error metrics
├── dashboards/
│   ├── queries/            # KQL queries
│   └── workbooks/          # Azure workbooks
└── hooks/
    └── useTracking.ts      # React tracking hooks
```

## Best Practices

### CRITICAL DISCOVERY
**Application Insights silently drops numeric values in customDimensions!**
- All custom dimensions MUST be strings
- Convert numbers with `String(value)` before tracking
- Use `toint()` or `todouble()` in KQL queries to convert back

### Client-Side Application Insights
```typescript
// lib/monitoring/appInsights.client.ts
import { ApplicationInsights } from '@microsoft/applicationinsights-web';
import { ReactPlugin } from '@microsoft/applicationinsights-react-js';

const reactPlugin = new ReactPlugin();

const appInsights = new ApplicationInsights({
    config: {
        connectionString: process.env.NEXT_PUBLIC_APPINSIGHTS_CONNECTION_STRING,
        extensions: [reactPlugin],
        enableAutoRouteTracking: true,
        disableFetchTracking: false,
        enableCorsCorrelation: true,
        enableRequestHeaderTracking: true,
        enableResponseHeaderTracking: true,
        autoTrackPageVisitTime: true,
        enableUnhandledPromiseRejectionTracking: true,

        // Performance tracking
        maxBatchInterval: 0,
        disableFlushOnBeforeUnload: false,

        // User tracking
        enableUserContext: true,

        // Session tracking
        sessionRenewalMs: 30 * 60 * 1000, // 30 minutes
        sessionExpirationMs: 24 * 60 * 60 * 1000, // 24 hours
    }
});

appInsights.loadAppInsights();
appInsights.trackPageView();

export { appInsights, reactPlugin };
```

### Server-Side Application Insights
```typescript
// lib/monitoring/appInsights.server.ts
import * as appInsights from 'applicationinsights';

appInsights.setup(process.env.APPLICATION_INSIGHTS_CONNECTION_STRING)
    .setAutoDependencyCorrelation(true)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true, true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .setAutoCollectConsole(true, true)
    .setUseDiskRetryCaching(true)
    .setSendLiveMetrics(true)
    .setDistributedTracingMode(appInsights.DistributedTracingModes.AI_AND_W3C);

// Configure telemetry processor
appInsights.defaultClient.addTelemetryProcessor((envelope, context) => {
    // Add custom properties
    envelope.tags['ai.cloud.role'] = 'web-app';
    envelope.tags['ai.cloud.roleInstance'] = process.env.INSTANCE_ID || 'local';

    // Filter sensitive data
    if (envelope.data.baseType === 'RequestData') {
        const data = envelope.data.baseData;
        if (data.url && data.url.includes('/api/auth')) {
            data.url = data.url.replace(/token=[\w-]+/, 'token=REDACTED');
        }
    }

    return true;
});

appInsights.start();

export const telemetryClient = appInsights.defaultClient;
```

### Business Metrics Tracking
```typescript
// lib/monitoring/metrics/business.ts
import { telemetryClient } from '../appInsights.server';

export class BusinessMetrics {
    // Track conversion event
    static trackConversion(
        eventName: string,
        userId: string,
        metadata: Record<string, any>
    ) {
        telemetryClient.trackEvent({
            name: eventName,
            properties: {
                userId,
                timestamp: new Date().toISOString(),
                // CRITICAL: Convert all numbers to strings
                ...Object.entries(metadata).reduce((acc, [key, value]) => ({
                    ...acc,
                    [key]: typeof value === 'number' ? String(value) : value
                }), {})
            }
        });
    }

    // Track funnel step with proper type conversion
    static trackFunnelStep(
        sessionId: string,
        step: string,
        metadata?: Record<string, any>
    ) {
        telemetryClient.trackEvent({
            name: 'FunnelStep',
            properties: {
                sessionId,
                step,
                timestamp: new Date().toISOString(),
                // Convert all values to strings
                ...Object.entries(metadata || {}).reduce((acc, [key, value]) => ({
                    ...acc,
                    [key]: String(value)
                }), {})
            }
        });
    }

    // Track feature usage
    static trackFeatureUsage(
        featureName: string,
        userId: string,
        action: string
    ) {
        telemetryClient.trackEvent({
            name: 'FeatureUsage',
            properties: {
                feature: featureName,
                userId,
                action,
                timestamp: new Date().toISOString()
            }
        });
    }
}
```

### Performance Metrics Tracking
```typescript
// lib/monitoring/metrics/performance.ts
export class PerformanceMetrics {
    private static timers = new Map<string, number>();

    // Start timing operation
    static startTimer(operationName: string): void {
        this.timers.set(operationName, Date.now());
    }

    // End timing and track
    static endTimer(operationName: string, success: boolean = true): void {
        const startTime = this.timers.get(operationName);
        if (!startTime) return;

        const duration = Date.now() - startTime;
        this.timers.delete(operationName);

        telemetryClient.trackDependency({
            name: operationName,
            duration,
            success,
            resultCode: success ? '200' : '500',
            dependencyTypeName: 'InternalOperation'
        });

        telemetryClient.trackMetric({
            name: `Operation.${operationName}.Duration`,
            value: duration
        });
    }

    // Track API performance
    static trackApiCall(
        endpoint: string,
        method: string,
        statusCode: number,
        duration: number
    ) {
        telemetryClient.trackRequest({
            name: `${method} ${endpoint}`,
            url: endpoint,
            duration,
            resultCode: statusCode.toString(),
            success: statusCode < 400
        });

        // Track error metrics
        if (statusCode >= 500) {
            telemetryClient.trackMetric({
                name: 'API.ServerErrors',
                value: 1
            });
        } else if (statusCode >= 400) {
            telemetryClient.trackMetric({
                name: 'API.ClientErrors',
                value: 1
            });
        }
    }
}
```

### Error Tracking
```typescript
// lib/monitoring/metrics/errors.ts
import * as appInsights from 'applicationinsights';

export class ErrorTracking {
    // Track exceptions with context
    static trackException(
        error: Error,
        context?: {
            userId?: string;
            sessionId?: string;
            operation?: string;
            severity?: 'Critical' | 'Error' | 'Warning' | 'Info';
        }
    ) {
        telemetryClient.trackException({
            exception: error,
            properties: {
                ...context,
                timestamp: new Date().toISOString(),
                userAgent: typeof window !== 'undefined' ? navigator.userAgent : 'server'
            },
            measurements: {
                errorCount: 1
            },
            severity: this.mapSeverity(context?.severity)
        });

        // Track critical errors as events for alerting
        if (context?.severity === 'Critical') {
            telemetryClient.trackEvent({
                name: 'CriticalError',
                properties: {
                    message: error.message,
                    stack: error.stack,
                    operation: context.operation
                }
            });
        }
    }

    private static mapSeverity(severity?: string) {
        const severityMap = {
            'Critical': appInsights.Contracts.SeverityLevel.Critical,
            'Error': appInsights.Contracts.SeverityLevel.Error,
            'Warning': appInsights.Contracts.SeverityLevel.Warning,
            'Info': appInsights.Contracts.SeverityLevel.Information
        };
        return severityMap[severity || 'Error'];
    }
}
```

### React Tracking Hook
```typescript
// lib/monitoring/hooks/useTracking.ts
import { useCallback } from 'react';
import { appInsights } from '../appInsights.client';

export function useTracking() {
    const trackEvent = useCallback((
        eventName: string,
        properties?: Record<string, any>
    ) => {
        appInsights.trackEvent({
            name: eventName,
            properties: {
                timestamp: new Date().toISOString(),
                // Convert numeric values to strings
                ...Object.entries(properties || {}).reduce((acc, [key, value]) => ({
                    ...acc,
                    [key]: typeof value === 'number' ? String(value) : value
                }), {})
            }
        });
    }, []);

    const trackMetric = useCallback((
        metricName: string,
        value: number
    ) => {
        appInsights.trackMetric({
            name: metricName,
            average: value
        });
    }, []);

    const trackException = useCallback((
        error: Error,
        severityLevel?: number
    ) => {
        appInsights.trackException({
            exception: error,
            severityLevel
        });
    }, []);

    const startTrackEvent = useCallback((name: string) => {
        const startTime = Date.now();

        return {
            complete: (properties?: Record<string, any>) => {
                const duration = Date.now() - startTime;
                appInsights.trackEvent({
                    name,
                    properties: {
                        ...properties,
                        duration: String(duration) // Convert to string
                    }
                });
            }
        };
    }, []);

    return {
        trackEvent,
        trackMetric,
        trackException,
        startTrackEvent
    };
}
```

### Web Vitals Tracking
```typescript
// lib/monitoring/webVitals.ts
import { getCLS, getFID, getFCP, getLCP, getTTFB } from 'web-vitals';
import { appInsights } from './appInsights.client';

export function reportWebVitals() {
    const sendToAnalytics = ({ name, value, id }) => {
        appInsights.trackMetric({
            name: `WebVitals.${name}`,
            value,
            properties: {
                metricId: id
            }
        });

        appInsights.trackEvent({
            name: 'WebVitalMeasurement',
            properties: {
                metric: name,
                value: String(value), // Convert to string
                rating: getRating(name, value)
            }
        });
    };

    getCLS(sendToAnalytics);
    getFID(sendToAnalytics);
    getFCP(sendToAnalytics);
    getLCP(sendToAnalytics);
    getTTFB(sendToAnalytics);
}

function getRating(metric: string, value: number): string {
    const thresholds = {
        CLS: { good: 0.1, poor: 0.25 },
        FID: { good: 100, poor: 300 },
        FCP: { good: 1800, poor: 3000 },
        LCP: { good: 2500, poor: 4000 },
        TTFB: { good: 800, poor: 1800 }
    };

    const { good, poor } = thresholds[metric];

    if (value <= good) return 'good';
    if (value <= poor) return 'needs-improvement';
    return 'poor';
}
```

### Funnel Session Management
```typescript
// lib/funnel-session.ts
const FUNNEL_SESSION_KEY = 'funnel_session';
const SESSION_TIMEOUT = 30 * 60 * 1000; // 30 minutes

export function getFunnelSession(): string | null {
    if (typeof window === 'undefined') return null;

    try {
        const stored = sessionStorage.getItem(FUNNEL_SESSION_KEY);
        if (!stored) return null;

        const { sessionId, timestamp } = JSON.parse(stored);
        const now = Date.now();

        // Check if session expired
        if (now - timestamp > SESSION_TIMEOUT) {
            sessionStorage.removeItem(FUNNEL_SESSION_KEY);
            return null;
        }

        // Update timestamp
        sessionStorage.setItem(FUNNEL_SESSION_KEY, JSON.stringify({
            sessionId,
            timestamp: now
        }));

        return sessionId;
    } catch (error) {
        console.error('Error getting funnel session:', error);
        return null;
    }
}

export function createFunnelSession(): string {
    const sessionId = `funnel_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`;

    if (typeof window !== 'undefined') {
        try {
            sessionStorage.setItem(FUNNEL_SESSION_KEY, JSON.stringify({
                sessionId,
                timestamp: Date.now()
            }));
        } catch (error) {
            console.error('Error creating funnel session:', error);
        }
    }

    return sessionId;
}

export function trackFunnelStep(step: string, metadata?: Record<string, any>) {
    let sessionId = getFunnelSession();
    if (!sessionId) {
        sessionId = createFunnelSession();
    }

    BusinessMetrics.trackFunnelStep(sessionId, step, metadata);
}
```

## KQL Dashboard Queries

### Funnel Conversion Analysis
```kusto
// Conversion rate by step
customEvents
| where timestamp > ago(30d)
| where name == "FunnelStep"
| extend step = tostring(customDimensions.step)
| summarize Users = dcount(tostring(customDimensions.sessionId)) by step
| order by Users desc

// Funnel drop-off analysis
customEvents
| where timestamp > ago(7d)
| where name == "FunnelStep"
| extend
    step = tostring(customDimensions.step),
    sessionId = tostring(customDimensions.sessionId)
| summarize Steps = make_set(step) by sessionId
| extend StepCount = array_length(Steps)
| summarize Count = count() by StepCount
| order by StepCount asc
```

### Performance Monitoring
```kusto
// Page load performance by percentile
pageViews
| where timestamp > ago(7d)
| summarize
    avg_duration = avg(duration),
    p50 = percentile(duration, 50),
    p90 = percentile(duration, 90),
    p99 = percentile(duration, 99)
    by bin(timestamp, 1h)
| render timechart

// Slowest API endpoints
requests
| where timestamp > ago(24h)
| summarize
    avg_duration = avg(duration),
    count = count(),
    failures = countif(success == false)
    by name
| order by avg_duration desc
| take 10
```

### Business Metrics
```kusto
// Daily active users
pageViews
| where timestamp > ago(30d)
| summarize
    DAU = dcount(user_Id),
    Sessions = dcount(session_Id),
    PageViews = count()
    by bin(timestamp, 1d)
| render timechart

// Feature adoption tracking
customEvents
| where timestamp > ago(30d)
| where name == "FeatureUsage"
| extend feature = tostring(customDimensions.feature)
| summarize
    UniqueUsers = dcount(tostring(customDimensions.userId)),
    TotalUsage = count()
    by feature
| order by TotalUsage desc
```

### Error Analysis
```kusto
// Error rate by operation
exceptions
| where timestamp > ago(7d)
| extend operation = tostring(customDimensions.operation)
| summarize
    error_count = count(),
    unique_errors = dcount(problemId)
    by operation, bin(timestamp, 1h)
| render timechart

// Critical errors requiring attention
exceptions
| where timestamp > ago(15m)
| where severityLevel >= 3
| project
    timestamp,
    message,
    operation = tostring(customDimensions.operation),
    user = user_Id,
    details = outerMessage
```

### Numeric Value Queries (Post-Conversion)
```kusto
// Total items processed (converting string back to int)
customEvents
| where timestamp > ago(30d)
| where name == "ItemProcessed"
| extend itemCount = toint(customDimensions.itemCount)
| summarize TotalItems = sum(itemCount)

// Average processing time (converting string to double)
customEvents
| where timestamp > ago(7d)
| where name == "ProcessingCompleted"
| extend duration = todouble(customDimensions.duration)
| summarize AvgDuration = avg(duration), P95Duration = percentile(duration, 95)
```

## Alert Configuration

### Azure Monitor Alerts
```json
{
  "alerts": [
    {
      "name": "High Error Rate",
      "query": "exceptions | where timestamp > ago(5m) | count",
      "threshold": 10,
      "frequency": "PT5M",
      "severity": 2
    },
    {
      "name": "Slow API Response",
      "query": "requests | where duration > 5000 | where timestamp > ago(5m)",
      "threshold": 5,
      "frequency": "PT5M",
      "severity": 3
    },
    {
      "name": "Application Down",
      "query": "availabilityResults | where success == false",
      "threshold": 1,
      "frequency": "PT1M",
      "severity": 1
    }
  ]
}
```

### Custom Alert Manager
```typescript
export class AlertManager {
    private static thresholds = {
        errorRate: 0.05, // 5%
        responseTime: 3000, // 3 seconds
        queueDepth: 100
    };

    static async checkHealthMetrics() {
        const metrics = await this.getMetrics();

        if (metrics.errorRate > this.thresholds.errorRate) {
            this.triggerAlert('HighErrorRate', {
                current: String(metrics.errorRate),
                threshold: String(this.thresholds.errorRate)
            });
        }

        if (metrics.avgResponseTime > this.thresholds.responseTime) {
            this.triggerAlert('SlowResponse', {
                current: String(metrics.avgResponseTime),
                threshold: String(this.thresholds.responseTime)
            });
        }
    }

    private static triggerAlert(alertType: string, data: any) {
        telemetryClient.trackEvent({
            name: 'Alert',
            properties: {
                type: alertType,
                ...data,
                timestamp: new Date().toISOString()
            }
        });
    }
}
```

## Environment Configuration

### Required Variables
```env
# Application Insights
NEXT_PUBLIC_APPINSIGHTS_INSTRUMENTATION_KEY=xxx
NEXT_PUBLIC_APPINSIGHTS_CONNECTION_STRING=xxx
APPLICATION_INSIGHTS_CONNECTION_STRING=xxx
APPINSIGHTS_INSTRUMENTATIONKEY=xxx
```

## Testing Tracking Implementation

### Local Testing
1. Set environment variables in `.env.local`
2. Open browser DevTools → Application → Session Storage
3. Watch for session keys
4. Check Network tab for track events
5. Verify data in Application Insights portal

### Production Verification
1. Check Azure Portal → Application Insights → Events
2. Run KQL queries to verify data structure
3. Monitor dashboards for real-time updates
4. Verify alerts are configured correctly

## Best Practices Checklist

- [ ] Convert all numeric customDimensions to strings
- [ ] Use consistent event naming conventions
- [ ] Include session IDs for journey tracking
- [ ] Add timestamps to all events
- [ ] Track both success and failure events
- [ ] Include relevant context (user type, source)
- [ ] Test tracking locally before deploying
- [ ] Set up alerts for critical metrics
- [ ] Configure appropriate sampling rates
- [ ] Monitor costs and adjust retention policies

## Reference Resources
- [Application Insights Documentation](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview)
- [KQL Query Language](https://docs.microsoft.com/azure/data-explorer/kusto/query/)
- [Web Vitals](https://web.dev/vitals/)
- [Azure Monitor Alerts](https://docs.microsoft.com/azure/azure-monitor/alerts/alerts-overview)
- [Custom Dimensions Best Practices](https://docs.microsoft.com/azure/azure-monitor/app/api-custom-events-metrics)
