## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/89

**Issue title:** API reference doc is missing the POST /profiles request body schema

**Tier:** Tier 1 

**Problem summary:**
The API reference currently lists the available endpoints for creating profiles and requesting reviews, but it does not document the expected request body for either POST /profiles or POST /reviews. As a result, developers cannot determine what fields are required, what each field represents, or what a valid request should look like without inspecting the implementation. The issue affects docs/API.md. A successful fix would add the missing request body schemas, including field descriptions and example values, so the documentation provides complete guidance for both endpoints.

**Branch name:** docs/89-add-api-request-schemas

**Setup confirmation:** App runs locally at localhost:5173

**Cohort ledger:** Issue added to cohort ledger