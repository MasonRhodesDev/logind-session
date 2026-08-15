# hypr-logind

Fail-closed systemd-logind session resolve and inhibitor RAII for the hypr suite.

Session resolution order:

1. `GetSessionByPID` (pid `0` = calling process). The D-Bus method returns an object path only.
2. `GetSession($XDG_SESSION_ID)` when that variable is set and non-empty
3. `ListSessions` scored for the calling uid (class=user +1, graphical type +2, active +4 / online +1)

The manager object path `/org/freedesktop/login1` is never a session path. There is no placeholder path.

`Inhibitor` holds the logind inhibit fd. Drop releases it. Callers pass `who` (canonical executable/service identity).

This public repo exists so packaged tools can git-depend on the crate.
hypr-commons is private. crates.io publish waits on a registry token.

```toml
hypr-logind = { git = "https://github.com/MasonRhodesDev/hypr-logind", rev = "<sha>" }
```
