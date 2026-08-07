## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/89

**Issue title:** API reference doc is missing the POST /profiles request body schema

**Tier:** Tier 1 

**Problem summary:**
The API reference currently lists the available endpoints for creating profiles and requesting reviews, but it does not document the expected request body for either POST /profiles or POST /reviews. As a result, developers cannot determine what fields are required, what each field represents, or what a valid request should look like without inspecting the implementation. The issue affects docs/API.md. A successful fix would add the missing request body schemas, including field descriptions and example values, so the documentation provides complete guidance for both endpoints.

**Is This Issue Right for Me? Checklist Reasoning:**

I was able to explain the issue in my own words and identify a clear before-and-after outcome. Currently, docs/API.md lists the two POST endpoints without explaining the data they accept. Once the issue is complete, developers should be able to use the documentation to understand and construct valid requests for both endpoints.

I confirmed that the primary file affected is docs/API.md, and I reviewed its current Profiles and Reviews sections. I will also inspect the corresponding API routes and request models to make sure the documented fields, types, required values, and examples match the actual implementation.

This issue is labeled Tier 1, which is a realistic fit because the final change is localized to the API documentation and should not require changes across multiple application modules. Although I need to review the route and schema definitions for accuracy, the expected implementation should remain limited to one documentation file.

The issue does not appear to require a new automated test because it changes documentation rather than application behavior. Instead, I can verify the work by comparing the documented schemas against the existing request models and checking that the Markdown is readable and complete. I understand the surrounding API structure well enough to outline the work: locate the request models for POST /profiles and POST /reviews, identify their accepted fields, and add field descriptions and example request bodies to docs/API.md.

I checked the issue scope and estimated effort of two to three hours, which is realistic within the Week 8–9 timeline. I also confirmed that the issue does not list any unresolved blockers or dependencies. Based on its limited scope, clear definition of done, and Tier 1 classification, I believe this issue is an appropriate choice for me.

**Branch name:** docs/89-add-api-request-schemas

**Setup confirmation:** App runs locally at localhost:5173

**Cohort ledger:** Issue added to cohort ledger

---

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** [42baabc](https://github.com/ascherj/pathreview/commit/42baabcb02244b357f149dfab9430496cdb55896)

**Reproduction summary:**
I opened `docs/API.md` and confirmed that the `POST /profiles` and `POST /reviews` entries each contain only a single descriptive line with no request body schema, field list, or example. I then inspected `api/routes/profiles.py`, `api/routes/reviews.py`, `api/schemas/profile.py`, and `api/schemas/review.py` to identify the actual accepted fields and types. The gap is concrete: a developer reading the docs has no way to construct a valid request for either endpoint without reading the source code.

**PLAN.md link:** [PLAN.md](PLAN.md)

**Blockers or open questions:**
`POST /profiles` uses `multipart/form-data` rather than a JSON body because it accepts a file upload. I need to confirm the best Markdown format for documenting a multipart form request (field table vs. code block) so the docs stay consistent with the existing style in `docs/API.md`.

---

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
The file API.md has been updated with the reqest body schemas of POST /profile and POST /review endpoints. I also created unit tests to verify the presence of these documentation changes. 

**Next steps:**
I will work on putting out a PR for these changes and closing the issue.

**Blockers:**
N/A

---

### Check-in 2 (end of week)

**PR link:** [[link to your submitted pull request](https://github.com/ascherj/pathreview/pull/1004)]

**Branch:** docs/89-add-api-request-schemas

**What you built:**
Added request body schemas for `POST /profiles` and `POST /reviews` to `docs/API.md`. Each entry now documents the content type, a field table with name, type, required/optional status, and constraints, and an example `curl` request. `POST /profiles` uses `multipart/form-data` with three optional fields (`github_username`, `portfolio_url`, `resume_file`); `POST /reviews` uses `application/json` with one required field (`profile_id`, UUID).

**Tests added or updated:**
`tests/unit/test_api_docs.py` — new file with 6 unit tests that assert each documented content type and field name is present in `docs/API.md`. Tests use `@pytest.mark.unit` and run as part of `make test-unit`.

**Self-review confirmation:** [ ] make check passes  [x] make test-unit passes (53 pre-existing failures unrelated to this change; 6 new tests pass)

**Draft PR feedback received from:** None