# Workshop: Building Software with Claude Code

In this workshop you'll use **Claude Code**, an AI coding agent that runs in your terminal. It can read your project, make a plan, edit files, run commands, and check the results.

There are two parts:

1. **Build something new.** In this repo, you'll build a small flashcard app from scratch, starting from just a `CLAUDE.md` file.
2. **Join an existing codebase.** You'll clone [studydeck-example](https://github.com/stevehob/studydeck-example), a larger flashcard app with months of history from a (fictional) team. You'll use Claude Code to understand it and then add a feature.

---

## What you need

| Tool | Why |
|---|---|
| **A Claude account** with Claude Code access | Claude Code needs a **Pro, Max, Team, Enterprise, or Console (API)** account. The free Claude plan does not include Claude Code. |
| **Claude Code** | The AI agent we'll use |
| **Git** | Downloading the projects, and tracking every change Claude makes |
| **Node.js** (LTS version) | Running the Part 2 app and its tests |
| **VS Code** (or any editor you like) | Reading the code Claude writes |

---

## Setup

Pick your operating system. After installing, **close your terminal and open a new one**, so it picks up the newly installed programs.

### Windows

Open **PowerShell** (press Start, type "PowerShell", press Enter) and run:

```powershell
winget install -e --id Microsoft.VisualStudioCode
winget install -e --id OpenJS.NodeJS.LTS
winget install -e --id Git.Git
winget install -e --id Anthropic.ClaudeCode
```

`-e --id` tells winget to match that exact package ID, so it doesn't prompt you to choose between similarly named packages. Accept any prompts that appear.

Git for Windows matters for more than downloading code. It includes **Git Bash**, which Claude Code uses to run commands on Windows.

> **If `npm` fails with "running scripts is disabled on this system":** PowerShell blocks some scripts by default, including the one that starts `npm`. Run this once to allow scripts you install locally, then open a new PowerShell window:
>
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
> ```

### macOS

You'll need [Homebrew](https://brew.sh), the standard Mac package manager. If you don't have it yet, open **Terminal** (press Cmd+Space, type "Terminal") and run the install command shown on [brew.sh](https://brew.sh). Then:

```sh
brew install git node
brew install --cask visual-studio-code
curl -fsSL https://claude.ai/install.sh | bash
```

The last line is Claude Code's official installer. It also keeps Claude Code updated automatically. (`brew install --cask claude-code` works too, but then you update it yourself with `brew upgrade`.)

### Linux (Ubuntu / Debian)

The Node.js in Ubuntu's default package list is often too old, so these commands get the current LTS release from NodeSource instead:

```sh
sudo apt update
sudo apt install -y git curl
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
sudo snap install code --classic
curl -fsSL https://claude.ai/install.sh | bash
```

On other distributions, install `git` and a current Node.js LTS with your package manager, then run the same Claude Code installer.

---

## Check that everything works

In a **new** terminal window, run each of these. Each one should print a version number.

```sh
git --version
node --version
claude --version
```

`node --version` should print v22 or higher. If a command says "not found" or "not recognized", close the terminal, open a new one, and try again. If it still fails, see the [Claude Code install troubleshooting guide](https://code.claude.com/docs/en/troubleshoot-install).

### Tell Git who you are

Git attaches a name and email to every commit, and it refuses to commit until you set them. Claude Code will make commits during the workshop, so do this now:

```sh
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Log in to Claude Code

```sh
claude
```

The first time you run it, Claude Code opens your browser so you can log in. When you see the Claude Code prompt in your terminal, you're done. Type `/exit` to quit.

---

## Get the workshop code

Put both projects in a folder you'll be able to find again:

```sh
mkdir claude-workshop
cd claude-workshop
git clone https://github.com/stevehob/flashcards-starter.git
git clone https://github.com/stevehob/studydeck-example.git
```

Then check that the Part 2 app works:

```sh
cd studydeck-example
npm test
npm start
```

`npm test` should report that all tests pass. `npm start` prints a link, `http://localhost:3000`. Open it in your browser and you should see three sample flashcard decks. Press **Ctrl+C** in the terminal to stop the app.

That's all the setup. See you in class.

---

## During the workshop

### Part 1: Build a flashcard app

```sh
cd flashcards-starter
claude
```

Start by opening `CLAUDE.md` in VS Code. It's the project's standing instructions, which Claude Code reads at the start of every session. Then follow along with the prompts in class.

To try the app, open `index.html` in your browser:

| Windows | macOS | Linux |
|---|---|---|
| `start index.html` | `open index.html` | `xdg-open index.html` |

### Part 2: Join the StudyDeck team

```sh
cd studydeck-example
npm start
```

Leave that running. Open a **second** terminal window, go to the same folder, and run `claude` there.

### Your results will look different, and that's expected

Claude Code doesn't produce identical output every time, so your app won't match what others generate line for line. When yours differs, that's worth looking at: ask Claude *why* it chose that approach.

### Useful Claude Code commands

| Command | What it does |
|---|---|
| `/clear` | Start a fresh conversation (Claude forgets the chat, but still reads `CLAUDE.md`) |
| `/init` | Have Claude study the project and write a `CLAUDE.md` for it |
| **Esc** | Stop Claude mid-task |
| **Shift+Tab** | Cycle permission modes, including **plan mode** (Claude plans but doesn't edit) |
| `/exit` | Quit Claude Code |

### If something goes wrong

Git is your undo button. To throw away every change since your last commit:

```sh
git restore .
git clean -fd
```

The first line undoes edits to existing files. The second deletes new files that were never committed. Use them carefully: anything not committed is gone.
