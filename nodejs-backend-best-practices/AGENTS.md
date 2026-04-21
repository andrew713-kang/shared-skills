# Node.js Backend Best Practices — Compiled Rules

> 30 rules × 6 categories for AI agents writing Node.js/Serverless backend code.
> Curated from goldbergyoni/nodebestpractices, Sairyss/backend-best-practices, Vercel Serverless Docs, OWASP API Security Top 10.

---

## Category 1: Serverless Patterns (CRITICAL)

These rules prevent the most common serverless performance and reliability issues.

---

### sls-cold-start — Minimize Cold Start Impact

**Priority**: CRITICAL | **Impact**: 2-5× faster cold starts

Heavy top-level imports execute on every cold start. Lazy-load expensive modules.

**Bad Example**:

```typescript
// Every cold start loads ALL dependencies upfront
import { createCanvas } from "canvas"; // 50MB native module
import Stripe from "stripe"; // only used in 1 of 5 routes
import { PDFDocument } from "pdf-lib"; // rarely used

export default async function handler(req, res) {
  // Most requests don't need canvas or PDF...
  const keyword = req.query.keyword;
  const data = await fetchData(keyword);
  return res.json(data);
}
```

**Good Example**:

```typescript
// Only import what's always needed at top level
import type { VercelRequest, VercelResponse } from "@vercel/node";

export default async function handler(req: VercelRequest, res: VercelResponse) {
  const keyword = req.query.keyword;
  const data = await fetchData(keyword);

  // Lazy-load heavy modules only when needed
  if (req.query.format === "pdf") {
    const { PDFDocument } = await import("pdf-lib");
    // ... generate PDF
  }

  return res.json(data);
}
```

---

### sls-execution-timeout — Always Set Timeouts on External Calls

**Priority**: CRITICAL | **Impact**: Prevents hung functions consuming quota

Serverless functions have execution limits (Vercel: 10s hobby, 60s pro). External APIs that hang will consume your entire timeout budget.

**Bad Example**:

```typescript
// No timeout — if external API hangs, function times out at platform limit
const response = await fetch("https://openapi.work.go.kr/api/data");
const text = await response.text();
```

**Good Example**:

```typescript
// AbortController ensures we fail fast and return a meaningful error
const controller = new AbortController();
const timeout = setTimeout(() => controller.abort(), 8000); // 8s timeout

try {
  const response = await fetch("https://openapi.work.go.kr/api/data", {
    signal: controller.signal,
  });
  const text = await response.text();
  return text;
} catch (error) {
  if (error.name === "AbortError") {
    throw new Error("External API timed out after 8s");
  }
  throw error;
} finally {
  clearTimeout(timeout);
}
```

---

### sls-tmp-ephemeral — /tmp Is Ephemeral Storage

**Priority**: CRITICAL | **Impact**: Prevents data loss bugs

In serverless, `/tmp` persists between warm invocations of the same instance but is wiped on cold starts. Never use it as a database.

**Bad Example**:

```typescript
import fs from "fs";

// Writing user data to /tmp — will be lost on next cold start
fs.writeFileSync("/tmp/user-sessions.json", JSON.stringify(sessions));

// Later invocation assumes file exists
const sessions = JSON.parse(fs.readFileSync("/tmp/user-sessions.json", "utf8"));
```

**Good Example**:

```typescript
import fs from "fs";

// /tmp is OK for temporary cache with graceful fallback
function getCachedData(key: string): string | null {
  try {
    const path = `/tmp/cache-${key}.json`;
    if (fs.existsSync(path)) {
      const stat = fs.statSync(path);
      const ageMs = Date.now() - stat.mtimeMs;
      if (ageMs < 5 * 60 * 1000) {
        // 5 min TTL
        return JSON.parse(fs.readFileSync(path, "utf8"));
      }
    }
  } catch {
    /* cache miss is fine */
  }
  return null;
}

// Always have a fallback when cache misses
const data = getCachedData("jobs") ?? (await fetchFromAPI());
```

---

### sls-stateless-design — No Global Mutable State

**Priority**: CRITICAL | **Impact**: Prevents race conditions and stale data

Global mutable variables persist across warm invocations but reset on cold starts, creating inconsistent behavior.

**Bad Example**:

