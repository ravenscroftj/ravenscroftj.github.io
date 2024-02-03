---
created: 2024-01-28T16:27
updated: 2024-02-03T08:20
---

## Troubleshooting Syncthing and systemd
#### Error  `Failed to enable unit: multi-user.target: Identifier removed`
- You have to start syncthing as a user service (per logged-in user) rather than a system-wide thing
- Run `systemctl --user start syncthing.service` (without sudo)
