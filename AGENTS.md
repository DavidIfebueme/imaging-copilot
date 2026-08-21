# agents.md

## conversational style

- keep answers short and concise. technical prose only, be direct.
- no emojis in commits, issues, pr comments, or code.
- no fluff or cheerful filler ("thanks so much!" and similar get cut).
- when the user asks a question, answer it first. edits and implementation commands come after.
- when responding to feedback or an analysis, state agree or disagree explicitly before saying what you changed.
- if the next action is non-destructive and follows naturally from the request, do it proactively. reserve approval gates for destructive actions and version control history.

## code quality

- read files in full before wide-ranging changes, before editing any file you have not fully inspected, and when asked to investigate or audit. search snippets are not enough for broad changes.
- code stays strictly typed. loosen or drop a type annotation only when nothing else works, and say why.
- inline single-line helpers that have only one call site.
- check installed dependency source or published types before calling an external api. never guess signatures.
- never fix dependency-related breakage by removing or downgrading working code. upgrade the dependency instead.
- always ask before removing functionality or code that appears intentional.
- do not preserve backward compatibility unless the user asks. greenfield repo.

## verification

- after code changes (not docs-only): run the repo's lint/typecheck commands with full output and fix every error and warning before proposing a commit.
- never run builds or the full test suite unless the user asks.
- if you create or modify a test file, run it and iterate on test or implementation until it passes.
- write ad-hoc scripts to a temp file (for example `/tmp/opencode`), run, edit if needed, remove when done. never embed multi-line scripts in bash commands.

## dependencies

- treat dependency and lockfile changes as reviewed code. pinned exact versions only.
- install with lifecycle scripts disabled (`--ignore-scripts` equivalent) unless the user asks. a new dependency that ships install scripts needs explicit approval before it enters the lockfile.

## git

multiple agent sessions may run in this repo at the same time, each modifying different files. operations touching unstaged, staged, or untracked files outside your own changes stomp other sessions' work.

committing:

- never commit or push anything without explicit approval from the user for that exact action. propose the change, then wait.
- only stage files you changed in this session, by explicit path (`git add <path1> <path2>`). never `git add -a` or `git add .`.
- before committing, run `git status` and verify the staged set contains only your files.
- all commits are lowercase, short, and concise. format: `{feat|fix|docs|chore}: <imperative summary>`. imperative mood ("add depth anchoring", never "added" or "adds"), no period at the end, no emojis, one logical change per commit.

never run (destroys other sessions' work or bypasses checks):

- `git reset --hard`, `git checkout .`, `git clean -fd`, `git stash`, `git add -a`, `git add .`, `git commit --no-verify`

rebase conflicts:

- resolve conflicts only in files you modified. if a conflict appears in a file you did not modify, abort and ask the user.
- never force push.

## github

- inspect prs without moving the worktree: `gh pr view`, `gh pr diff`, `gh api`, and `git show <ref>:<path>` against fetched refs. switch branches only when the user explicitly asks.
- write issue/pr comments to a temp file and post with `--body-file`. keep comments concise, technical, in the user's tone.
- when closing an issue from a commit, include `fixes #<number>` (repeat the keyword per issue; a shared keyword closes only the first).

## research discipline

- speed is a feature: the copilot runs against a live camera feed. measure frame time before and after any change to the per-frame path. correctness alone does not justify a slower loop.
- every experiment result must be reproducible. record the exact command, config, input data, and environment next to the result.
- document why beside every non-trivial function whose purpose is not obvious from its name and types. future readers should understand the decision without reconstructing the reasoning.
- one-time scripts (data conversion, dataset prep) run once, then get deleted or promoted into proper modules. nothing migration-shaped keeps running on startup just in case.
- "mvp", "fallback", or "safety net" is not a reason to keep glue code. name the exact gap it covers, cite the source, and delete the path when the gap closes.
- do not invent constants. use library defaults first; add a timeout, threshold, or magic number only when a measured failure or documented limit requires it, and explain why that exact value is correct.

## academic and medical writing

- every factual claim carries a citation to a primary source. if you have not at least read the abstract, do not cite it.
- never invent references, statistics, or findings. if a number cannot be verified, mark it unverified or drop it entirely.
- quantitative claims carry their uncertainty: sample size, error measure, and spread where available. a bare average is not a result.
- match claim strength to evidence. "suggests" for a single study; "demonstrates" only for replicated controlled results. no causal language from correlational data.
- the system advises qualified professionals only. docs never describe it as diagnostic, autonomous, or clinically validated until each of those is literally true. regulatory status stays stated as what it is, not what it might become.
- use standard radiography vocabulary (projection, central ray, sid, kvp, mas, aec) consistently, and define every abbreviation at first use in any document.
- methods descriptions must allow independent reproduction: hardware, software versions, parameters, data splits, all recorded.
- respect dataset licenses and access terms (mimic-cxr requires credentialing and carries usage obligations; chexpert has its own license). record license and conditions beside every dataset used.
- human-subject data collection needs ethics approval before acquisition, without exception. even retrospective public data gets documented provenance: where it came from, under what terms, what it may be used for.
- keep speculation out of results. label opinions, hypotheses, and open questions explicitly so they never read as findings.

## skills

- invoke skills only after understanding the problem surface. read the relevant files, confirm what the task touches, then decide whether a skill applies. if you invoke one, state which and why it fits the verified surface.
- when listing skills to the user, present it as a check: name only ones whose triggers match what you verified about the task. never dump the full list.

## terminology

- centering point: the anatomical landmark the central ray must pass through for a given projection.
- technique profile: department-owned config of centering points, tolerances, and exposure steps, edited through conversation by an agent, read at runtime by deterministic code only.
- detector plane: the image receptor surface used to anchor monocular depth scale.

## user override

if the user's instructions conflict with any rule here, ask for explicit confirmation before overriding. only then execute.