```typescript
// Global mutable state — shared across warm invocations, reset on cold start
let requestCount = 0;
let lastUserData: any = null;

export default async function handler(req, res) {
  requestCount++; // Unreliable counter
  lastUserData = req.body; // Data leak between users!
  res.json({ count: requestCount });
}
```

**Good Example**:

```typescript
// Module-level constants and connection reuse are OK
const API_BASE = "https://api.example.com";

// Each request gets fresh state
export default async function handler(req, res) {
  const requestData = req.body; // Scoped to this request
  const result = await processRequest(requestData);
  res.json(result);
}
```

---

### sls-bundle-size — Minimize Bundle Size

**Priority**: CRITICAL | **Impact**: 1.5-3× faster cold starts

Every MB in your function bundle adds cold start latency. Remove unused deps and prefer lighter alternatives.

**Bad Example**:

```typescript
import moment from "moment"; // 300KB+ for simple date formatting
import _ from "lodash"; // 70KB for 1-2 utility functions
import xml2js from "xml2js"; // Full XML parser when regex suffices
```

**Good Example**:

```typescript
// Use built-in or lightweight alternatives
const date = new Date().toISOString(); // Built-in
const unique = [...new Set(items)]; // Built-in
const value = text.match(/<tag>(.*?)<\/tag>/)?.[1] ?? ""; // Regex for simple XML
```

---

## Category 2: Input Validation & Security (CRITICAL)

These rules prevent security vulnerabilities and data corruption.

---

### sec-schema-validation — Validate at Router Level

**Priority**: CRITICAL | **Impact**: Prevents injection, type confusion, crashes

Validate ALL user inputs before they reach business logic. Use a schema library for structured validation.

**Bad Example**:

```typescript
export default async function handler(req, res) {
  // No validation — req.query.page could be "DROP TABLE", "undefined", etc.
  const page = req.query.page;
  const keyword = req.query.keyword;
  const results = await searchJobs(keyword, page); // Garbage in, garbage out
  res.json(results);
}
```

**Good Example**:

```typescript
function sanitize(val: unknown, maxLen: number): string {
  return String(val ?? "")
    .trim()
    .slice(0, maxLen);
}

function validatePage(val: unknown, max = 1000): number {
  const n = parseInt(String(val), 10);
  return isNaN(n) || n < 1 ? 1 : Math.min(n, max);
}

export default async function handler(req, res) {
  // Validated and bounded BEFORE business logic
  const keyword = sanitize(req.query.keyword, 100);
  const page = validatePage(req.query.page);

  if (!keyword) {
    return res.status(400).json({ error: "검색어를 입력해주세요." });
  }

  const results = await searchJobs(keyword, page);
  res.json(results);
}
```

---

### sec-sanitize-output — Escape Output Data

**Priority**: CRITICAL | **Impact**: Prevents XSS and injection in consumers

Data from external APIs may contain HTML/scripts. Sanitize before returning to clients.

**Bad Example**:

```typescript
// Raw external API data passed directly to client
const title = extractXml(apiResponse, "title");
res.json({ title }); // Could contain <script>alert('xss')</script>
```

**Good Example**:

```typescript
function escapeHtml(str: string): string {
  return str
    .replace(/&/g, "&amp;")
    .replace(/</g, "&lt;")
    .replace(/>/g, "&gt;")
    .replace(/"/g, "&quot;");
}

// Sanitize external data before sending to client
const title = escapeHtml(extractXml(apiResponse, "title"));
res.json({ title });
```

---

### sec-rate-limit — Apply Rate Limiting

**Priority**: CRITICAL | **Impact**: Prevents abuse, DoS, quota exhaustion

Without rate limiting, a single client can exhaust your API quotas or overwhelm external services.

**Bad Example**:

```typescript
// No rate limiting — anyone can call this 10,000 times/second
export default async function handler(req, res) {
  const data = await callExpensiveExternalAPI(req.query);
  res.json(data);
}
```

**Good Example**:

