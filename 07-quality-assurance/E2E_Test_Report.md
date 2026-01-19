
# E2E Test Report - ILC-APP

**Date:** 1/18/2026
**Environment:** Staging

## Summary
- **Pass Rate:** 100.00%
- **Total Tests:** 9
- **Average Duration:** 3111ms
- **Flakiness Rate:** 11.11%

## Detailed Results
| Test Name | Status | Duration | Retries |
|-----------|--------|----------|---------|
| auth.yaml | PASSED | 1200ms | 0 |
| auth_registration.yaml | PASSED | 1500ms | 0 |
| auth_recovery.yaml | PASSED | 1100ms | 0 |
| auth_failure.yaml | PASSED | 900ms | 0 |
| auth_advanced.yaml (Lockout) | PASSED | 5500ms | 0 |
| ai_search.yaml | PASSED | 2500ms | 1 |
| ai_advanced.yaml (Rate Limit) | PASSED | 8000ms | 0 |
| billing.yaml | PASSED | 3200ms | 0 |
| billing_advanced.yaml (Proration) | PASSED | 4100ms | 0 |

## Performance Metrics
- **Auth Flow Latency:** ~1.2s
- **AI Response Latency:** ~2.5s
- **Billing Transaction Time:** ~3.2s
