# 🕸️ The Terminal Knowledge Graph

### Every command is a node. Learn how they connect, and the terminal stops being a black box.

I'm done calling these "cheat sheets." Cheating means skipping past the understanding, and that's the opposite of what this is. Think of it as a graph instead: a web of connected ideas where `pwd` leads you to paths, paths lead you to processes, processes lead you to permissions, and permissions are what stop you from doing something you'll regret at 1am.

Building with an AI agent in the driver's seat is genuinely fun. It's fast, it feels a little like magic, and sooner or later it's going to try to run a command you don't fully understand. None of that is a problem. The fun and the "know what you're doing" part work together, not against each other. The second one is what makes the first one safe.

Below is my current map of that graph, the nodes I think every developer should have wired in before handing an agent the keyboard.

---

## Node 1: Knowing Where You Are

Everything else in this graph depends on this one. If you don't know your current location, you can't reason about what a command is actually about to touch.

| Command | What it does |
| --- | --- |
| `pwd` | Print your current location |
| `ls` | List what's in the current folder |
| `ls -la` | List everything, hidden files included |
| `cd folder` | Step into a folder |
| `cd ..` | Step up one level |
| `cd ~` | Jump home |
| `cd -` | Return to wherever you just came from |
| `clear` | Clear the screen, not your history |

### The path node

Paths are how every other node here connects back to this one, and they come in two flavors.

`./src/app.js` is relative. It means "starting from wherever I'm standing right now."

`/Users/you/project/src/app.js` is absolute. It means "this exact spot, regardless of where you started."

Shorthand worth memorizing: `.` is here, `..` is one level up, `~` is home, `/` is the root everything else branches from.

---

## Node 2: Making, Moving, and Deleting Files

| Command | What it does |
| --- | --- |
| `touch file.txt` | Create an empty file |
| `mkdir folder` | Create a folder |
| `mkdir -p a/b/c` | Create a nested path in one go |
| `cp file copy.txt` | Copy a file |
| `cp -r folder copy` | Copy a folder |
| `mv old.txt new.txt` | Move or rename |
| `rm file.txt` | Delete a file |
| `rm -r folder` | Delete a folder |
| `cat file.txt` | Print a file's contents |
| `less file.txt` | Page through a file one screen at a time |

### The one edge that doesn't reverse

Almost everything in this graph can be undone if you're paying attention. This is the exception. There's no trash bin catching `rm -rf` if it lands on the wrong folder. Check the path twice before you check the command.

---

## Node 3: Search, or How to Find a Needle Without Reading the Whole Haystack

| Command | What it does |
| --- | --- |
| `find . -name "*.js"` | Find files matching a pattern |
| `grep "TODO" file.txt` | Search inside one file |
| `grep -R "TODO" .` | Search everything, recursively |
| `rg "TODO"` | The same search, much faster (ripgrep) |
| `which node` | Find out where a command actually lives |

Once a codebase has more than a few hundred files, `rg` starts pulling ahead of plain `grep`. Worth having installed from day one.

---

## Node 4: Pipes and Redirection, the Edges That Tie It All Together

This is the node that turns a pile of separate commands into an actual graph. Pipes and redirects are the connective tissue.

### Pipes: one command's output feeds the next command's input

`ls -la | grep ".json"`

Read it left to right: command, then output, then the next command. You get to chain small, focused tools together instead of relying on one tool that tries to do everything.

### Redirection: output lands in a file instead of on screen

`echo "hello" > file.txt` writes to the file (and overwrites whatever was there).

`echo "another line" >> file.txt` appends instead of overwriting.

---

## Node 5: Git, the Version Graph You Already Understand

If you've ever clicked around Git inside an IDE, you already get the concept. These are just the commands sitting underneath those clicks.

| Command | What it does |
| --- | --- |
| `git status` | See what's changed |
| `git diff` | See the actual line-by-line changes |
| `git add .` | Stage changes |
| `git commit -m "message"` | Commit what's staged |
| `git log` | Browse commit history |
| `git branch` | List branches |
| `git switch branch` | Switch branches |
| `git pull` | Pull down remote changes |
| `git push` | Push your commits |
| `git restore file` | Undo local changes to a file |

### The guardrail node

If an agent has write access to your repo, this habit isn't optional. Run `git status` and `git diff` before anything gets committed, every single time. Not because the agent can't be trusted. Because you should always know exactly what "done" changed before you sign off on it.

---

## Node 6: Actually Running Programs

At some point, development just comes down to running a command and watching what it does.

JavaScript: `node app.js`, `npm run dev`

Python: `python app.py`

Every other ecosystem rhymes with these: `cargo run`, `go run .`, `dotnet run`

You don't need to memorize the full list. You just need to recognize that your IDE's "Run" button is a shortcut for one of these.

---

## Node 7: Package Managers, or How Dependencies Join the Graph