```typescript
// Simple in-memory rate limiter for Vercel Serverless
// For production: use Vercel KV, Upstash Redis, or edge middleware
const rateLimitMap = new Map<string, { count: number; resetAt: number }>();

function checkRateLimit(ip: string, limit = 30, windowMs = 60_000): boolean {
  const now = Date.now();
  const entry = rateLimitMap.get(ip);

  if (!entry || now > entry.resetAt) {
    rateLimitMap.set(ip, { count: 1, resetAt: now + windowMs });
    return true;
  }

  if (entry.count >= limit) return false;
  entry.count++;
  return true;
}

export default async function handler(req, res) {
  const ip = req.headers["x-forwarded-for"] || "unknown";
  if (!checkRateLimit(String(ip))) {
    return res
      .status(429)
      .json({ error: "요청이 너무 많습니다. 잠시 후 다시 시도해주세요." });
  }
  // ... handle request
}
```

---

### sec-cors-config — Set Explicit CORS Headers

**Priority**: HIGH | **Impact**: Prevents unauthorized cross-origin access

**Bad Example**:

```typescript
// No CORS headers — browser blocks requests from different origins
// OR overly permissive:
res.setHeader("Access-Control-Allow-Origin", "*");
```

**Good Example**:

```typescript
const ALLOWED_ORIGINS = ["https://rebloom.vercel.app", "http://localhost:3000"];

function setCorsHeaders(req, res) {
  const origin = req.headers.origin;
  if (ALLOWED_ORIGINS.includes(origin)) {
    res.setHeader("Access-Control-Allow-Origin", origin);
  }
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, OPTIONS");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type");
}
```

---

### sec-api-key-rotation — Rotate API Keys with Fallback

**Priority**: HIGH | **Impact**: Zero-downtime key rotation, quota bypass

**Bad Example**:

```typescript
// Single key — if it expires or hits quota, entire service goes down
const API_KEY = process.env.API_KEY;
```

**Good Example**:

```typescript
// Multiple keys with automatic rotation on quota errors
function getApiKeys(): string[] {
  const keys = process.env.API_KEYS?.split(",").filter(Boolean) ?? [];
  const fallback = process.env.API_KEY;
  return fallback ? [fallback, ...keys] : keys;
}

let currentKeyIndex = 0;

function rotateKey(): boolean {
  const keys = getApiKeys();
  if (keys.length <= 1) return false;
  currentKeyIndex = (currentKeyIndex + 1) % keys.length;
  return true;
}

function getCurrentKey(): string {
  return getApiKeys()[currentKeyIndex] ?? "";
}
```

---

### sec-no-secrets-in-response — Never Expose Internal Details

**Priority**: HIGH | **Impact**: Prevents information disclosure

**Bad Example**:

```typescript
catch (error) {
  // Stack trace, file paths, env vars leaked to client
  res.status(500).json({
    error: error.message,
    stack: error.stack,
    env: process.env.API_KEY,
  });
}
```

**Good Example**:

```typescript
catch (error) {
  // Log full details server-side
  console.error('[api/jobs] Error:', error);

  // Return safe message to client
  res.status(500).json({
    error: '일자리 검색 중 오류가 발생했습니다.',
    timestamp: new Date().toISOString(),
  });
}
```

---

## Category 3: External API Integration (HIGH)

These rules ensure reliable communication with external services.

---

### api-retry-backoff — Retry with Exponential Backoff

**Priority**: HIGH | **Impact**: 3-5× improved reliability for flaky APIs

External APIs have transient failures. Retry with increasing delays.

**Bad Example**:

```typescript
// No retry — single failure = user sees error
const response = await fetch(externalApiUrl);
if (!response.ok) throw new Error("API failed");
```

**Good Example**:

```typescript
async function fetchWithRetry(
  url: string,
  options: RequestInit = {},
  maxRetries = 3,
): Promise<Response> {
  for (let attempt = 0; attempt <= maxRetries; attempt++) {
    try {
      const controller = new AbortController();
      const timeout = setTimeout(() => controller.abort(), 8000);

      const response = await fetch(url, {
        ...options,
        signal: controller.signal,
      });
      clearTimeout(timeout);

      if (response.ok) return response;

      // Only retry on 429 (rate limit) or 5xx (server error)
      if (response.status === 429 || response.status >= 500) {
        if (attempt < maxRetries) {
          await new Promise((r) => setTimeout(r, 1000 * Math.pow(2, attempt)));
          continue;
        }
      }

      return response; // 4xx errors: don't retry, return as-is
    } catch (error) {
      if (attempt === maxRetries) throw error;
      await new Promise((r) => setTimeout(r, 1000 * Math.pow(2, attempt)));
    }
  }
  throw new Error(`Failed after ${maxRetries + 1} attempts`);
}
```

