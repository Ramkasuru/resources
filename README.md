# 💻 The Terminal Cheat Sheet Every Developer Needs Right Now

### Because AI agents live in your terminal — and so should you

AI coding agents (Claude Code, Codex, Cursor, etc.) spend most of their time in one place: the terminal. They navigate your repo, run your tests, install your dependencies, and fire off git commands — all from the command line.

Which means the less you know about the terminal, the harder it is to tell whether an agent just did something brilliant or something dangerous.

This is my running cheat sheet of what I think every developer — especially one working alongside AI agents — should have down cold.

---

## 1. Getting Around the File System

The absolute basics.

| Command | What it does |
| --- | --- |
| `pwd` | Print where you currently are |
| `ls` | List what's in the current folder |
| `ls -la` | List everything, hidden files included |
| `cd folder` | Step into a folder |
| `cd ..` | Step back up one level |
| `cd ~` | Jump straight home |
| `cd -` | Bounce back to your last folder |
| `clear` | Wipe the screen |

### 🔑 Concept: Paths

Know the difference between **relative** and **absolute** paths.

`./src/app.js` — relative to wherever you're standing.

`/Users/you/project/src/app.js` — the full, unambiguous location.

Shorthand you'll see everywhere:

`.` → here

`..` → one level up

`~` → home

`/` → the root of everything

---

## 2. Handling Files

| Command | What it does |
| --- | --- |
| `touch file.txt` | Create an empty file |
| `mkdir folder` | Create a folder |
| `mkdir -p a/b/c` | Create a whole nested folder path at once |
| `cp file copy.txt` | Duplicate a file |
| `cp -r folder copy` | Duplicate a folder |
| `mv old.txt new.txt` | Move or rename |
| `rm file.txt` | Delete a file |
| `rm -r folder` | Delete a folder |
| `cat file.txt` | Dump a file's contents to screen |
| `less file.txt` | Page through a file |

### ⚠️ Respect `rm`

There's no recycle bin here. What you delete from the terminal is usually gone.

`rm -rf` especially — know exactly what you're pointing it at before you hit enter.

---

## 3. Finding Things

Sooner or later you'll need to hunt down a file or a string of code.

| Command | What it does |
| --- | --- |
| `find . -name "*.js"` | Find files matching a pattern |
| `grep "TODO" file.txt` | Search inside one file |
| `grep -R "TODO" .` | Search every file, recursively |
| `rg "TODO"` | Same idea, but fast — ripgrep |
| `which node` | Find out where a command actually lives |

If you're working in a large codebase, `rg` (ripgrep) will save you real time over plain `grep`.

---

## 4. Pipes & Redirection

This is where the terminal stops being a list of commands and starts being a toolkit.

### Pipes

`|` feeds the output of one command straight into the next.

`ls -la | grep ".json"`

Mental model: **command → output → next command.**

Instead of one giant tool that does everything, you chain small tools that each do one thing well.

### Redirecting output

`>` sends output into a file (overwriting it).

`echo "hello" > file.txt`

`>>` does the same, but appends.

`echo "another line" >> file.txt`

---

## 5. Git

Even if you mostly click around Git in your IDE, these need to be second nature.

| Command | What it does |
| --- | --- |
| `git status` | See what's changed |
| `git diff` | Look at the actual changes |
| `git add .` | Stage changes |
| `git commit -m "message"` | Commit staged changes |
| `git log` | Browse commit history |
| `git branch` | List branches |
| `git switch branch` | Switch to a branch |
| `git pull` | Pull down remote changes |
| `git push` | Push your commits |
| `git restore file` | Undo local changes to a file |

### 🔑 Concept: Never trust, always verify

When an AI agent touches your repo, these two commands are your seatbelt:

`git status` and `git diff`

Run them. Every time. They tell you exactly what actually changed before you commit to it.

---

## 6. Running Programs

At some point, development is just running commands.

JavaScript: `node app.js`, `npm run dev`

Python: `python app.py`

Other stacks have their own version of the same idea:

`cargo run` · `go run .` · `dotnet run`

You don't need to memorize all of them. You need to understand that your IDE's "Run" button is usually just a shortcut for exactly this.

---

## 7. Package Managers

Know the package manager for whatever ecosystem you're in.