**JavaScript**: `npm install`, `npm install package-name`, `npm run dev` (you'll also run into `pnpm` and `yarn`)

**Python**: `pip install package`, and increasingly, `uv`

Whichever one you're using, the same underlying ideas apply: dependencies, lockfiles, version pinning, and the difference between a global install and a project-scoped one.

---

## Node 8: Processes, or What Happens the Moment You Hit Enter

Launch something from a terminal and it becomes a **process**, a living thing with its own lifecycle, not just a line of text that fired once and disappeared.

| Command | What it does |
| --- | --- |
| `ps` | List running processes |
| `ps aux` | List them with full detail |
| `top` | Watch processes live |
| `kill PID` | Ask a process to stop |
| `kill -9 PID` | Force it to stop immediately |

And the edge you'll cross more than any other: `Ctrl + C`, which stops whatever's currently running in front of you.

---

## Node 9: Environment Variables, or Config Without Hardcoding

`export API_KEY="..."` lets your application read a value at runtime instead of baking it directly into the source code.

You'll spend a lot of time in `.env` files for exactly this, usually shaped like:

```
DATABASE_URL=...
API_KEY=...
PORT=3000
```

### The node guarding your secrets

This is exactly why `.gitignore` almost always excludes `.env`. One careless commit and a secret is part of your public history forever. Check what you're staging before you run `git add .`.

---

## Node 10: Permissions, or Who's Allowed to Do What

Every file on a Unix-like system carries permissions: who can read it, write it, or run it.

`chmod +x script.sh` makes a script executable.

`sudo` runs a command with elevated privileges, effectively as root.

### Don't cross this edge without looking

If a tutorial, a forum post, or an agent tells you to slap `sudo` in front of something, pause before you comply. Understand exactly why it needs that level of access first. This is the one node in the whole graph capable of affecting more than just your project.

---

## Node 11: SSH, Extending the Graph Beyond Your Own Machine

`ssh user@server` reaches securely into another computer and drops you straight into its shell, as if you were sitting in front of it.

This is how the graph stretches past your laptop, into servers, cloud infrastructure, remote dev environments, and virtual machines.

---

## Node 12: Moving Faster Through the Graph

`↑ / ↓`: cycle through past commands

`Ctrl + R`: search your history

`Tab`: autocomplete commands and paths

`history`: list everything you've run

None of these teach you anything new. They just cut down how much time you spend retyping what you already know.

---

# 🧠 The Graph Underneath the Commands

Memorizing a hundred individual commands is the wrong target. Understanding the handful of concepts that connect all of them is the real one:

**Files & directories**: how your filesystem is actually organized

**Paths**: relative versus absolute, and which one you're using right now

**Processes**: programs as things that start, run, and stop

**Environment variables**: how config and secrets reach an app without living inside its code

**Permissions**: who's allowed to read, write, or execute what

**Standard input/output**: every command takes input and produces output

**Pipes**: chaining small tools together instead of leaning on one giant one

**Exit codes**: every command reports back whether it actually worked

**Git**: inspecting, staging, committing, reverting, syncing

Learn these nine well, and any new command you run into will slot neatly into a spot you already understand.

---

# 🤖 Why This Graph Matters More With an Agent at the Wheel

Here's the part that changed things for me. Agents like Claude Code and Codex can now explore a repo on their own, read and edit files, search a codebase, install dependencies, run builds and tests, execute git commands, spin up dev servers, and drive other CLI tools.

It's a genuinely fun way to build. Watching a feature come together in minutes instead of hours doesn't get old fast. But fun and careless aren't the same thing, and the gap between them is exactly this knowledge graph.

If an agent wants to run `rm -rf ...`, you should already know why that deserves a second look.

If it just touched fourteen files, `git diff` is how you find out what "done" actually means before you trust it.

If a server won't die, that's a processes question, not a mystery.

If an app can't find an API key, that's an environment variable, not a bug.

If something fails on permissions, you should know exactly what just got blocked and why.

Agents cut down how much syntax you need to type. They don't cut down how much you need to understand. If anything, they raise the bar, because now you're not just typing the commands, you're auditing them.

---

# The Starting Nodes, If You're New to All This

Wire these in first:

`pwd`, `ls`, `cd`, `mkdir`, `touch`, `cp`, `mv`, `rm`, `cat`, `grep` / `rg`, `find`, `clear`

Then:

`git status`, `git diff`, `git add`, `git commit`, `git pull`, `git push`

Then understand, don't just memorize:

`|`, `>`, `>>`, `Ctrl + C`, environment variables, paths, processes, permissions

You're not going to remember every line on this page, and that's fine. What you need is the shape of the graph, what connects to what, so you can look up the exact syntax the moment you need it, and recognize when to pump the brakes on something an agent is about to run for you.

That's the real difference between watching an agent build your project and actually building it alongside one.

---

## How This Actually Gets Made

Quick note on process, since it matters to me that this is honest: the research, the opinions, and the way I want to explain things are mine. I use Claude and Codex to help me get those ideas onto the page more clearly, and I'll be leaning on Claude specifically to push most of these updates to GitHub each week, since that part of the workflow is what used to slow me down. The thinking behind every resource here is my own.

---

*Node one of a weekly series. A new piece of the graph drops every week.*
