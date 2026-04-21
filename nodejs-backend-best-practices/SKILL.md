---
name: nodejs-backend-best-practices
description: Node.js and Serverless backend optimization guidelines curated from industry best practices. This skill should be used when writing, reviewing, or refactoring backend API routes, serverless functions, or Node.js server code. Triggers on tasks involving API endpoints, data validation, external API calls, error handling, caching, or backend testing.
---

# Node.js Backend Best Practices

Curated backend optimization guide for Node.js and Serverless applications. Contains 30 rules across 6 categories, prioritized by impact to guide automated refactoring and code generation.

## When to Apply

Reference these guidelines when:

- Writing new API routes or serverless functions
- Calling external APIs (REST, SOAP, XML)
- Implementing input validation or error handling
- Reviewing backend code for security or performance issues
- Adding tests for API endpoints
- Configuring caching or rate limiting

## Rule Categories by Priority

| Priority | Category                    | Impact   | Prefix   |
| -------- | --------------------------- | -------- | -------- |
| 1        | Serverless Patterns         | CRITICAL | `sls-`   |
| 2        | Input Validation & Security | CRITICAL | `sec-`   |
| 3        | External API Integration    | HIGH     | `api-`   |
| 4        | Error Handling              | HIGH     | `err-`   |
| 5        | Caching & Performance       | MEDIUM   | `cache-` |
| 6        | Testing & Observability     | MEDIUM   | `test-`  |

## Quick Reference

### 1. Serverless Patterns (CRITICAL)

- `sls-cold-start` - Minimize top-level imports, use lazy initialization
- `sls-execution-timeout` - Always set AbortController timeout on external calls
- `sls-tmp-ephemeral` - /tmp is ephemeral; never rely on it for persistence
- `sls-stateless-design` - No global mutable state; each request is independent
- `sls-bundle-size` - Remove unused dependencies, enable tree-shaking

### 2. Input Validation & Security (CRITICAL)

- `sec-schema-validation` - Validate inputs with Zod/Joi at router level
- `sec-sanitize-output` - Escape output to prevent XSS in API responses
- `sec-rate-limit` - Apply rate limiting per IP or API key
- `sec-cors-config` - Set explicit CORS headers on API routes
- `sec-api-key-rotation` - Rotate API keys periodically with fallback
- `sec-no-secrets-in-response` - Never expose internal errors or stack traces

### 3. External API Integration (HIGH)

- `api-retry-backoff` - Retry with exponential backoff for 429/5xx
- `api-timeout-abort` - Use AbortController with 10s timeout
- `api-parallel-fetch` - Use Promise.allSettled() for independent API calls
- `api-circuit-breaker` - Fast-fail after consecutive failures
- `api-response-normalize` - Normalize XML/JSON to unified interface

### 4. Error Handling (HIGH)

- `err-standard-response` - Use RFC 7807 Problem Details format
- `err-graceful-degradation` - Return partial data on partial failure
- `err-no-swallow` - Never silently catch errors; always log
- `err-typed-errors` - Use custom error classes (AppError, ValidationError)
- `err-http-status-semantic` - Use correct HTTP status codes (400 vs 422 vs 500)

### 5. Caching & Performance (MEDIUM)

- `cache-response-headers` - Set appropriate Cache-Control headers
- `cache-stale-while-revalidate` - Use SWR pattern for freshness + speed
- `cache-key-strategy` - Include query params in cache keys
- `cache-invalidation` - TTL + event-driven invalidation
- `cache-memory-guard` - Limit in-memory cache size to prevent OOM

### 6. Testing & Observability (MEDIUM)

- `test-api-route` - Integration test each API route (happy + error paths)
- `test-mock-external` - Mock external APIs with msw/nock
- `test-error-paths` - Test error responses, not just success
- `test-structured-logging` - Use JSON structured logging format

## How to Use

Read `AGENTS.md` for the full compiled document with all 30 rules expanded, including Bad/Good code examples and impact explanations.

## Templates

Common backend utility patterns are included in the compiled guide:

- Input validation utilities (sanitize, validatePage, requireEnvKey)
- Error response helpers (RFC 7807 format)
- External API fetch wrapper (timeout + retry + XML parsing)
