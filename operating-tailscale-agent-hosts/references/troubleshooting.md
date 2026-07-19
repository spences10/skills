# Troubleshooting

## Tailscale responds but SSH does not

```bash
tailscale status
tailscale ping <worker>
ssh -o ConnectTimeout=10 <user>@<worker>
```

- `Connection refused`: no SSH service is accepting traffic.
- Timeout while Tailscale ping succeeds: inspect SSH policy, worker reachability, and Tailscale SSH state.
- Additional-check URL: the matching SSH rule uses check mode.
- Local-user lookup failure: use an existing Linux username, not the tailnet/GitHub identity.

MagicDNS can fail transiently while the Tailscale IP still works. Do not bypass host-key verification casually when switching names or addresses.

## Worker appears only after graphical login

Check these independently:

- NetworkManager enabled and active
- Wi-Fi connection set to autoconnect
- connection permissions empty/all-users
- Wi-Fi `psk-flags=0`
- Tailscale enabled and active
- no disk-encryption or firmware prompt blocking boot

A Tailscale daemon cannot provide access until the underlying network is online.

## Worker sleeps or disappears

Inspect sleep target state:

```bash
for unit in sleep.target suspend.target hibernate.target hybrid-sleep.target; do
  printf '%s: ' "$unit"
  systemctl is-enabled "$unit" || true
done
```

Expected for a deliberately disabled worker: `masked`. Desktop power managers can also initiate sleep; system-level masks provide the final guard.

## OAuth fails over SSH

Do not transcribe wrapped URLs from screenshots. PKCE URLs are exact and short-lived; a single changed character or a callback from an older attempt returns HTTP 400.

Use tmux when terminal selection is unreliable:

```bash
tmux new -s auth
<tool> auth login
```

Leave the URL visible and capture the pane exactly if needed. Keep each callback paired with the same still-running login attempt. A line saying “Login successful” means later retries are unnecessary; verify status before restarting authentication.

## Agent opens but cannot call a model

A TUI opening proves only that the program started. Validate with a minimal headless request. Check the selected provider/model and authenticate that exact runtime on the worker. Provider credentials copied from another machine may be stale or unusable.

## pnpm dlx requests build approval

Modern pnpm can require explicit approval for dependency lifecycle scripts. Do not select packages blindly. Verify they are expected dependencies, then use the supported `--allow-build=<package>` flags for a deterministic launcher where appropriate.

## Case/GPU fans

GPU telemetry does not imply motherboard fan control. Check `sensors` and `/sys/class/hwmon` for `fan*_input` or `pwm*`. If absent, case fans are likely controlled by firmware or a separate hub; configure their curve in BIOS/UEFI rather than forcing unsupported software control.
