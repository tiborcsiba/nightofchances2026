# DevQuote Workshop

A 60-minute hands-on workshop: build a small .NET 10 Web API from scratch using **GitHub Copilot**, covering every phase of the Software Development Lifecycle.

By the end you'll have a working, tested, CI-wired REST API that stores developer quotes — and, more importantly, you'll have seen how AI assists at every stage: planning, design, coding, testing, packaging, deployment, operations, and documentation.

## What we're building: DevQuote

A **.NET 10 Minimal Web API** that manages a collection of developer quotes.

- 5 REST endpoints (list, get, create, update, delete)
- In-memory storage (no database to install)
- Swagger UI to try endpoints in the browser
- Unit + integration tests
- `/health` endpoint and structured logging
- GitHub Actions CI pipeline *(demonstrated by the instructor — students don't need Git/GitHub set up)*

## How to use this prompt

1. **Install prerequisites** — see [SETUP.md](./SETUP.md).
2. **Open an empty folder** in VS Code (not this cloned repo — a fresh folder where Copilot will generate the project).
3. **Open GitHub Copilot Chat** and switch to **Agent mode** (dropdown at the top of the chat panel).
4. **Copy the entire contents of [`PROMPT.md`](./PROMPT.md)** and paste it as your first message to Copilot.
5. **Follow along** — Copilot announces each phase, pauses between steps, and tells you which commands to run.

## Workshop pacing

| Min   | Phase                   |
| ----- | ----------------------- |
| 0–5   | Customization & Memory  |
| 5–10  | Plan (user stories)     |
| 10–15 | Design (model, API)     |
| 15–30 | Develop (scaffold + CRUD) |
| 30–42 | Test (xUnit)            |
| 42–45 | Build (publish + Docker mention) |
| 45–52 | Deploy (GitHub Actions CI) |
| 52–57 | Operate (health, logging) |
| 57–60 | Document + retrospective |

## Copilot customization features we'll touch

- **`.github/copilot-instructions.md`** — persistent project memory loaded every session
- **Prompt files** (`.github/prompts/*.prompt.md`) — reusable task recipes, invoked with `/name`
- **Custom chat modes / agents** — scoped personas with their own tools
- **MCP servers** — external tools and data sources Copilot can call

## If you fall behind

The prompt is designed to pause between phases. If your Copilot is slower or you get stuck, skip ahead by typing: *"Skip to Phase N."* The final retrospective works even if you only completed half the phases.

## Homework / extensions

- Add a Dockerfile (ask Copilot: *"Add a multi-stage Dockerfile for this API"*)
- Swap the in-memory repo for SQLite + EF Core
- Add a `/quotes/random` endpoint
- Add a tiny HTML/Blazor frontend
- Add a deploy job to the CI workflow (Azure Web App, container registry, etc.)

## License

MIT — do whatever you like with the prompt and code.