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
- **Generate a Dockerfile** during the "Build & Package" phase (multi-stage, production-ready) 
  so students can see what one looks like. Students don't have Docker installed, so **do not** 
  ask them to build or run the image — show the file, walk through the stages briefly, and move on.
- After each step, **pause and tell me the exact commands to run** so students can see output 
  (dotnet run, curl, dotnet test, etc.). Do not batch everything at once.
- **All terminal commands must be PowerShell-compatible, single-line, copy-pasteable into the 
  VS Code integrated terminal on Windows.** Specifically:
  - No multi-line commands, no backtick line continuations, no heredocs.
  - Prefer native PowerShell cmdlets over `curl` for HTTP requests — use `Invoke-RestMethod` with 
    a hashtable piped to `ConvertTo-Json`, so there is no quote-escaping. If you must use curl, 
    use `curl.exe` (not the PowerShell alias) and keep the whole command on one line.
  - Use single quotes for string literals where possible to avoid PowerShell variable expansion 
    issues.
  - Separate multiple statements with `;` on one line when the student needs to run them together 
    (e.g. capture a response and extract an id), but prefer giving one command at a time.
  - Never use smart/curly quotes — only straight ASCII quotes.

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
a new endpoint + test from a one-line requirement. **We will actually invoke this prompt file 
in Phase 4** — so make sure its instructions are concrete enough to produce a working endpoint 
(reuse the existing repository, follow the same Minimal API patterns, add an integration test, 
return a summary + commands to run).

### 2. Plan
Generate 3–4 user stories in "As a … I want … so that …" form, each with 2–3 acceptance 
criteria. Save to `docs/user-stories.md`.

### 3. Design
Produce a short `docs/design.md` with: the data model (`Quote` record), 5 REST endpoints 
(GET all, GET by id, POST, PUT, DELETE), the folder structure, and a one-paragraph 
rationale for choices.

### 4. Develop
Scaffold the solution and both projects, implement the `Quote` model, `IQuoteRepository` 
+ `InMemoryQuoteRepository`, DI registration, and **four of the five endpoints** (GET all, 
GET by id, POST, PUT) with input validation and proper status codes, and Swagger UI enabled 
in Development. Give me the `Invoke-RestMethod` commands to try each endpoint.

Then **stop and instruct me (the instructor) to add the DELETE endpoint by invoking the 
prompt file we created in Phase 1**, like this:

> "Now run `/add-endpoint Requirement: add DELETE /quotes/{id} that removes a quote and 
> returns 204 No Content, or 404 if the id does not exist` in Copilot Chat to scaffold 
> the last endpoint from the reusable prompt."

Explain to students in one sentence why this matters: the prompt file enforces the same 
conventions (Minimal API style, repo reuse, integration test) without the instructor 
having to re-state them. Wait for me to run it before continuing to Phase 5.

### 5. Test
Create unit tests for the repository and integration tests for the endpoints using 
`WebApplicationFactory`. Aim for ~6–8 focused tests. Run them and show results.

### 6. Build & Package
Run `dotnet publish -c Release` and show the produced artifacts. Then **generate a 
production-ready multi-stage `Dockerfile`** at the repo root (SDK image for build, 
ASP.NET runtime image for the final stage, non-root user, exposed port). Walk through 
the stages in one short paragraph so students see how containerization works. Do **not** 
ask them to build or run the image — they don't have Docker installed. Also add a 
`.dockerignore` next to the Dockerfile.

### 7. Deploy (CI) — instructor demo
Students are not required to have Git or a GitHub account set up. Generate 
`.github/workflows/ci.yml` with these jobs, in order, on push/PR:
1. `dotnet restore` + `dotnet test` on the runner — fast feedback with readable test output.
2. `docker build` using the Dockerfile from Phase 6 — the production compile happens inside 
   the image's SDK stage, so there is **no standalone `dotnet build` step**. The container 
   image is the build artifact.

Briefly explain the story: *"CI runs the tests, then packages the app into a container — one 
build artifact, one deploy target."* Mention that adding a push-to-registry + deploy job 
(Azure, AWS, GHCR) is a one-prompt extension, but we won't add it today. The **instructor 
will demonstrate** pushing to GitHub and watching the workflow run.

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
  suggestion for what a student could extend as homework (e.g. swap the in-memory 
  repository for SQLite + EF Core, or add a `/quotes/random` endpoint).

Start now with **Phase 1: Customization & Memory**.