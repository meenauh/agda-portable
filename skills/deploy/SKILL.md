---
name: deploy
description: Deploy an AGDA-managed project by bumping the project version, merging release or hotfix work to main, adding a version tag, pushing develop/main/tag refs, and returning the checkout to develop. Use when the user asks to deploy, publish, ship, tag, promote a release, or finish a hotfix outside the normal release procedure.
---

# AGDA: Deploy

Use this skill after release notes/backlog packaging are done, or when the user explicitly wants a hotfix shipped outside the release procedure.

## Preconditions

1. Confirm the worktree state with `git status --short --branch`.
2. Identify the current branch and whether this is:
   - normal release: deploy from `develop` to `main`;
   - hotfix: deploy the current hotfix branch directly to `main` unless the user says otherwise.
3. Locate the real runtime version source before editing. Do not assume `package.json` is authoritative.
4. Pull or fetch remotes only when needed to verify branch/tag state.

Stop before destructive cleanup, force-push, or overwriting an existing tag unless the user explicitly approves it.

## Version

- Normal release procedure: bump the minor version and reset patch to zero.
- Hotfix outside release procedure: bump the patch version.
- Major version: only when explicitly requested.

Edit only the file or files that are the project's established version source. If the version source is unclear, search imports/config references before changing anything.

## Deploy Flow

1. Commit the version bump or confirm it is already committed.
2. Switch to `main`.
3. Merge:
   - normal release: merge `develop` into `main`;
   - hotfix: merge the current hotfix branch into `main`.
4. Create the annotated version tag on the deployed commit:

```bash
git tag -a vX.Y.Z -m "vX.Y.Z"
```

5. Push branches and tags:

```bash
git push origin develop main
git push origin vX.Y.Z
```

6. Switch back to `develop`.
7. For a hotfix, merge `main` back into `develop` after the deploy unless the branch model clearly keeps hotfixes separate.
8. Verify:

```bash
git status --short --branch
git log -1 --format="%h %s" main
git log -1 --format="%h %s" vX.Y.Z
```

## Output

Report:

- deployed version;
- version source changed;
- branches merged;
- tag pushed;
- final checkout branch.

End with:

```text
Recommended next skill: status-check
```
