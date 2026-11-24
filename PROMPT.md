You are helping me run a 60-minute live university workshop on practical AI-assisted development. 
We will build a small .NET 10 application **together, step by step**, demonstrating how GitHub 
Copilot helps across the entire Software Development Lifecycle (Plan → Design → Develop → Test 
→ Build → Deploy → Operate → Document).

## The application: "DevQuote"
A **.NET 10 Minimal Web API** that manages a collection of developer quotes (author + text + tags), 
with Swagger UI, an in-memory repository, structured logging, a health endpoint, unit tests, 
and a GitHub Actions CI workflow.

## Hard constraints
- Total time budget: **60 minutes**. Keep every step small and runnable. Leave buffer time — 
  don't rush to fill every minute.
- Target: **.NET 10**, C# 14, Minimal APIs (no MVC controllers), nullable enabled.
- Single solution, two projects: `DevQuote.Api` and `DevQuote.Tests` (xUnit + FluentAssertions).
- No database — use a thread-safe in-memory `ConcurrentDictionary` repository behind an interface.
- **Docker is out of scope** for the live build (students don't have Docker installed), but you 
  should briefly mention during the "Build & Package" phase that containerization is the modern 
  packaging approach and that Copilot can generate a Dockerfile on demand — just don't create one.
- After each step, **pause and tell me the exact commands to run** so students can see output 
  (dotnet run, curl, dotnet test, etc.). Do not batch everything at once.

## Walk us through these phases in order, announcing each phase explicitly

### 1. Customization & Memory (first — this is a teaching moment)
Before writing code, create `.github/copilot-instructions.md` with project-wide rules 
(C# style, minimal API preference, test framework, naming conventions). Briefly explain 
to the students, in the chat output, that:
- `copilot-instructions.md` = **persistent project memory** Copilot auto-loads every session
- **Prompt files** (`.github/prompts/*.prompt.md`) = reusable task recipes invoked with `/name`
- **Custom chat modes / agents** = scoped personas with their own tools and instructions
- **MCP servers** = external tools/data sources Copilot can call
Also create one example prompt file: `.github/prompts/add-endpoint.prompt.md` that scaffolds 
a new endpoint + test from a one-line description. Mention it but don't use it yet.

### 2. Plan
Generate 3–4 user stories in "As a … I want … so that …" form, each with 2–3 acceptance 
criteria. Save to `docs/user-stories.md`.

### 3. Design
Produce a short `docs/design.md` with: the data model (`Quote` record), 5 REST endpoints 
(GET all, GET by id, POST, PUT, DELETE), the folder structure, and a one-paragraph 
rationale for choices.

### 4. Develop
Scaffold the solution and both projects, implement the `Quote` model, `IQuoteRepository` 
+ `InMemoryQuoteRepository`, DI registration, all five endpoints with input validation 
and proper status codes, and Swagger UI enabled in Development. Give me the curl commands 
to try each endpoint.

### 5. Test
Create unit tests for the repository and integration tests for the endpoints using 
`WebApplicationFactory`. Aim for ~6–8 focused tests. Run them and show results.

### 6. Build & Package
Run `dotnet publish -c Release` and show the produced artifacts. **Briefly mention** 
(don't implement) that in a real project this is where a Dockerfile would live, and 
that Copilot can generate a production-ready multi-stage Dockerfile from a one-line 
request — this is the modern way to ship .NET services.

### 7. Deploy (CI) — instructor demo
Students are not required to have Git or a GitHub account set up. Generate 
`.github/workflows/ci.yml` (restore, build, test on push/PR) so it exists in the 
project, and briefly explain each job — the **instructor will demonstrate** pushing 
to GitHub and watching the workflow run. Mention that adding a deploy job (to Azure, 
AWS, or a container registry) is a one-prompt extension.

### 8. Operate
Add a `/health` endpoint, Serilog console logging with request logging middleware, 
and a basic global exception handler returning Problem Details.

### 9. Document
Generate a `README.md` with: what it is, how to run locally, how to run tests, 
endpoint table, and a "Built with Copilot in 60 minutes" note.

## How you should behave throughout
- Announce "**Phase N: <name>**" at the start of each phase.
- Keep code minimal and idiomatic — no premature abstractions, no excessive comments.
- After each phase, give me a **one-sentence recap** and the **commands to run next**.
- If something would take longer than its time slot, say so and offer a shorter variant.
- At the very end, print a short retrospective: which phase benefited most from AI, 
  which Copilot customization feature we actually used vs. just mentioned, and one 
  suggestion for what a student could extend as homework (e.g. "add a Dockerfile — 
  ask Copilot: 'add a multi-stage Dockerfile for this API'").

Start now with **Phase 1: Customization & Memory**.