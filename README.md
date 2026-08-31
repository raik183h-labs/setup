# RAIK183H Setup Guide

Everything you need to write, run, and turn in code for this course.

**Do [Part 1](#part-1--one-time-setup) once, ever.** After that, starting a lab
is a single command.

- [Part 1 — One-time setup](#part-1--one-time-setup)
- [Part 2 — Every lab](#part-2--every-lab)
- [Part 3 — When something goes wrong](#part-3--when-something-goes-wrong)

---

# Part 1 — One-time setup

## ✅ Step 1: Get Your Editor

**Either Cursor or VS Code works for this course.** Everything in this guide,
every course command, and every extension works the same in both — pick one and
stick with it.

- **Cursor** is an AI-assisted editor built on VS Code. Its free tier is all you
  need. This is what your instructor demonstrates in class.
- **VS Code** is Microsoft's editor. Free, and the more transferable skill.

Wherever this guide says "your editor," it means whichever one you installed.

### 1a. Install It

**If you chose VS Code:** download from
[code.visualstudio.com](https://code.visualstudio.com), run the installer, and
skip to **1c**. No account needed.

**If you chose Cursor**, make an account first:

1. Go to [https://cursor.com](https://cursor.com)
2. Click "Sign Up" or "Get Started"
3. Choose "Sign up with email"
4. Enter your school email address
5. Create a password
6. Verify your email address

### 1b. About Paid Plans *(Cursor only — you don't need one)*

**You do not need to pay for anything in this course.** Cursor's free tier covers everything in this guide and everything we do in class.

You may see older blog posts or videos advertising "a free year of Cursor Pro for students." **That program has ended** and there is no longer a student verification page. Don't go looking for it — you'll just hit a dead end.

If any course credits or event promotions become available, your instructor will tell you in class.

### 1c. Download and Install Cursor *(Cursor only)*

1. After creating your account, you'll be taken to the download page
2. Click the big "Download" button
3. Install Cursor on your computer:
   - **Mac**: Double-click the downloaded file, then drag Cursor to your Applications folder
   - **Windows**: Double-click the downloaded file and follow the installation wizard
   - **Linux**: Extract the file and run the installer

### 1d. Sign In to Cursor *(Cursor only)*

1. Open Cursor from your Applications/Programs menu
2. Sign in with the email and password you created
3. You should see a welcome screen - you're all set!

### 1e. Install the Shell Command — do not skip this

This is what lets the course tools open your editor and install your extensions.
It takes ten seconds and saves a lot of pain later.

1. Open your editor and press `Cmd + Shift + P` (Mac) or `Ctrl + Shift + P` (Windows)
2. Type **shell command**
3. Run **Install 'cursor' command** (Cursor) or
   **Shell Command: Install 'code' command in PATH** (VS Code)
4. **Close your terminal and open a new one**

Check it worked — one of these should print a version:

```
cursor --version
code --version
```

---

## ✅ Step 2: Install Java (Required!)

Before you can run your Java program, you need to install Java on your computer. Don't worry - it's free and easy!

### 2a. Download Java Development Kit (JDK)

1. Go to [https://adoptium.net](https://adoptium.net)
2. The site should detect your operating system automatically
3. Download the **LTS** version it recommends

### 2b. Install Java

**Mac:**

- Open the downloaded `.pkg` file
- Follow the installation wizard
- Click "Install" when prompted

**Windows:**

- Open the downloaded `.msi` file
- Click "Next" through the installation
- Click "Install" when ready

> ⚠️ **Windows:** if the installer offers a checkbox like **"Set JAVA_HOME
> variable"** or **"Add to PATH"**, turn it on. If you miss it, Java installs
> but your terminal can't find it — see
> [Fixing your PATH](#fixing-your-path).

### 2c. Verify Java is Installed

1. Open **Terminal** (Mac) or **Git Bash** (Windows — you'll install it in Step 3)
2. Type `java -version` and press Enter
3. You should see a few lines starting with something like `openjdk 25.0.1` - the exact version number will depend on whichever LTS release is current when you download it. **Any version number means Java is working!**

If instead you see "command not found" or "not recognized", Java didn't install
correctly — go back to 2b or see [Fixing your PATH](#fixing-your-path).

---

## ✅ Step 3: Install Git and the Course Tools

Your labs live on GitHub. These four things get them onto your computer.

### 3a. Install Git

**Mac** — open **Terminal** (`Cmd + Space`, type `Terminal`) and run:

```
git --version
```

If you see a version number, you already have it. If a box offers to install
"command line developer tools", click **Install** and wait.

**Windows** — download from
[git-scm.com/downloads](https://git-scm.com/downloads) and run the installer.
**Accept every default.** This also installs **Git Bash**, which is the terminal
you'll use for the rest of this guide.

### 3b. Install the GitHub CLI

**Mac:**

```
brew install gh
```

No Homebrew? Grab the installer from [cli.github.com](https://cli.github.com).

**Windows** — in **PowerShell**:

```
winget install --id GitHub.cli -e --source winget
```

> ⚠️ **Close every terminal window and open a new one after installing.** A
> window that was already open won't find the new command. This is the single
> most common reason "it doesn't work."

### 3c. Install the Course Command

In **Terminal** (Mac) or **Git Bash** (Windows):

```
gh extension install raik183h-labs/gh-lab
gh extension install raik183h-labs/gh-homework
```

One gives you `gh lab`, the other `gh homework`.

### 3d. Sign In to GitHub

```
gh student login
```

Choose **GitHub.com**, then **HTTPS**, then **Login with a web browser**. Copy
the code it shows, press Enter, and approve it in the browser.

> ⚠️ **Use `gh student login`, not `gh auth login`.** They look
> interchangeable and they are not. Plain `gh auth login` grants fewer
> permissions than the classroom needs, and you won't find out until it fails
> to start a lab. If you already ran `gh auth login`, just run
> `gh student login` now — it fixes it.

This also lets your editor push your work without ever asking for a password.

### 3e. Accept Your GitHub Invitation

Check your **email** (including spam) for an invitation to the course GitHub
organization and accept it. If you never got one, message your instructor your
**GitHub username** on Slack.

---

## ✅ Step 4: Check That It All Worked

```
gh lab --check
```

Everything should be green. Anything red tells you what to fix, and
[Part 3](#part-3--when-something-goes-wrong) covers each one.

> If this says `unknown command: lab`, close your terminal, open a new one, and
> try again. That fixes it most of the time.

**You're done with setup.** You never have to do Part 1 again.

---

# Part 2 — Every lab

## ✅ Step 5: Get Your Lab or Homework

Labs are done in **pairs or trios**, and each team shares **one** repository.
Homework you do on your own.

**Homework is individual. Labs are done in teams.** Both start with one
command; the lab command also handles your partner.

> ### 🛑 Do not accept a lab on the GitHub website
>
> Use the `gh lab` command below — nothing else. It puts your whole team in
> **one** repository, which is the only thing that gets graded.
>
> If you accept the lab through the GitHub website instead, you each get your
> own disconnected copy, and only one of them counts. There is no way to merge
> them afterward.
>
> You do **not** have to decide who goes first. Run the command whenever you're
> ready — it sorts itself out.

### 5a. Homework — One Command

```
gh homework homework-3
```

Homework is **individual work**, so it won't ask about a partner. It sets up
your repository, downloads it, and opens it in your editor. Skip to
[Step 6](#-step-6-write-and-run-your-code).

### 5b. Labs — One Command

In **Terminal** (Mac) or **Git Bash** (Windows), go to the folder where you keep
your RAIK183H work, then run the lab name your instructor posted:

```
gh lab lab-loops-1
```

It will ask:

```
Partner's GitHub username (press Enter if working alone):
```

Type your partner's **GitHub username** — not their real name. That's the only
question. It then sets everything up and opens the lab in your editor.

**The first time you run it, it also installs the course extensions** —
SpecStory, Local History, Java language support, and our Checkstyle linter. That
takes an extra minute once and never again.

### 5c. It Doesn't Matter Who Runs It First

Whoever gets there first creates the team's repo. The other one joins it
automatically — no waiting, no clicking, no deciding in advance.

- **Partner already started?** Yours joins their repo.
- **You start first?** Yours creates it and adds them.
- **Both at the exact same moment?** It sorts itself out: whichever repo was
  created first is the one you'll both end up in. You might see a note that it
  switched you over. Nothing is lost — this happens before you've written any
  code.

You never have to visit GitHub or click a notification.

**If your partner isn't here**, press Enter at the partner question and work
alone for now. Tell your instructor so they can sort out the pairing.

**Safe to re-run any time.** If you close the terminal, get lost, or want to
pick your work back up the next day, run the same command again.

### 5d. If It Didn't Open Automatically

`gh lab` prints the folder path instead — open that folder in your editor by hand
(**File → Open Folder**). Your work is already downloaded; nothing is lost.

To fix it for next time, do [Step 1e](#1e-install-the-shell-command--do-not-skip-this).

---

## ✅ Step 6: Write and Run Your Code

Your lab repository already contains a `README.md` telling you what to build,
and the course AI rules. Read the README first.

### 6a. Run Your Program

1. Look for a small "Run" button (▶️) above your code or in the top-right corner
2. Click on it, or press `F5`
3. Your editor will compile and run your Java program automatically

**What happens:** The Java extension will compile your code and show the output!

**If the play button doesn't work:**

1. **Check the bottom status bar** - Look for any error messages in red
2. **Try restarting your editor** - Close and reopen it completely
3. **Check Java installation** - Make sure Java is properly installed (Step 2)
4. **Verify file extension** - Your file must end with `.java`
5. **Ask for help** - If nothing works, raise your hand and ask your instructor!

**Alternative way to run:** right-click anywhere in your `.java` file, look for
"Run Java" in the context menu, and click it.

### 6b. See Your Results

If everything works correctly, you should see:

- A new panel at the bottom called "Output" or "Terminal"
- Your program's output displayed (after a complicated-looking command)

---

## ✅ Step 7: Use the AI to Learn

### 7a. The Course AI Rules

Your lab repository ships with the course AI rules already in it, so the
assistant knows to teach you rather than hand you finished code. You don't have
to set anything up.

This repository also has a copy in [`AGENTS.md`](AGENTS.md) — that filename is a
shared standard that most AI coding tools understand, so you can drop it into any
project where you want the same behavior.

### 7b. Open the AI Chat Panel

1. Look for the AI Chat icon on the left sidebar (looks like a chat bubble or message icon)
2. Click on it to open the AI chat panel
3. You should see a chat interface where you can talk to the AI

### 7c. Ask the AI for Help

**What to expect:** The AI will:

- Explain programming concepts in simple terms
- Give you small examples to understand
- Guide you through learning one concept at a time
- Ask you to explain what you understand before moving forward

**For beginners:** Don't ask for complete solutions! Ask for explanations of concepts first.

1. **Start small** - "How do I make my program print my name?"
2. **Ask for small examples** - "Can you show me a simple example of this?"
3. **Explain back** - Tell the AI what you think you understand
4. **Build gradually** - Add one feature at a time

**Remember:** It's okay to not know everything! The AI is here to teach you step by step.

**Check that it's working:** ask the AI `"What rules are you following for this
project?"` It should mention the CS1 tutor rules — things like the Comprehension
Gate, or not giving full solutions. If it doesn't, tell your instructor.

---

## ✅ Step 8: Turn It In

Write your code as usual. To turn in your work:

1. Click the **Source Control** icon in the left sidebar (the branching-path icon)
2. Type a short message describing what you did — e.g. `finished part 1`
3. Click **✓ Commit**
4. Click **Sync Changes** (or **Push**)

**Pushing is turning it in.** There is no separate submit button, no screenshot,
and no upload. You can push as many times as you like — we look at your most
recent work.

**Everyone on the team gets the same grade**, based on the team repository. It
doesn't matter whose computer the code was pushed from.

**How to know it worked:** open the repository on github.com and check that your
latest changes are there.

---

## ✅ Step 9: Working Together Without Stepping on Each Other

Since you share one repository, get in the habit of:

1. **Pull before you start.** In the Source Control panel, click the `…`
   menu → **Pull**. This grabs your teammate's latest work.
2. **Push when you stop.** Don't sit on finished work — your teammate can't see
   it until you push.

If your editor warns about a conflict, don't panic and don't force anything — grab a
TA. Conflicts are normal and quick to fix once you've seen one.

> **Easiest way to avoid conflicts entirely:** work together on one screen, or
> agree on who is editing which file before you split up.

---

# Part 3 — When something goes wrong

**Start here, every time:**

```
gh lab --check
```

(`gh homework --check` does the same thing.) This prints your setup and marks
anything broken in red. If you're asking a TA
for help, run this first and show them the output — it answers most of the
questions they'd otherwise have to ask you.

---

## "command not found" / "'gh' is not recognized"

This is the **single most common problem**, and it almost never means the
install failed. It means your terminal doesn't know where to look yet.

**Try this first, and it fixes it most of the time:**

> **Close every terminal window and open a new one.** Not a new tab — a whole
> new window. A terminal only learns about newly-installed programs when it
> starts up.

If you have Cursor or VS Code open, **quit and reopen the whole app** too. Its
built-in terminal inherited the old settings when the app launched.

Still not found? Then it really isn't on your PATH — see the next section.

---

## Fixing your PATH

Your PATH is the list of folders your computer searches when you type a command.
If a program isn't in one of those folders, your terminal says "not found" even
though the program is sitting right there on your disk.

**First, see what your computer thinks:**

| Where you are | Command |
|---|---|
| Mac Terminal | `echo $PATH` |
| Windows **Git Bash** | `echo $PATH` |
| Windows **PowerShell** | `$env:PATH -split ';'` |
| Windows **Command Prompt** | `echo %PATH%` |

And to find out whether a program exists at all:

| | Mac / Git Bash | PowerShell |
|---|---|---|
| Where is it? | `which gh` | `where.exe gh` |

**Windows — adding a folder to your PATH**

1. Find the program's folder in File Explorer. For Java this is the **`bin`**
   folder inside the JDK — go **all the way into `bin`**, not the folder above
   it. That is the mistake people make.
2. Click the address bar and copy the full path.
3. Press the **Windows key**, type `environment variables`, and open **Edit the
   system environment variables**.
4. Click **Environment Variables…**
5. Under **System variables**, select **Path**, click **Edit**, then **New**,
   and paste.
6. **OK** out of all three windows.
7. **Open a brand-new terminal window** and try again.
8. Still nothing? **Restart your computer.** Windows sometimes won't pick up
   the change until it does. This is annoying and it is not your fault.

**Mac — `brew` itself isn't found**

On Apple Silicon Macs Homebrew installs to a folder that isn't searched by
default. Run:

```
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```

Then close the terminal, open a new one, and try `brew --version` again.

---

## `gh lab` or `gh homework` isn't a thing / "unknown command"

The extension didn't install. Run:

```
gh extension install raik183h-labs/gh-lab
gh extension install raik183h-labs/gh-homework
```

One gives you `gh lab`, the other `gh homework`.

If that errors, run `gh auth status` — you have to be signed in first.

---

## Windows: which terminal do I run these in?

**Git Bash.** Search your Start menu for it. `gh lab` and `gh homework` are
Bash programs and will not run correctly in PowerShell or Command Prompt.

Use PowerShell only for the one `winget install` line in the setup steps.

---

## "Couldn't start '<lab>'. Have you accepted your invitation to github.com/…"

You're not in the course GitHub organization yet.

1. Check your **email** (including spam) for an invitation to the organization
   and accept it.
2. No invitation? Message your instructor your **GitHub username** on Slack.
   A few people never submitted theirs.
3. Already accepted it? Visit the organization named in the error message
   (`github.com/...`) while signed in and confirm you can see it. If you're signed into a *different* GitHub
   account in your browser than the one `gh` is using, that will do it —
   compare `gh api user --jq .login` against the account shown on github.com.

---

## "There's no GitHub user called 'Alex Kim'"

The command wants your partner's **GitHub username** — the short one from their
profile URL, like `akim42`. Not their real name, not their email, not their
NUID. Have them read it off their own GitHub page.

Typing `@akim42` or pasting `github.com/akim42` is fine — those get cleaned up.

---

## "No invitation from <partner> yet"

Your partner started the repo but the invite hasn't reached you yet. Wait about
ten seconds and run the same command again. If it still fails after two tries,
have your partner run their command again — that re-sends it.

---

## "You and <partner> started at the same moment"

Nothing is wrong. You both ran the command in the same breath, so two repos got
created. The command picked the one that was created first and moved you into
it, before either of you wrote any code.

Keep working. Your instructor deletes the leftover empty one.

---

## It didn't open my editor

`gh lab` prints the folder path instead. Open that folder yourself:
**File → Open Folder**. Your work is already downloaded — nothing is lost.

To fix it permanently, do [Step 1e](#1e-install-the-shell-command--do-not-skip-this).
Then close and reopen your terminal. `cursor --version` (or `code --version`)
should now answer.

---

## Sign-in problems

`gh student login` → **GitHub.com** → **HTTPS** → **Login with a web browser**.
Copy the code, press Enter, paste it in the browser. (Use `gh student login`,
not `gh auth login` — see below.)

If sign-in keeps failing with a vague server error, it is usually a **wrong
password**, not a broken server — the error message lies. Don't keep retrying:
after enough attempts you'll get temporarily locked out, and then you have to
wait it out before you can even reset it. Reset the password instead.

To start completely over: `gh auth logout`, then `gh student login`.

---

## Java: "java is not recognized" or the wrong version

`gh lab` doesn't need Java, but your lab code does. Check with:

```
java -version
```

If that fails, the JDK either isn't installed or its `bin` folder isn't on your
PATH — see [Fixing your PATH](#fixing-your-path), and note that you must add the path all
the way down to `bin`.

---

## My editor says it can't push / asks for a password

You signed into `gh` but not into Git itself. Run:

```
gh auth setup-git
```

Then try the push again.

---

## "Updates were rejected" when pushing

Your partner pushed something you don't have yet. In the Source Control
panel, click the `…` menu → **Pull**, then push again.

If it reports a **conflict**, stop and get a TA. Don't force anything and
don't delete the folder — conflicts are normal and take about two minutes to
fix with someone who's seen one.

---

## I think I broke it / I want to start clean

Your work lives on GitHub once you've pushed, so this is safe **if you've
pushed**:

```
gh lab <the-lab-name>
```

Run it from a different folder and it will download a fresh copy. If you have
unpushed work you care about, get a TA before deleting anything.

---

## "permissions incomplete" / it won't start a lab

Run:

```
gh student login
```

`gh auth login` on its own doesn't request everything the classroom needs, so
if you signed in that way, starting a lab fails. `gh student login` is the same
browser flow with the right permissions — you only ever do it once.

You do **not** need this to *join* a lab your partner already started. It's only
required by whoever starts it.

---

## The course extensions didn't install

`gh lab` installs SpecStory, Local History, Red Hat's Java support, and our
Checkstyle linter the first time you run it. If it couldn't:

**Most likely cause:** there's no `cursor` (or `code`) command on your PATH, so
`gh lab` can't talk to your editor. Go back and do
[Step 1e](#1e-install-the-shell-command--do-not-skip-this), then close and
reopen your terminal and run `gh lab` again.

**To install them by hand instead** — Extensions icon in the left sidebar, then
search for and install:

- `SpecStory`
- `Local History`
- `Language Support for Java(TM) by Red Hat`

**Checkstyle is different in Cursor.** Cursor installs extensions from a
registry called Open VSX, and Checkstyle isn't published there — so it ships as
a file. **VS Code users can skip this** and just install **Checkstyle for Java**
from the Extensions panel like any other extension.

To install the file in Cursor:

1. Download [`CheckstyleForJava.vsix`](CheckstyleForJava.vsix) from this repository (click the file, then click "Download")
2. Extensions panel → **`...`** menu → **Install from VSIX…**
3. Pick the file you downloaded

---

## No Run button on my Java file

The Java extension isn't installed or Java itself isn't set up. Check
`java -version` first (see above), then confirm **Language Support for Java** is
in your Extensions list. Your file also has to end in `.java`.

---

## Nothing here helped

Run `gh lab --check`, copy **all** of the output, and bring it to your
instructor or a TA — in person, on Slack, whatever's faster. Include what you
typed and what it said back. Don't spend more than ten minutes stuck; that's
what we're here for.

---

# Appendix: Practice on Your Own

Want to try Java outside of a lab? Make a folder anywhere, open it in your editor
(**File → Open Folder**), create a file named `HelloWorld.java`, and type this
in **by hand** — don't copy and paste, that's the whole point:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

Check that:

- You have the `.java` extension on your filename
- There are no extra spaces or typos
- All the brackets `{` and `}` match up

Then run it the same way as [Step 6a](#6a-run-your-program).

---

_If you have any trouble with these steps, raise your hand in class or ask your
instructor for help._
