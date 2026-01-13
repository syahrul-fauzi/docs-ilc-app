# 📋 Test Cases

| ID | Module | Scenario | Expected | Status |
| :--- | :--- | :--- | :--- | :--- |
| TC-01 | Auth | Login valid | Redirect to Home | ✅ Passed |
| TC-02 | AI Search | AI Search empty | Show validation message | ✅ Passed |
| TC-03 | AI Search | Trending question selection | Show AI analysis result | ✅ Passed |
| TC-04 | AI Search | Manual query submission | Show AI analysis result | ✅ Passed |
| TC-05 | AI Search | Share AI result to Community | Post created in feed | ✅ Passed |
| TC-06 | AI Search | Clear chat history | Messages cleared from UI | ✅ Passed |
| TC-07 | Community | View feed | List of posts displayed | ✅ Passed |
| TC-08 | Community | Create regular post | Post visible in feed | ✅ Passed |
| TC-09 | Community | Like a post | Like count increments | ✅ Passed |
| TC-10 | Community | Comment on a post | Comment visible in detail view | ✅ Passed |
| TC-11 | Community | Delete own post | Post removed from feed | ✅ Passed |
| TC-12 | Community | Admin delete any post | Post removed by admin | ✅ Passed |
| TC-13 | Community | Explore AI Insight topic | Redirect to Search with topic | ✅ Passed |

## 📊 Coverage Report (Community Hub)

| File | Statements | Branches | Functions | Lines |
| :--- | :--- | :--- | :--- | :--- |
| CommunityRepository.ts | 100% | 100% | 100% | 100% |
| CommunityService.ts | 100% | 100% | 100% | 100% |
| communityContext.tsx | 90.9% | 78.9% | 91.7% | 93.1% |
| PostCard.tsx | 91.7% | 66.7% | 100% | 94.4% |
| AIInsightCard.tsx | 100% | 87.2% | 100% | 100% |

**Total Community Coverage: >90%**

## 🚀 Maestro E2E Suites

- `auth.yaml`: Login flow validation.
- `ask_ai_journey.yaml`: Full end-to-end AI search & share journey.
- `community.yaml`: Feed, posting, and engagement validation.
- `ai_search_no_results.yaml`: Empty state validation.
