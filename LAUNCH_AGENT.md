## LaunchAgent: Daily GLaDOS Check‑in (Quick Guide)

- **Label**: `com.admin.gladoscheckin`
- **Script**: `/Users/admin/bin/glados_checkin.sh`
- **Schedule**: daily 14:00 (local). Runs after login, survives reboot.
- **Logs**: `/Users/admin/bin/gladoscheckin.out` (stdout), `/Users/admin/bin/gladoscheckin.err` (stderr)
- **Plist**: `/Users/admin/Library/LaunchAgents/com.admin.gladoscheckin.plist`

**Use**: Stay logged in and keep the Mac awake at 14:00. No manual action needed.

**Verify**:
```bash
launchctl print gui/$UID/com.admin.gladoscheckin | egrep -A2 "descriptor|runs|last exit code"
```

**Logs**:
```bash
tail -n50 /Users/admin/bin/gladoscheckin.out; tail -n50 /Users/admin/bin/gladoscheckin.err
stat -f "%Sm %N" -t "%Y-%m-%d %H:%M:%S" /Users/admin/bin/gladoscheckin.out /Users/admin/bin/gladoscheckin.err
```

**Run now**:
```bash
launchctl kickstart -k gui/$UID/com.admin.gladoscheckin
```

**Change time**:
```bash
open -e /Users/admin/Library/LaunchAgents/com.admin.gladoscheckin.plist
launchctl bootout gui/$UID /Users/admin/Library/LaunchAgents/com.admin.gladoscheckin.plist
launchctl bootstrap gui/$UID /Users/admin/Library/LaunchAgents/com.admin.gladoscheckin.plist
launchctl enable gui/$UID/com.admin.gladoscheckin
```

**Update cookie**:
```bash
open -e /Users/admin/bin/glados_checkin.sh; launchctl kickstart -k gui/$UID/com.admin.gladoscheckin
```

**Disable/remove**:
```bash
launchctl disable gui/$UID/com.admin.gladoscheckin   # or: launchctl enable ...
launchctl bootout gui/$UID /Users/admin/Library/LaunchAgents/com.admin.gladoscheckin.plist
```

**Troubleshoot**:
```bash
plutil -lint /Users/admin/Library/LaunchAgents/com.admin.gladoscheckin.plist
```
