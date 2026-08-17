# Copilot Instructions --- API Automation Framework (Python + Pytest + Requests)

You are working inside an existing API automation framework. Your job is
to add or modify API tests with **ZERO framework drift**.

This repository supports multiple APIs. Each API lives under:

`API/api_<api_name>/`

Example:

`API/api_dummyjson/`

------------------------------------------------------------------------

## Non-Negotiables

-   DO NOT change or reorganize the existing folder structure.
-   DO NOT create new framework layers or utilities unless explicitly
    requested.
-   DO NOT duplicate API client or configuration logic.
-   DO NOT hardcode base URLs, credentials, tokens, or environment
    values.
-   Base URL must come from the existing environment/configuration.
-   Environment/profile selection must use the existing repository
    pattern.
-   Keep tests deterministic, independent, and repeatable.

------------------------------------------------------------------------

## Project Structure Rules --- READ ONLY

Treat the existing workspace structure as **READ-ONLY**.

### Allowed locations for new or updated files

Create or modify files only in the correct existing locations for the
target API.

API tests:

`API/api_<api_name>/tests/`

Shared fixtures for that API:

`API/api_<api_name>/tests/conftest.py`

Update `conftest.py` only when required for the requested tests.

### API Client / Configuration Utilities

-   Reuse existing utilities.
-   Do not reinvent HTTP wrappers.
-   Update framework utilities only when explicitly requested.

------------------------------------------------------------------------

## Creating a New API Module

Create a new API module only when a module for the required base URL
does not already exist.

Create:

`API/api_<api_name>/`

Inside it, create only the minimum required test structure:

`API/api_<api_name>/tests/`

`API/api_<api_name>/tests/conftest.py` only when required.

Do not create a new root-level framework. Do not reorganize existing API
modules.

------------------------------------------------------------------------

## Scope Control

-   Implement ONLY the API test cases provided in the prompt,
    requirement, or ticket.
-   Do NOT add additional endpoints or flows unless explicitly
    requested.
-   Do NOT refactor unrelated code while implementing tests.
-   Do NOT add unnecessary utilities or abstractions.

------------------------------------------------------------------------

## HTTP & Assertion Rules

-   Reuse the existing `APIClient` fixture/utilities.
-   Do not duplicate Requests logic inside tests when the existing
    client supports the operation.

Validate:

-   HTTP status code
-   Essential response contract
-   Minimal schema / required key checks
-   Scenario-specific values only when deterministic

Use clear assertions with explicit failure messages where appropriate.

For write endpoints, do not assert persistence unless the API explicitly
guarantees persistence.

Keep negative tests aligned only with defined or known API behavior.

------------------------------------------------------------------------

## Test Rules

Tests follow:

**Arrange → Act → Assert**

Each test should include meaningful validations:

-   Status code
-   Response schema / key checks
-   Scenario-specific deterministic value checks

Allowed Pytest markers:

``` python
@pytest.mark.smoke
@pytest.mark.regression
```

Tests must be:

-   Independent
-   Repeatable
-   Deterministic

Use parametrization where appropriate to avoid unnecessary copy-paste
tests.

------------------------------------------------------------------------

## Environment & Secrets

-   Use the existing dotenv/configuration behavior.
-   Do not implement a new environment loader.
-   Keep secrets in environment files or CI variables.
-   Never hardcode secrets in tests.
-   OS environment variables should override environment-file values
    where the framework already supports this behavior.

### Environment Convention

For each API, follow the existing repository environment-selection
pattern.

Preferred pattern:

`<API_NAME>_ENV`

Example:

`DUMMYJSON_ENV`

If the repository already uses another naming convention, follow it
exactly.

Do NOT introduce a new environment system.

------------------------------------------------------------------------

## No Guessing Policy --- STRICT

If any of the following are unclear, **DO NOT GUESS**:

-   Endpoint contract
-   Expected status code
-   Required headers
-   Authentication details
-   Response payload expectations
-   Error behavior
-   Other undocumented assumptions

Instead:

-   Add a TODO comment where appropriate.
-   Clearly identify the missing information.
-   Stop implementing the unclear portion until details are provided.
-   If a test cannot safely be implemented, use `pytest.skip()` with a
    clear reason only when skipping is allowed by the project/ticket.

Example:

``` python
pytest.skip("Expected API behavior is not confirmed")
```

------------------------------------------------------------------------

## AI-Assisted Development Rules

AI tools such as GitHub Copilot may be used to accelerate:

-   API test generation
-   Boilerplate creation
-   Assertion suggestions
-   Debugging
-   Error analysis
-   Code understanding

However:

-   Validate AI-generated code before implementation.
-   Ensure generated code follows the existing framework.
-   Do not allow AI to redesign the framework unnecessarily.
-   Reject hardcoded URLs, credentials, tokens, or environment values.
-   Do not accept guessed API behavior.
-   Remove unnecessary generated code.
-   Keep implementation limited to the requested scope.

The goal is to use AI for productivity while maintaining framework
consistency.

------------------------------------------------------------------------

## Reporting Requirements

For each implementation batch, always provide:

1.  List of files created or updated.
2.  Full contents of new or updated files.
3.  TODOs or blockers, including missing endpoint behavior or contracts.
4.  Exact Pytest command(s) to run the affected tests.
5.  Confirmation that:
    -   No structure drift occurred.
    -   No base URL or credentials were hardcoded.
    -   No unrelated refactoring was performed.

------------------------------------------------------------------------

## Goal

Maintain a clean, reusable, and maintainable API automation framework
while leveraging AI tools to improve implementation and debugging
productivity.

**Existing Framework → Requirement → AI Assistance → Validation →
Implementation**