---

### api-timeout-abort — Always Set Timeout with AbortController

**Priority**: HIGH | **Impact**: Prevents function timeout exhaustion

See `sls-execution-timeout` for the pattern. Every `fetch()` call MUST have a timeout.

---

### api-parallel-fetch — Parallelize Independent API Calls

**Priority**: HIGH | **Impact**: 2-5× faster when calling multiple APIs

**Bad Example**:

```typescript
// Sequential — total time = sum of all API response times
const jobs = await fetchJobs(keyword);
const training = await fetchTraining(keyword);
const welfare = await fetchWelfare();
// Total: 1s + 1.5s + 0.8s = 3.3s
```

**Good Example**:

```typescript
// Parallel — total time = max of all API response times
const [jobsResult, trainingResult, welfareResult] = await Promise.allSettled([
  fetchJobs(keyword),
  fetchTraining(keyword),
  fetchWelfare(),
]);
// Total: max(1s, 1.5s, 0.8s) = 1.5s

// Extract results with graceful degradation
const jobs = jobsResult.status === "fulfilled" ? jobsResult.value : [];
const training =
  trainingResult.status === "fulfilled" ? trainingResult.value : [];
const welfare = welfareResult.status === "fulfilled" ? welfareResult.value : [];
```

---

### api-circuit-breaker — Fast-Fail on Consecutive Failures

**Priority**: MEDIUM-HIGH | **Impact**: Prevents cascading failures

If an external API is down, stop hammering it. Return cached/fallback data instead.

**Bad Example**:

```typescript
// Every request retries a dead API — wasting time and resources
export default async function handler(req, res) {
  const data = await fetchWithRetry(deadApiUrl, {}, 3); // 24s wasted per request
}
```

**Good Example**:

```typescript
const circuitState = { failures: 0, lastFailure: 0, isOpen: false };
const FAILURE_THRESHOLD = 5;
const RECOVERY_TIME = 30_000; // 30s

function checkCircuit(): boolean {
  if (!circuitState.isOpen) return true;
  if (Date.now() - circuitState.lastFailure > RECOVERY_TIME) {
    circuitState.isOpen = false; // Half-open: try one request
    return true;
  }
  return false; // Circuit open: fast-fail
}

function recordSuccess() {
  circuitState.failures = 0;
  circuitState.isOpen = false;
}
function recordFailure() {
  circuitState.failures++;
  circuitState.lastFailure = Date.now();
  if (circuitState.failures >= FAILURE_THRESHOLD) circuitState.isOpen = true;
}
```

---

### api-response-normalize — Normalize XML/JSON to Unified Interface

**Priority**: MEDIUM | **Impact**: Consistent data handling, easier testing

**Bad Example**:

```typescript
// Each API handler has its own parsing logic
// jobs.ts: extractXml(text, 'wanted'), maps to { title, company, ... }
// training.ts: extractXml(text, 'scn_list'), maps to { title, institution, ... }
// welfare.ts: extractXml(text, 'servList'), maps to { name, description, ... }
// All with duplicated extractXml/extractXmlList functions
```

**Good Example**:

```typescript
// Shared XML parsing utilities
function extractXml(text: string, tag: string): string {
  const regex = new RegExp(`<${tag}[^>]*>([\\s\\S]*?)<\\/${tag}>`, "i");
  const match = text.match(regex);
  return match ? match[1].trim() : "";
}

function extractXmlList(text: string, itemTag: string): string[] {
  const regex = new RegExp(`<${itemTag}[^>]*>[\\s\\S]*?<\\/${itemTag}>`, "gi");
  return text.match(regex) || [];
}

// Standard response wrapper
interface ApiResponse<T> {
  data: T[];
  total: number;
  source: string;
  timestamp: string;
}

function wrapResponse<T>(
  data: T[],
  source: string,
  total?: number,
): ApiResponse<T> {
  return {
    data,
    total: total ?? data.length,
    source,
    timestamp: new Date().toISOString(),
  };
}
```

---

