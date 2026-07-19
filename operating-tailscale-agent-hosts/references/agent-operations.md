# Agent Operations

## Persistent sessions with tmux

Create one named session per responsibility:

```bash
tmux new -s general
tmux new -s issue-123
```

Detach without stopping the process: press `Ctrl-b`, release, then press `d`.

```bash
tmux ls
tmux attach -t issue-123
tmux kill-session -t issue-123
```

For terminals that support modified Enter keys, configure:

```tmux
set -g extended-keys on
```

Apply it to a running server with `tmux set-option -g extended-keys on`; avoid killing a server that contains active work.

Read-only monitoring does not interrupt an agent:

```bash
tmux capture-pane -p -t issue-123 -S -100
git -C <worktree> status --short --branch
```

Do not send keys or signals merely to check progress.

## Isolate concurrent changes

Update a clean primary checkout, then create a branch and worktree per mutating agent:

```bash
git fetch origin --prune
git pull --ff-only origin main
git worktree add -b feature/issue-123 ../worktrees/project-issue-123 origin/main
```

Give each agent explicit ownership, acceptance criteria, validation requirements, and delivery boundaries. State whether it may commit, push, open a PR, publish, or merge; never infer those approvals.

## Authentication

Authenticate each tool on the worker. A successful login for one CLI does not authenticate another agent runtime.

Use browser/device flows from SSH:

1. Start login on the worker.
2. Keep the remote prompt open.
3. Open the displayed URL on a trusted local browser.
4. Enter the one-time code or paste the callback code into the same remote prompt.
5. Verify with the tool's status command and a minimal real request.

Copying an auth file can fail because refresh tokens may rotate, bind to a client, or require a new device flow. Prefer fresh authentication. If a credential file must be transferred, copy it directly without reading it into model context, set mode `0600`, and verify functionality afterward.

## GitHub delivery

Verify both Git transport and API authentication:

```bash
ssh -T git@github.com
gh auth status
gh repo view <owner>/<repo>
```

Git over SSH can work while `gh` remains unauthenticated. Agents need `gh` authentication to create issues or pull requests remotely.

## Remote development servers

Prefer keeping the application on worker localhost:

```bash
pnpm dev
tailscale serve --bg 5173
```

Open the private HTTPS URL from another tailnet device. As a fallback, bind explicitly and use the worker hostname:

```bash
pnpm dev -- --host 0.0.0.0
# open http://<worker-hostname>:5173
```

Binding to `0.0.0.0` may expose the service to other connected networks; check host firewall and application trust assumptions.
