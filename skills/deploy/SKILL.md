---
name: deploy
description: Deploy an AGDA-managed Railway project by bumping the project version, merging release or hotfix work to main, adding a version tag, pushing refs, and verifying the Railway deployment. Use when the user asks to deploy, publish, ship, tag, promote a release, or finish a hotfix outside the normal release procedure.
---

# AGDA: Deploy

Use this skill after release notes and backlog packaging are done. Use it when the user wants a Railway release or a Railway hotfix shipped outside the normal release procedure.

This skill is Railway-based. Do not use it for a project that deploys through another platform.

## Preconditions

1. Confirm the worktree state with `git status --short --branch`.
2. Identify the current branch and whether this is:
   - normal release: deploy from `develop` to `main`;
   - hotfix: deploy the current hotfix branch directly to `main` unless the user says otherwise.
3. Locate the real runtime version source before editing. Do not assume `package.json` is authoritative.
4. Pull or fetch remotes only when needed to verify branch/tag state.
5. Confirm the Railway project and production service that deploy the `main` branch.

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

6. Confirm that Railway deploys the pushed `main` commit to the production service.
7. Check the Railway deployment result. Stop and report the deployment error if Railway does not report success.
8. Run the production smoke check defined by the project.
9. Switch back to `develop`.
10. For a hotfix, merge `main` back into `develop` after the deploy unless the branch model clearly keeps hotfixes separate.
11. Verify:

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
- Railway deployment result;
- production smoke-check result;
- final checkout branch.

End with:

```text
Recommended next skill: status-check
```
