# autosuspend.sh
 
A simple bash script that automatically suspends your system after a period of inactivity, but only if nothing useful is actually happening.
 
## How it works
 
Every 60 seconds (configurable), the script checks how long the system has been idle using `xprintidle`. If the idle time exceeds the threshold, it runs a series of checks before suspending:
 
- **Inhibit file** — if `/tmp/no-suspend` exists, suspend is skipped
- **SSH session** — if someone is connected remotely, suspend is skipped
- **Active download** — if network throughput exceeds the threshold, suspend is skipped
- **Audio playing** — if PipeWire/PulseAudio has a running sink, suspend is skipped
If none of those conditions are met, it turns off the display and suspends the system.

## Dependencies
 
- `xprintidle` — reads keyboard/mouse idle time
- `xset` — turns off the display before suspend
- `pactl` — checks audio sink state (works with both PipeWire and PulseAudio)
- `systemctl` — triggers suspend
- `ip`, `awk` — network interface detection

## Installation

Download the script directly with `wget`:

```bash
wget https://raw.githubusercontent.com/diegorezm/autosuspend.sh/refs/heads/main/autosuspend.sh
chmod +x autosuspend.sh
mv autosuspend.sh ~/.local/bin/
```

To make it available system-wide, move it to a directory in your `$PATH`

## License
 
MIT
