# SSH ControlMaster

ControlMaster multiplexes SSH connections so subsequent calls to the same host reuse an existing TCP+auth session instead of opening a new one. With FIDO2 / YubiKey keys this is especially useful — the first connection requires a touch, but every subsequent connection within the `ControlPersist` window reuses the master socket with no further touches.

This directory is keycutter's home for the ControlMaster feature: the config file that turns it on, the README you're reading, and the runtime sockets it produces.

## STRUCTURE

    controlmaster/
    ├── README.md          # this file
    ├── controlmaster.conf # SSH config block that enables multiplexing
    └── sockets/           # runtime multiplex sockets (one per host:port:user)

`controlmaster.conf` is loaded into your SSH config via the `Include keycutter/controlmaster/controlmaster.conf` directive in `keycutter.conf` (the keycutter main config).

`sockets/` holds the runtime sockets created by `ssh` itself when a multiplex master is established. Each socket file is named `<user>@<host>:<port>` and represents one open master session. Sockets are machine-local runtime state — gitignored, never committed.

## CONFIGURATION

The shipped `controlmaster.conf` enables multiplexing for GitHub and a placeholder set of personal hosts:

    Host github.com github.com_* laptop desktop homeserver
      ControlMaster auto
      ControlPath ~/.ssh/keycutter/controlmaster/sockets/%r@%h:%p
      ControlPersist 5m
      ServerAliveInterval 10
      ServerAliveCountMax 3

Replace `laptop desktop homeserver` with your real personal hostnames so multiplexing kicks in for them.

Key settings:

- **`ControlMaster auto`** — open a master if one isn't already running; reuse it otherwise.
- **`ControlPath ~/.ssh/keycutter/controlmaster/sockets/%r@%h:%p`** — where the socket file lives. The `%r@%h:%p` expands to `<user>@<host>:<port>` so each `(user, host, port)` triple gets its own socket.
- **`ControlPersist 5m`** — after the last client disconnects, keep the master alive for 5 minutes so a quick follow-up connection still gets reuse. Adjust to taste; longer means more reuse but a wider session-piggyback window.

## SECURITY CONSIDERATIONS

ControlMaster is a convenience-vs-isolation trade-off. Things to be aware of:

- **Socket permissions.** The socket file is created with Unix permissions that only your user can read or write. SSH refuses to use a master socket whose ownership or permissions are wrong.
- **Session piggyback during the persist window.** While a master is alive, anything else running as your user (a stray script, an unexpected process) can open a new session over the existing master *without* re-authenticating. The window closes when the persist timer expires or the master is explicitly killed (`ssh -O exit <host>`).
- **FIDO2 keys themselves are safe.** A YubiKey-backed key cannot be stolen — it's a hardware-bound key handle. ControlMaster only widens the window in which already-authenticated sessions can be reused; it doesn't change what an attacker who somehow lands on your machine could *steal*.
- **`sockets/` is gitignored.** The runtime sockets are machine-local and shouldn't be synced across machines. The `.gitignore` at the top of the keycutter tree excludes `controlmaster/sockets/`.

## DISABLING / OPTING OUT

Two ways to opt out:

- **Per-host:** remove the host from the `Host` line in `controlmaster.conf`, or add an explicit `Host <name> ControlMaster no` block earlier in your SSH config (first match wins).
- **Globally:** uncomment the trailing `Host *` block in `controlmaster.conf`, which sets `ControlMaster no` for everything except the explicit allow-list above.

To close an existing master without waiting for the persist timer:

    ssh -O exit <host>     # graceful exit
    ssh -O check <host>    # is a master running?

## RELATED

- `~/.ssh/keycutter/agents/` — the *other* socket directory. Holds ssh-agent sockets per identity bundle, a different concern entirely (authentication isolation, not connection multiplexing). See `agents/README.md`.
- `~/.ssh/keycutter/keycutter.conf` — the main SSH config that `Include`s this file.