**JavaScript**

`npm install` · `npm install package-name` · `npm run dev`

You'll also run into `pnpm` and `yarn`.

**Python**

`pip install package`, and increasingly, `uv`

Across all of them, understand:

- dependencies
- lockfiles
- version pinning
- global vs. project-level installs

---

## 8. Processes

Anything you launch from the terminal becomes a **process**.

| Command | What it does |
| --- | --- |
| `ps` | List running processes |
| `ps aux` | List them with full detail |
| `top` | Watch processes live |
| `kill PID` | Ask a process to stop |
| `kill -9 PID` | Force it to stop |

And the shortcut you'll use more than any of these:

`Ctrl + C` — stops whatever's currently running in your terminal.

---

## 9. Environment Variables

You'll run into these constantly.

`export API_KEY="..."`

That lets your app read a value at runtime instead of hardcoding it into your source.

You'll also live in `.env` files, which usually look like:

```
DATABASE_URL=...
API_KEY=...
PORT=3000
```

### ⚠️ Keep secrets out of Git

That's exactly why `.gitignore` almost always has a line for `.env`. Don't be the reason it doesn't.

---

## 10. Permissions

On Unix-like systems, every file carries permissions.

`chmod +x script.sh` makes a script executable.

`sudo` runs a command with elevated privileges.

### ⚠️ Don't rubber-stamp `sudo`

If a tutorial, a Stack Overflow answer, or an AI agent tells you to slap `sudo` in front of something, stop and understand *why* it needs that power before you grant it.

---

## 11. SSH

SSH is how you securely reach into another machine from your terminal.

`ssh user@server`

Once you're in, you're working in that machine's shell as if you were sitting at it.

You'll lean on this constantly for servers, cloud infrastructure, remote dev environments, and VMs.

---

## 12. Command History & Speed

You shouldn't be retyping commands all day.

`↑ / ↓` — cycle through past commands

`Ctrl + R` — search your history

`Tab` — autocomplete commands and paths

`history` — list everything you've run

Small habits, big speed difference.

---

# 🧠 Concepts Beat Command Memorization

Don't try to cram 100 commands into your head. Understand these ideas instead:

**Files & directories** — how your filesystem is actually organized

**Paths** — relative vs. absolute

**Processes** — programs are things that start, run, and stop

**Environment variables** — how config and secrets reach your app without living in your code

**Permissions** — who's allowed to read, write, or execute what

**Standard input/output** — commands take input and produce output

**Pipes** — chaining commands together instead of one command doing it all

**Exit codes** — every command reports back whether it worked

**Git** — inspecting, staging, committing, reverting, syncing

---

# 🤖 Why This Matters More Because of AI Agents

Tools like Claude Code and Codex can now:

- explore your repo
- read and edit files
- search your codebase
- install dependencies
- run builds and tests
- execute git commands
- spin up dev servers
- drive other CLI tools

You don't have to type every one of those commands by hand anymore.

But you still need to **understand what's happening when the agent does.**

If it wants to run `rm -rf ...` — you should know exactly why that's a red flag.

If it just touched 14 files — you should know to run `git diff` before you trust it.

If your server won't die — you should understand processes.

If your app can't find an API key — you should understand environment variables.

If something fails with a permissions error — you should know what that actually means.

AI shrinks how much syntax you need to memorize. It doesn't shrink how much you need to understand your own environment. If anything, it raises the bar — because now you're not just running the commands, you're auditing them.

---

# ✅ If You're Starting From Zero

Learn these first:

`pwd` · `ls` · `cd` · `mkdir` · `touch` · `cp` · `mv` · `rm` · `cat` · `grep` / `rg` · `find` · `clear`

Then:

`git status` · `git diff` · `git add` · `git commit` · `git pull` · `git push`

Then understand:

`|` · `>` · `>>` · `Ctrl + C` · environment variables · paths · processes · permissions

You don't need to memorize every line on this page. You need to know what these tools *can* do, understand the concepts underneath them, and look up the exact syntax when you actually need it.

That's enough to be genuinely comfortable in a terminal — and far better equipped to work alongside AI coding agents instead of just watching them work.

---

*Part of a weekly resource drop — new sheet every week. Follow along or check back for updates.*
