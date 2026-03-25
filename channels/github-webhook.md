# Push Event — Documentation Changes

The JSON webhook payload is appended directly after these instructions
in the user message. Parse it inline — do not fetch, list, or search
for the payload elsewhere. Do NOT use tools to read the payload.

You received a GitHub webhook for a push event indicating new commits
were pushed to the repository.

## Scope

Extract the `ref`, `commits`, and `repository.full_name` from the
payload. Only proceed if the push is to the default branch (typically
`refs/heads/main` or `refs/heads/master`). For pushes to other
branches, stop and say "No action needed — push is not to the default branch."

All actions are scoped to the files changed in the commits listed in
this payload.

## Steps

1. Extract `ref`, `repository.full_name`, `commits`, and `head_commit`
   from the payload.
2. If the push is not to the default branch, stop — no action needed.
3. Scan the `added` and `modified` arrays in each commit for
   documentation files (`.md`, `.mdx`, `.txt`, `.rst`, or files under
   a `docs/` directory). Ignore `removed` files.
4. If no documentation files are found across any commits, stop — no
   action needed.
5. Deduplicate the file list. If the same file appears in multiple
   commits, process it once.
6. Follow the Workflow in SOUL.md starting from Phase 2 (Fetch Updated
   Content) using the deduplicated file list.
