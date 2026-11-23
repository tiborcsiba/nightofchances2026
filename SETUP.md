# Setup — do this before the workshop

Please have everything below working **before** the session starts. We only have 60 minutes and no time for installs.

## 1. .NET 8 SDK

Download and install from <https://dotnet.microsoft.com/download/dotnet/8.0>.

Verify:

```bash
dotnet --version
```

You should see `8.0.x`.

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

## 5. Git

Download from <https://git-scm.com/downloads>.

Verify:

```bash
git --version
```

## 6. A GitHub account

If you don't have one: <https://github.com/signup>. You'll push your finished DevQuote to your own repo at the end.

## 7. (Optional but nice) PowerShell 7 or a Unix-like shell

Any terminal works, but the workshop commands assume a shell where `curl` is available. On Windows, PowerShell 7 or Git Bash both work.

## Quick self-test

Run these — all four should succeed:

```bash
dotnet --version
git --version
code --version
curl --version
```

If any fail, fix them before the workshop. Bring questions to the start of the session if stuck.

## That's it

You're ready. See you at the workshop!