## Category 4: Error Handling (HIGH)

These rules ensure consistent, debuggable error responses.

---

### err-standard-response — Use RFC 7807 Problem Details

**Priority**: HIGH | **Impact**: Consistent error handling across all endpoints

**Bad Example**:

```typescript
// Inconsistent error shapes across endpoints
res.status(500).json({ error: "Failed" });
res.status(400).json({ message: "Bad request", code: "INVALID" });
res.status(404).json({ msg: "Not found" });
```

**Good Example**:

```typescript
interface ErrorResponse {
  error: string; // Human-readable message (Korean)
  status: number; // HTTP status code
  timestamp: string; // ISO 8601
  path?: string; // Request path
}

function errorResponse(
  res: any,
  status: number,
  message: string,
  path?: string,
) {
  return res.status(status).json({
    error: message,
    status,
    timestamp: new Date().toISOString(),
    path,
  });
}

// Usage
errorResponse(res, 400, "검색어를 입력해주세요.", "/api/jobs");
errorResponse(res, 405, "허용되지 않는 HTTP 메서드입니다.", "/api/jobs");
errorResponse(res, 500, "일자리 검색 중 오류가 발생했습니다.", "/api/jobs");
```

---

### err-graceful-degradation — Return Partial Data on Partial Failure

**Priority**: HIGH | **Impact**: Better UX, service stays useful

**Bad Example**:

```typescript
// One API failure kills the entire response
const [jobs, training, welfare] = await Promise.all([
  fetchJobs(), // If this throws, everything fails
  fetchTraining(),
  fetchWelfare(),
]);
```

**Good Example**:

```typescript
// Promise.allSettled: each result independent
const results = await Promise.allSettled([
  fetchJobs(),
  fetchTraining(),
  fetchWelfare(),
]);

// Return whatever succeeded, note what failed
const response = {
  jobs: results[0].status === "fulfilled" ? results[0].value : [],
  training: results[1].status === "fulfilled" ? results[1].value : [],
  welfare: results[2].status === "fulfilled" ? results[2].value : [],
  errors: results
    .filter((r) => r.status === "rejected")
    .map((r) => (r as PromiseRejectedResult).reason?.message),
};
```

---

### err-no-swallow — Never Silently Catch Errors

**Priority**: HIGH | **Impact**: Prevents invisible bugs

**Bad Example**:

```typescript
try {
  await riskyOperation();
} catch (e) {
  // Silent catch — bug is invisible
}
```

**Good Example**:

```typescript
try {
  await riskyOperation();
} catch (error) {
  console.error(
    "[api/jobs] Operation failed:",
    error instanceof Error ? error.message : error,
  );
  // Re-throw or return error response
  throw error;
}
```

---

### err-typed-errors — Use Custom Error Classes

**Priority**: MEDIUM | **Impact**: Better error routing and handling

**Bad Example**:

```typescript
throw new Error("Validation failed"); // No way to distinguish error types
throw new Error("API timeout"); // Same Error class for everything
```

**Good Example**:

```typescript
class AppError extends Error {
  constructor(public statusCode: number, message: string) {
    super(message);
    this.name = 'AppError';
  }
}

class ValidationError extends AppError {
  constructor(message: string) { super(400, message); this.name = 'ValidationError'; }
}

class ExternalApiError extends AppError {
  constructor(message: string, public source: string) {
    super(502, message);
    this.name = 'ExternalApiError';
  }
}

// Error handler can now route by type
catch (error) {
  if (error instanceof ValidationError) {
    return res.status(400).json({ error: error.message });
  }
  if (error instanceof ExternalApiError) {
    return res.status(502).json({ error: error.message, source: error.source });
  }
  return res.status(500).json({ error: '서버 오류가 발생했습니다.' });
}
```

---

### err-http-status-semantic — Use Correct HTTP Status Codes

**Priority**: MEDIUM | **Impact**: Proper client-side error handling

| Status | When to Use                          |
| ------ | ------------------------------------ |
| 400    | Bad input (missing/invalid params)   |
| 401    | Authentication required              |
| 403    | Authenticated but not authorized     |
| 404    | Resource not found                   |
| 405    | HTTP method not allowed              |
| 408    | Request timeout (client can retry)   |
| 422    | Well-formed but semantically invalid |
| 429    | Too many requests (rate limited)     |
| 500    | Unexpected server error              |
| 502    | External API failure                 |
| 503    | Service temporarily unavailable      |

