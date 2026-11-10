# logind-session

Fail-closed systemd-logind session resolve and inhibitor RAII.

Session resolution order:

1. `GetSessionByPID` (pid `0` = calling process). The D-Bus method returns an object path only.
2. `GetSession($XDG_SESSION_ID)` when that variable is set and non-empty
3. `ListSessions` scored for the calling uid (class=user +1, graphical type +2, active +4 / online +1)

The manager object path `/org/freedesktop/login1` is never a session path. There is no placeholder path.

`Inhibitor` holds the logind inhibit fd. Drop releases it. Callers pass `who` (canonical executable/service identity).

Published from CI on a `v*` tag (`CARGO_REGISTRY_TOKEN` org secret). Do not
`cargo publish` from a laptop.

```toml
logind-session = "0.3.0"
```
