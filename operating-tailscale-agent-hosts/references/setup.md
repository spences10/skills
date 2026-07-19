# Host Setup

## 1. Establish the private path

Install Tailscale on both machines, join the same tailnet, and confirm the worker is online:

```bash
tailscale status
tailscale ping <worker-hostname>
```

Enable Tailscale SSH on the worker:

```bash
sudo tailscale set --ssh
```

Connect using the worker's real local username:

```bash
ssh <user>@<worker-hostname>
```

A refused port usually means neither Tailscale SSH nor a regular SSH daemon is accepting the connection. A “failed to look up local user” error means the requested Linux account does not exist on the worker.

## 2. Make boot unattended

Verify services rather than only checking installed packages:

```bash
systemctl is-enabled tailscaled
systemctl is-active tailscaled
systemctl is-enabled NetworkManager
```

For a dedicated always-on worker, disable system sleep only after the owner approves:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

Undo with `systemctl unmask` using the same targets.

### Wi-Fi before desktop login

Prefer wired Ethernet for an unattended server. Making Wi-Fi available before login moves the credential from a user's desktop wallet into a root-protected, system-wide NetworkManager profile. Only do this on a trusted, physically secure worker whose administrators may access that credential.

If the worker appears only after a graphical login, inspect the active connection without printing its secret:

```bash
nmcli -g connection.id,connection.permissions,connection.autoconnect,802-11-wireless-security.psk-flags connection show '<connection>'
```

`psk-flags=1` means a user secret agent such as KDE Wallet owns the password. Store it as a system connection from the worker's own terminal; have the user enter the PSK invisibly and never place it in agent-visible output.

```bash
read -rsp 'Wi-Fi password: ' WIFI_PSK; echo
sudo nmcli connection modify '<connection>' \
  802-11-wireless-security.psk "$WIFI_PSK" \
  802-11-wireless-security.psk-flags 0 \
  connection.permissions '' \
  connection.autoconnect yes
unset WIFI_PSK
```

Reboot and test before anyone logs into the desktop. If networking still waits, investigate disk encryption, firmware prompts, or NetworkManager logs.

## 3. Install worker tools

Use the distribution's official packages where possible:

```bash
sudo pacman -S tmux docker docker-compose
sudo systemctl enable --now docker
sudo usermod -aG docker "$USER"
```

A new login or reboot is required for Docker group membership. Validate daemon access without sudo:

```bash
docker info
docker compose version
```

Install runtime/version managers and the chosen agent distribution normally on the worker. Do not copy executable caches from another machine.

## 4. Configure Tailscale SSH policy

Keep periodic check mode when stronger interactive assurance is desired. To avoid recurring browser checks, add a narrow `accept` rule:

- source: one trusted tailnet identity or device
- destination: one worker
- destination user: one non-root Linux account
- check mode: off

Do not turn a broad `autogroup:member → autogroup:self → root` rule into `accept`.