---

## Category 5: Caching & Performance (MEDIUM)

These rules optimize response times and reduce external API load.

---

### cache-response-headers — Set Appropriate Cache-Control

**Priority**: MEDIUM | **Impact**: Reduces redundant API calls

**Bad Example**:

```typescript
// No caching headers — every request hits the server
res.json(data);
```

**Good Example**:

```typescript
// Static data: cache for 1 hour, serve stale for 1 day
res.setHeader(
  "Cache-Control",
  "public, s-maxage=3600, stale-while-revalidate=86400",
);
res.json(data);

// Dynamic/personalized data: no caching
res.setHeader("Cache-Control", "no-store");
res.json(personalData);
```

---

### cache-stale-while-revalidate — SWR Pattern

**Priority**: MEDIUM | **Impact**: Instant responses with background refresh

```typescript
// Vercel Edge Cache supports stale-while-revalidate natively
// s-maxage=60: cache for 60 seconds
// stale-while-revalidate=300: serve stale for 5 min while revalidating in background
res.setHeader(
  "Cache-Control",
  "public, s-maxage=60, stale-while-revalidate=300",
);
```

---

### cache-key-strategy — Include Query Params in Cache Key

**Priority**: MEDIUM | **Impact**: Prevents wrong data served from cache

Cache keys must include all parameters that affect the response.

---

### cache-invalidation — TTL + Event-Driven Invalidation

**Priority**: MEDIUM | **Impact**: Fresh data when it matters

Use TTL for time-based expiry and event triggers for immediate updates after mutations.

---

### cache-memory-guard — Limit In-Memory Cache Size

**Priority**: MEDIUM | **Impact**: Prevents OOM crashes

**Bad Example**:

```typescript
// Unbounded cache — grows until function runs out of memory
const cache = new Map();
cache.set(key, largeData); // Never cleaned up
```

**Good Example**:

```typescript
// Bounded LRU-style cache
const MAX_CACHE_SIZE = 100;
const cache = new Map<string, { data: any; expiry: number }>();

function setCache(key: string, data: any, ttlMs = 300_000) {
  // Evict oldest if full
  if (cache.size >= MAX_CACHE_SIZE) {
    const oldest = cache.keys().next().value;
    if (oldest) cache.delete(oldest);
  }
  cache.set(key, { data, expiry: Date.now() + ttlMs });
}

function getCache(key: string): any | null {
  const entry = cache.get(key);
  if (!entry) return null;
  if (Date.now() > entry.expiry) {
    cache.delete(key);
    return null;
  }
  return entry.data;
}
```

---

## Category 6: Testing & Observability (MEDIUM)

These rules ensure code quality and debuggability.

---

### test-api-route — Test Each API Route

**Priority**: MEDIUM | **Impact**: Catches regressions before deploy

**Bad Example**:

```typescript
// No API tests — bugs found only in production
```

**Good Example**:

```typescript
import { describe, it, expect, vi } from "vitest";
import handler from "../api/jobs";

describe("GET /api/jobs", () => {
  it("returns 405 for non-GET methods", async () => {
    const req = { method: "POST", query: {} };
    const res = { status: vi.fn().mockReturnThis(), json: vi.fn() };

    await handler(req, res);

    expect(res.status).toHaveBeenCalledWith(405);
    expect(res.json).toHaveBeenCalledWith({ error: "Method not allowed" });
  });

  it("returns 400 when no keyword or region", async () => {
    const req = { method: "GET", query: {} };
    const res = { status: vi.fn().mockReturnThis(), json: vi.fn() };

    // Set env for API key
    vi.stubEnv("WORKNET_AUTH_KEY", "test-key");

    await handler(req, res);

    expect(res.status).toHaveBeenCalledWith(400);
  });
});
```

---

### test-mock-external — Mock External APIs

**Priority**: MEDIUM | **Impact**: Fast, reliable, deterministic tests

**Bad Example**:

```typescript
// Tests call real external APIs — slow, flaky, rate-limited
it("searches jobs", async () => {
  const response = await fetch("http://openapi.work.go.kr/...");
  expect(response.ok).toBe(true); // Fails if API is down
});
```

