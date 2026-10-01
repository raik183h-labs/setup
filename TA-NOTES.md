# `gh lab` — TA notes

Supplement to the course guide at **`raik183h-labs/setup`** (public README,
Part 3 "When something goes wrong" covers 30 student-facing cases). Students
should be sent there, not here.

This page holds only what that guide doesn't: mechanism a TA needs in order to
diagnose, where the student-facing symptom is misleading. Verified against
`gh-lab` @ `d3560967`, 2026-09-30.

---

## Three failures whose symptom is silence

**1. JUnit — the hamcrest trap.** `lib/*.jar` must be the *console-standalone*
JUnit jar, which shades in hamcrest. A plain `junit-4.12.jar` **compiles fine
and then dies at run time**:

```
ClassNotFoundException: org.hamcrest.SelfDescribing
```

Eclipse supplied hamcrest invisibly; Cursor does not. A student whose tests
compile but explode on run has the wrong jar, not broken code. `--check`
catches a *missing* jar ("JUnit library MISSING from lib/"); a *wrong* jar is a
run-time surprise it cannot see.

**2. Checkstyle — a broken pointer is indistinguishable from clean code.**
Every rule in `raik-style.xml` is `severity=warning`. A missing or misspelled
`java.checkstyle.configuration` therefore produces **no errors and no
warnings**. So "the linter says my code is fine" may mean the linter is not
running. The guide's "I don't see the yellow squiggly lines" section handles
this for students; the detail TAs need is *why* it is silent rather than loud,
and that `gh lab <name>` rewrites the pointer on every run — so re-running the
assignment is the fix, and a student's hand edits to
`.vscode/settings.json` do not survive it.

`${workspaceFolder}` is the only variable the extension expands.

**3. The ruleset is a live URL, so there is no offline linting.** It is read
from `raw.githubusercontent.com/raik183h-labs/setup/main/raik-style.xml`.
Deliberate tradeoff: one place to edit course style, at the cost of silence
without a network. Same symptom as the two above.

> Possible wording fix in the guide: the squiggly-lines section says the rules
> are "downloaded from a link the first time," which reads as cached. Worth
> confirming whether the extension caches or re-fetches, since it changes the
> offline advice.

---

## `couldn't update — ask a TA` means local commits

This is a bare `git pull --ff-only` whose only failure output is that string.
It had two causes; one has since been split out:

- *Assignment was re-released* — now detected separately and reported as "this
  assignment was replaced after you downloaded it," with the old copy **moved**
  to `<name>-old` rather than clobbered.
- *The student has local commits* — **still has no message of its own, so this
  is now almost certainly what the string means.**

Diagnose it as the second:

```
git -C <assignment folder> status
git -C <assignment folder> log --oneline origin/main..HEAD
```

Non-empty log = unpushed commits. **Push them.** Do not reset, do not
re-clone — their work is in those commits.

---

## Automatic repairs, so you can say "run it again" with confidence

These print a red line and then fix themselves. A student showing you one of
these is usually already fine:

| Printed | What happened |
|---|---|
| `the copy you have is empty — repairing it` | clone landed before GitHub copied the starter files |
| `your files didn't unpack properly — repairing it` | checkout aborted mid-way; on Windows, a path containing a forbidden character. HEAD resolves fine, so only a whole-tree check catches it. Repaired by `fetch` + `reset --hard`, and only when *every* tracked file is missing — so there is no work to lose |
| `this assignment was replaced after you downloaded it` | re-released assignment shares no commits with the copy on disk; git calls the histories unrelated and refuses every pull |

**The empty-repo timing window.** GitHub creates the repo and copies the
starter files *seconds later*, and both `git clone` and `git pull` **exit 0 on
an empty repo** — nothing looks wrong and re-running appears not to help. The
script polls for content for up to 30s before cloning and re-checks after. A
student reporting "it downloaded but the folder is empty" either gave up during
that wait or hit it before the guards existed.

**Nothing is ever deleted.** Superseded folders go to `<name>-old`, then
`-old-2`, `-old-3`. Source comment: "Move, never delete."

**Duplicate downloads are prevented on purpose.** Before downloading, the
script searches the course folder, `$PWD`, `$HOME`, `~/Desktop`, `~/Documents`,
then `find $HOME -maxdepth 3`. Rationale in the source: *"Downloading a second
copy is worse than downloading none — work goes into one copy and gets pushed
from neither."*

---

## There is no update command, and students shouldn't be given one

Every invocation runs `self_update()`: compares local extension HEAD against
`git ls-remote origin HEAD`, and on a difference runs `gh extension upgrade
lab` then `exec`s itself with `RAIK_UPDATED=1`. Consequences:

- Students are on current code from their second run onward.
- Offline (`ls-remote` returns nothing) is a silent no-op, not an error.
- `RAIK_NO_UPDATE=1` is the escape hatch, but the real fix for a bad version is
  pushing a good one — the next run picks it up.
- At most one re-exec per invocation, so no loop risk.

---

## Open bug: the multi-root workspace and the linter

Every run rebuilds `<course folder>/RAIK183H.code-workspace` from whatever
sibling directories contain a `.git`, and Cursor opens *that* rather than the
single assignment. Checkstyle behaves differently in that multi-root workspace
than with one project open.

The workspace is deliberate — one window for the whole course, documented in
the guide's Step 3f. **So this is a real open bug, not student error. Don't
tell students they opened it wrong.**

Rebuilt from disk each run, so it self-repairs if mangled and drops entries for
deleted folders.

---

## Escalate rather than improvise

- Windows blocking `gh student` — needs a Defender exclusion. **Never** have a
  student disable Defender.
- A posted slug missing from `assignments.json` (served statically from
  `https://<org>.github.io/classroom50/<classroom>/assignments.json`) — that's
  an instructor-side fix, not a student one.
- Student not on the classroom roster (`Couldn't add <partner> — are they
  enrolled?`).
- `Couldn't get access to <partner>'s repo.`
- Checkstyle running but silent on code you know is non-compliant — see the
  three silent failures above.

---

## Two details only relevant if you debug the script itself

**`gh api repos/<name>` follows GitHub's rename redirect**, returning HTTP 200
describing a *different* repo. The script compares the returned `full_name`
against what it asked for rather than trusting the 200.

**Scopes differ by action.** Only *starting* a repo needs `admin:org`;
*joining* a partner's does not. So the second partner can often proceed while
the first is still fixing permissions.
