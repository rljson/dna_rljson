---
name: gg-publish
description: Releases a reviewed ticket with `gg do publish` once the user says "publish". Use when the user says "/gg-publish", "publish" or asks to release the ticket.
---

# Publish

`gg do publish` merges the pull requests, publishes to the registry and
creates and pushes the version tags. In the rljson repos you run it
yourself, once the user has said "publish" for this ticket. The user types
nothing: the npm, GitHub and Azure credentials of this machine let gg run
without a prompt.

## 1. Check the preconditions

- The user said "publish" for this ticket.
- Every repo of the ticket is committed and pushed.
- The pull requests created by `gg do review` are green.
- Every repo with `doc/guides/blog-guide.md` holds the post of this ticket
  in `doc/blog/<yyyy>`. If one is missing, go back to `/gg-review`.
- `npm whoami` answers without a prompt. If it asks for a login or a
  one-time password, stop and tell the user.

## 2. Configure the publish

Write per repo into `.gg/publish_config.json` (see the development guide):

- `mergeMessage` — the pull request title and merge commit message
- `versionIncrement` — `patch`, `minor` or `major`, matching what the
  ticket changed

`gg do publish` takes these values without asking. Never run
`gg do configure-publish`, it is interactive. Check that `CHANGELOG.md`
reads well.

## 3. Publish

From the ticket folder, without a terminal attached so gg asks nothing:

```bash
gg do publish < /dev/null
```

- gg waits for every pull request to merge and never gives up on a red
  one: watch the pull requests while it runs, and stop it if a check fails.
- Without a terminal gg keeps the ticket. Run `/gg-cleanup` afterwards,
  and ask the user before deleting anything.
- If it stops half way, fix the cause and resume with
  `gg do publish --continue < /dev/null`.

## 4. Report

Per repo: the released version, the merged pull request and the pushed
tag. Check each npm version with `npm view <package>@<version> version`;
the registry can lag a few minutes behind the upload.

## Important

- Never publish without the user's "publish" for this ticket.
- Never write versions or tags by hand.