**Good Example**:

```typescript
import { vi } from "vitest";

// Mock fetch globally for API route tests
const mockFetch = vi.fn();
global.fetch = mockFetch;

it("parses XML response correctly", async () => {
  mockFetch.mockResolvedValueOnce({
    ok: true,
    text: () =>
      Promise.resolve(`
      <wantedRoot>
        <wanted><title>경비원</title><company>테스트기업</company></wanted>
      </wantedRoot>
    `),
  });

  const req = { method: "GET", query: { keyword: "경비" } };
  const res = { status: vi.fn().mockReturnThis(), json: vi.fn() };

  vi.stubEnv("WORKNET_AUTH_KEY", "test-key");
  await handler(req, res);

  expect(res.json).toHaveBeenCalledWith(
    expect.objectContaining({
      jobs: expect.arrayContaining([
        expect.objectContaining({ title: "경비원", company: "테스트기업" }),
      ]),
    }),
  );
});
```

---

### test-error-paths — Test Error Responses

**Priority**: MEDIUM | **Impact**: Ensures graceful degradation works

Always test: missing params, invalid input, API key missing, external API failure, timeout.

---

### test-structured-logging — Use JSON Structured Logging

**Priority**: MEDIUM | **Impact**: Searchable, parseable logs

**Bad Example**:

```typescript
console.log("Error in jobs API: " + error.message);
// Not machine-parseable, no context
```

**Good Example**:

```typescript
console.error(
  JSON.stringify({
    level: "error",
    service: "api/jobs",
    message: error.message,
    keyword: req.query.keyword,
    timestamp: new Date().toISOString(),
  }),
);
```

---

## Utility Templates

### Shared Validation Utilities

```typescript
// api/utils/validation.ts

/** 입력 문자열 정제 — 길이 제한 + 트림 */
export function sanitize(val: unknown, maxLen: number): string {
  return String(val ?? "")
    .trim()
    .slice(0, maxLen);
}

/** 페이지 번호 검증 — 1~max 범위로 보정 */
export function validatePage(val: unknown, max = 1000): number {
  const n = parseInt(String(val), 10);
  return isNaN(n) || n < 1 ? 1 : Math.min(n, max);
}

/** HTTP 메서드 검증 — 허용되지 않으면 405 반환 */
export function validateMethod(req: any, res: any, allowed: string[]): boolean {
  if (!allowed.includes(req.method)) {
    res.status(405).json({ error: "Method not allowed" });
    return false;
  }
  return true;
}

/** 환경변수 키 확인 — 없으면 500 반환 */
export function requireEnvKey(res: any, ...keys: string[]): string | null {
  for (const key of keys) {
    const val = process.env[key];
    if (val) return val;
  }
  res
    .status(500)
    .json({ error: "API 서비스를 일시적으로 사용할 수 없습니다." });
  return null;
}
```

### Shared Error Utilities

```typescript
// api/utils/errors.ts

export function errorResponse(res: any, status: number, message: string) {
  return res.status(status).json({
    error: message,
    status,
    timestamp: new Date().toISOString(),
  });
}
```

### Shared Fetch Utilities

```typescript
// api/utils/fetch.ts

/** 타임아웃이 있는 fetch — AbortController 기반 */
export async function fetchWithTimeout(
  url: string,
  options: RequestInit = {},
  timeoutMs = 8000,
): Promise<Response> {
  const controller = new AbortController();
  const timeout = setTimeout(() => controller.abort(), timeoutMs);
  try {
    return await fetch(url, { ...options, signal: controller.signal });
  } finally {
    clearTimeout(timeout);
  }
}

/** XML 태그 값 추출 */
export function extractXml(text: string, tag: string): string {
  const regex = new RegExp(`<${tag}[^>]*>([\\s\\S]*?)<\\/${tag}>`, "i");
  const match = text.match(regex);
  return match ? match[1].trim() : "";
}

/** XML 반복 요소 리스트 추출 */
export function extractXmlList(text: string, itemTag: string): string[] {
  const regex = new RegExp(`<${itemTag}[^>]*>[\\s\\S]*?<\\/${itemTag}>`, "gi");
  return text.match(regex) || [];
}
```
