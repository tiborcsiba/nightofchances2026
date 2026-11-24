# Setup — do this before the workshop

Please have everything below working **before** the session starts. We only have 60 minutes and no time for installs.

## 1. .NET 10 SDK

Download and install from <https://dotnet.microsoft.com/download/dotnet/10.0>.

Verify:

```bash
dotnet --version
```

You should see `10.0.x`.

## 2. Visual Studio Code

Download from <https://code.visualstudio.com/>.

## 3. VS Code extensions

Install these from the Extensions panel (Ctrl+Shift+X):

- **C# Dev Kit** (`ms-dotnettools.csdevkit`)
- **GitHub Copilot** (`github.copilot`)
- **GitHub Copilot Chat** (`github.copilot-chat`)

## 4. GitHub Copilot access

You need an active Copilot subscription. **Students: the free GitHub Copilot tier via GitHub Education works** — sign up at <https://education.github.com/> if you haven't already.

Verify Copilot works:

1. Open VS Code
2. Open the Copilot Chat panel (chat icon in the sidebar, or Ctrl+Alt+I)
3. Type "hello" — you should get a reply

## 5. Quick self-test

Run these — both should succeed:

```bash
dotnet --version
code --version
```

If either fails, fix it before the workshop. Bring questions to the start of the session if stuck.

> Git, GitHub, and the CI/deploy parts will be **demonstrated by the instructor** — you don't need to install Git or have a GitHub account to follow along.

## That's it

You're ready. See you at the workshop!